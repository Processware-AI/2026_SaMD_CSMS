# 전용 AI Agent 프레임워크 설계 제안

> 현재 Claude Code 하네스로 검증된 개념을 **독립 실행 프레임워크**로 승격시키는 방향 설계안.
> 작성일: 2026-04-17 · 상태: draft (depth 검토 예정)
> 관련: [[표준프로세스_구성원칙]], 현 하네스(`.claude/agents/`, `.claude/commands/`)

---

## 1. 먼저 확정할 선택지

| 축 | 옵션 A | 옵션 B | 옵션 C |
|---|---|---|---|
| **사용자 범위** | 내부 컨설팅 툴 | 컨설팅 펌 B2B | 멀티테넌트 SaaS |
| **배포 형태** | CLI / 데스크탑 | 온프렘 서버 | 클라우드 |
| **데이터 저장** | 로컬 Vault만 | Vault + 서버 DB | 클라우드 DB + Git |
| **진입 UI** | CLI | 웹 대시보드 | Obsidian 플러그인 |
| **LLM 모델** | Claude 전용 | 멀티 프로바이더 | BYO Key |

어느 조합을 노리냐에 따라 프레임워크 규모가 3배 이상 달라짐.
**추천 진화 경로**: 내부 툴 → B2B 온프렘 → SaaS (단계적)

---

## 2. 필수 구성 요소 (프레임워크 무관)

```
┌──────────────────────────────────────────────────────────┐
│                   Entry Points                            │
│    CLI   │   HTTP API   │   Web UI   │  Obsidian Plugin  │
└────────────────────────┬─────────────────────────────────┘
                         │
┌────────────────────────▼─────────────────────────────────┐
│                 Orchestrator (Graph/Plan)                 │
│   · Pipeline DSL (analyze→design→write→trace→QA)         │
│   · Human-in-the-Loop 게이트 (심사원 검수)                │
│   · Retry / Backoff / Partial resume                      │
└────────────────────────┬─────────────────────────────────┘
                         │
      ┌──────────────────┼──────────────────┐
      │                  │                  │
┌─────▼──────┐   ┌──────▼──────┐   ┌───────▼────────┐
│   Agent    │   │    Tool     │   │    Memory      │
│  Registry  │   │  Registry   │   │   / RAG        │
│            │   │  (MCP 호환) │   │                │
│ analyzer   │   │ vault-fs    │   │ 표준 카탈로그  │
│ designer   │   │ obsidian    │   │ 요구사항 DB    │
│ wi-writer  │   │ web-search  │   │ 과거 산출물    │
│ mapper     │   │ git-commit  │   │ 조직별 테일러링│
│ qa-review  │   │ legal-db    │   │ (pgvector)     │
└────────────┘   └─────────────┘   └────────────────┘
                         │
┌────────────────────────▼─────────────────────────────────┐
│               Cross-Cutting Services                      │
│  Audit Log · Tracing(OTel) · RBAC · Secrets · Billing    │
└──────────────────────────────────────────────────────────┘
                         │
┌────────────────────────▼─────────────────────────────────┐
│                    Storage                                │
│  Vault(MD) │ Postgres │ Object(S3) │ Git │ Vector(pgv)   │
└──────────────────────────────────────────────────────────┘
```

**핵심 포인트**
- **MCP 호환 Tool 레지스트리** — Obsidian, GitHub, 법령DB, ISO.org 같은 외부소스 플러그인으로
- **Audit Log는 필수** — 심사증적으로 직접 쓰일 수 있어야 함(MAT-005와 연동)
- **Human-in-the-Loop** — 심사원/Process Owner 가 승인해야 다음 단계 진행
- **Vault를 Git + DB 이중 저장** — 버전 추적(Git) + 쿼리(DB)

---

## 3. 프레임워크 비교

| 프레임워크 | 장점 | 단점 | 적합도 |
|---|---|---|---|
| **Claude Agent SDK** | 현 하네스 개념 그대로 이식. 서브에이전트·MCP 네이티브 | Claude 종속 | ★★★★★ (1순위) |
| **LangGraph** | 그래프 기반 상태머신·재개·HITL 강력 | 학습곡선·상태모델 복잡 | ★★★★ (복잡 워크플로우면) |
| **CrewAI** | 역할 기반 다중에이전트 직관적 | 프로덕션 성숙도 부족 | ★★ |
| **AutoGen** | 대화형 에이전트 강점 | 구조적 파이프라인엔 과잉 | ★★ |
| **직접 구축** | 최대 자유도 | 6개월+ 재발명 | ★ (비추) |

**추천: Claude Agent SDK + LangGraph 하이브리드**
- 에이전트 실행: Claude Agent SDK (서브에이전트/MCP 패턴 그대로)
- 파이프라인 오케스트레이션: LangGraph (체크포인트·재개·HITL)

MVP 단계는 **Claude Agent SDK 전용**도 충분함.

---

## 4. 제안 아키텍처 (Python 기준)

```
spx/                              ← 프레임워크 패키지명 예시 (SPX=Standard Process eXpert)
├── core/
│   ├── orchestrator.py          ← 파이프라인 엔진
│   ├── agent_registry.py
│   ├── tool_registry.py         ← MCP 서버 로더
│   └── state.py                 ← 체크포인트
├── agents/                      ← 현 .claude/agents/ 포팅
│   ├── standard_analyzer.py
│   ├── process_designer.py
│   ├── wi_tmp_writer.py
│   ├── traceability_mapper.py
│   └── qa_reviewer.py
├── tools/                       ← MCP 서버들
│   ├── vault_fs/                ← Obsidian vault 읽기/쓰기
│   ├── standards_catalog/       ← ISO/IEC/KS 메타DB
│   ├── legal_kr/                ← 국가법령정보센터 API
│   └── git_sync/                ← vault ↔ Git
├── standards/                   ← 표준별 지식팩
│   ├── iso9001/
│   ├── iso27001/
│   └── ...
├── templates/                   ← T03~T13 템플릿
├── api/                         ← FastAPI 엔드포인트
├── cli/                         ← typer CLI (spx build-standard ISO9001)
├── web/                         ← Next.js 대시보드 (선택)
└── audit/                       ← 감사증적 로거 (OTel)
```

**데이터 레이어**
- **Postgres**: 테넌트·프로젝트·표준 카탈로그·실행 이력
- **Git (서버사이드 Gitea 등)**: 각 테넌트의 vault 버전 관리
- **pgvector**: 표준 조항·법령·과거 산출물 RAG
- **S3 호환**: 첨부증적·대용량 REC

---

## 5. MVP 로드맵 (4단계)

### Phase 1. 코어 포팅 (핵심 기능 확보)
- 현 `.claude/agents/*.md` → Python 에이전트 클래스로 이식
- Claude Agent SDK로 서브에이전트 호출 재현
- CLI 1개: `spx build-standard ISO9001 --vault ./vault`
- Obsidian vault 쓰기 기능 검증

### Phase 2. 프레임워크화
- Orchestrator + 체크포인트 (실패 지점부터 재개)
- MCP 기반 Tool Registry
- 감사증적 (JSONL + OTel)
- 표준 카탈로그 DB (ISO/IEC/KS 메타)

### Phase 3. B2B 배포 가능한 상태
- HTTP API + 인증(RBAC)
- Docker Compose 온프렘 배포 키트
- 웹 대시보드 (실행 상태·산출물 브라우저·심사증적)
- Human-in-the-Loop 승인 UI

### Phase 4. SaaS화
- 멀티테넌트·결제·Git 분리
- RAG 지식팩 마켓플레이스(표준별 프리셋 판매)

---

## 6. 기술적 도전 포인트 (미리 알아야 할 것)

| 이슈 | 대응 |
|---|---|
| LLM 비환각 보장 | 각 에이전트 출력을 **스키마 검증** + RAG 근거 링크 강제 |
| 대용량 표준 원문 | 조항 단위 청크 + hybrid search (BM25 + vector) |
| 개정판 추적 | 표준 카탈로그에 `version`·`effective_date`·`superseded_by` |
| 고객 데이터 격리 | 테넌트별 vault·DB 스키마 분리, 키 BYO 옵션 |
| 심사 증적 무결성 | Git hash + 서명(sigstore) 로 추적증적 |
| AI 결과 책임 | 모든 산출물 `generated_by: claude-opus-4-6`, `reviewed_by: human` 필드 |

---

## 7. 즉시 결정 필요한 항목

1. **언어**: Python(SDK 1순위) vs TypeScript vs 양쪽?
2. **타겟 고객 최소단위**: 1인 컨설턴트 vs 10인 펌 vs 100인 기업
3. **Obsidian 유지 여부**: 계속 핵심 UI로 쓸지, 웹 UI로 대체할지, 둘 다 지원할지
4. **오픈소스 / 상용**: 코어는 OSS 두고 상용 부가기능(멀티테넌트·지식팩)만 판매할지
5. **단독 빌드 vs 파운데이션 활용**: 완전 자체 구현 vs Claude Agent SDK + LangGraph 조합

---

## 8. 결론 및 첫 수

**가능하다.** 현재 하네스는 이미 "설계 수준"에서 프레임워크의 씨앗이 거의 다 들어가 있음. 남은 것은 **실행 엔진을 Claude Code CLI 에서 떼어내는 것**. Claude Agent SDK 가 그 용도로 만들어진 도구이므로 포팅 비용은 예상보다 작음.

**가장 현실적인 첫 수**:
> "Python + Claude Agent SDK 로 현 `.claude/agents/*` 를 포팅 → CLI 1개로 ISO 9001 구축 재현 → 거기서부터 기능 확장"

→ 2~4주 내 Phase 1 MVP 가능.

---

## 9. 후속 심화 검토 주제 (다음 세션 용)

- [ ] (A) Phase 1 MVP 코드베이스 골격 생성 (디렉터리·주요 파일 스캐폴딩)
- [ ] (B) Claude Agent SDK vs LangGraph 상세 비교 + 의사결정
- [ ] (C) 멀티테넌트 SaaS 아키텍처 상세 (DB 스키마·격리 전략)
- [ ] (D) 지식팩(표준 카탈로그·RAG) 구조 설계
- [ ] (E) 감사증적 + HITL 워크플로우 상세
- [ ] (F) 사업화 연계 (사업 모델 문서와 이 설계안의 접점)

---

## 참고 관련 문서 (프로젝트 내)
- 전체 구성원칙: `vault/01_구성원칙/표준프로세스_구성원칙.md`
- 현 하네스 README: `README.md`
- 현 에이전트 정의: `.claude/agents/*.md`
- 문서체계·번호체계: `vault/00_공통관리/01_문서체계.md`, `02_문서번호체계.md`
