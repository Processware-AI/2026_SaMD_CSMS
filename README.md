# SaMD-CSMS 사이버보안 관리체계 구축 프로젝트

의료기기 소프트웨어(SaMD) 사이버보안 관리체계(CSMS)를 **IEC 81001-5-1 · FDA Premarket Cybersecurity 2023 · MDCG 2019-16** 기반으로 구축하는 문서 체계 프로젝트. Claude Code 에이전트 파이프라인으로 표준 요구사항을 분해하고, Obsidian Vault에 8종 문서 유형으로 자동 생성·관리한다.

---

## 적용 표준 및 규제

| 구분 | 문서 | 비고 |
|---|---|---|
| 국제 표준 | IEC 81001-5-1 | 의료 소프트웨어 사이버보안 활동 |
| 미국 규제 | FDA Premarket Cybersecurity Guidance (2023) | 시판 전 사이버보안 |
| 유럽 규제 | MDCG 2019-16 Cybersecurity | EU MDR/IVDR 지침 |

---

## 현재 구축 현황

| 유형 | 코드 | 설명 | 건수 |
|---|---|---|---|
| POL | 정책서 | 의료기기 사이버보안 방침·정책 | 6 |
| PRO | 절차서 | 보안 관리 업무 절차 | 11 |
| WI  | 업무지침서 | 실무 수행 상세 지침 | 60 |
| TMP | 템플릿 | 빈 양식 | 83 |
| EX  | 작성예시 | 교육용 샘플 | 83 |
| REF | 참고자료 | 표준·규제 요약 | 3 |
| MAT | 관리대장 | 추적성·목록·대조표 | 7 |

### 정책서 (POL)
| 코드 | 문서명 |
|---|---|
| POL-MDCS-001 | 의료기기 사이버보안 기본방침 |
| POL-MDCS-002 | 사이버보안 리스크관리 정책 |
| POL-MDCS-003 | 보안 개발수명주기(SDLC) 정책 |
| POL-MDCS-004 | 기술적·물리적 보안통제 정책 |
| POL-MDCS-005 | 침해행위 대응 정책 |
| POL-MDCS-006 | 취약점 관리 정책 |

### 절차서 (PRO)
| 코드 | 문서명 |
|---|---|
| PRO-MDCS-101 | 보안 문서화 관리 절차 |
| PRO-MDCS-201 | 사이버보안 리스크 관리 절차 |
| PRO-MDCS-301 | 보안 SDLC 절차 |
| PRO-MDCS-302 | SBOM 관리 절차 |
| PRO-MDCS-303 | 레거시 의료기기 관리 절차 |
| PRO-MDCS-401 | 접근통제 및 인증 관리 절차 |
| PRO-MDCS-402 | 보안 통신 및 암호화 관리 절차 |
| PRO-MDCS-403 | 데이터 및 파일 보안 관리 절차 |
| PRO-MDCS-501 | 보안 모니터링 및 로그 관리 절차 |
| PRO-MDCS-502 | 침해사고 대응 및 신고 절차 |
| PRO-MDCS-601 | 취약점 감시·공개·조치 절차 |

---

## 디렉터리 구조

```
2026_SaMD_CSMS/
├── .claude/
│   ├── agents/                      ← Claude Code 서브에이전트 정의
│   │   ├── standard-analyzer.md
│   │   ├── process-designer.md
│   │   ├── wi-tmp-writer.md
│   │   ├── traceability-mapper.md
│   │   └── qa-reviewer.md
│   └── commands/
│       └── build-standard.md        ← 오케스트레이터 슬래시 커맨드
└── vault/                           ← Obsidian Vault 루트
    ├── 00_MOC/                      ← Map of Content (전체 인덱스)
    ├── 00_공통관리/                 ← 문서체계·번호체계·용어집·파이프라인 규약
    ├── 01_구성원칙/                 ← 표준프로세스 구성원칙 (최상위 기준)
    ├── 02_표준/SaMD-CSMS/           ← 표준 작업 공간 (개요·요구사항분해·작업노트)
    ├── 03_POL_정책/                 ← POL-MDCS-001~006
    ├── 04_PRO_절차/                 ← PRO-MDCS-101~601
    ├── 05_WI_업무지침/              ← WI-* (60건)
    ├── 06_TMP_템플릿/               ← TMP-* (83건)
    ├── 07_EX_작성예시/              ← EX-* (83건)
    ├── 08_REC_기록/                 ← REC-* (운영 단계 생성)
    ├── 09_REF_참고자료/             ← IEC·FDA·MDCG 요약 (3건)
    ├── 90_MAT_통합매핑/             ← MAT-001~006 + SaMD-CSMS 추적성
    ├── 99_템플릿/                   ← Obsidian 문서 템플릿 (T03~T15)
    ├── 99_템플릿/_골든샘플/         ← POL/PRO/WI 품질 기준 샘플
    ├── 99_폐기_보관/                ← 만료·폐지 문서 아카이브
    └── _inputs_common/              ← 표준별 공통 입력자료
```

---

## 에이전트 파이프라인

```
/build-standard SaMD-CSMS
        │
        ▼
┌──────────────────┐   표준개요 / 요구사항분해 / REF / MAT-002
│ standard-analyzer│──────────────────────────────────────▶ 02_표준/, 09_REF/, 90_MAT/
└──────────────────┘
        │
        ▼
┌──────────────────┐   POL / PRO (정책서·절차서)
│ process-designer │──────────────────────────────────────▶ 03_POL_정책/, 04_PRO_절차/
└──────────────────┘
        │
        ▼
┌──────────────────┐   WI / TMP / EX + MAT-001 등록
│  wi-tmp-writer   │──────────────────────────────────────▶ 05_WI/, 06_TMP/, 07_EX/
└──────────────────┘
        │
        ▼
┌──────────────────┐   표준별 추적성 + MAT-001~006 갱신
│traceability-mapper│─────────────────────────────────────▶ 90_MAT_통합매핑/
└──────────────────┘
        │
        ▼
┌──────────────────┐   8종 유형 분리·링크 정합성 감사
│   qa-reviewer    │──────────────────────────────────────▶ 02_표준/SaMD-CSMS/99_QA리포트_*
└──────────────────┘
        │
        ▼
     MOC 갱신 + 완료 보고
```

---

## 사용법

### 1. Obsidian 열기
`vault/` 폴더를 Obsidian에서 **Open folder as vault**로 열기.

### 2. 입력자료 배치 (권장)
```
vault/02_표준/SaMD-CSMS/_inputs/
```
표준원문·법규·해설서·As-Is 문서를 투하. 상세 규칙: `vault/00_공통관리/05_입력자료_규칙.md`

### 3. 표준 편입 실행
```
/build-standard SaMD-CSMS
```

### 4. 중단된 실행 재개
```
/build-standard SaMD-CSMS --resume          # 현재 phase 부터 자동 재개
/build-standard SaMD-CSMS --from design     # design phase 부터 강제 재시작
/build-standard SaMD-CSMS --restart         # 기존 state 폐기 후 처음부터
```

### 5. 자가수정 루프 조정
```
/build-standard SaMD-CSMS --max-attempts 5  # 자가수정 최대 횟수
/build-standard SaMD-CSMS --skip-qa         # QA·자가수정 생략
```

> **주의**: `_inputs/` 없이 실행하면 LLM 추정 모드로 동작하여 감사 방어력이 낮습니다. 프로덕션 용도는 반드시 입력자료를 배치하세요.

---

## 문서 유형 8종

| 코드 | 유형 | 역할 |
|---|---|---|
| POL | 정책서 | 원칙·방침·책임 |
| PRO | 절차서 | 업무 흐름·관리 절차 |
| WI  | 업무지침서 | 실무 수행 상세 |
| TMP | 템플릿 | 빈 양식 |
| EX  | 작성예시 | 교육용 샘플 |
| REC | 기록본 | 실제 수행 증빙 |
| MAT | 매핑/관리대장 | 추적성·목록·대조표 |
| REF | 참고자료 | 외부 규정·가이드 요약 |

상세: `vault/00_공통관리/01_문서체계.md`

## 파일명 규칙

```
[유형]-[식별번호]_[문서명]_v[버전].md
```
예: `POL-MDCS-001_의료기기_사이버보안_기본방침_v1.0.md`

상세: `vault/00_공통관리/02_문서번호체계.md`

---

## 체크포인트·자가수정 (자동)

각 표준 편입 시 `vault/02_표준/SaMD-CSMS/_state.yaml` 이 자동 생성·갱신됩니다.
- phase 별 `pending → running → done` 이력
- QA Fail 시 `qa_failures[]` 에 담당 에이전트(`assigned_to`)·수정 범위(`fix_scope`) 기록
- 오케스트레이터가 담당 에이전트를 재호출하여 자동 수정 (최대 3회)
- 수동 개입 필요 시 `assigned_to: manual` 로 에스컬레이션

상세: `vault/00_공통관리/06_파이프라인_상태규약.md`

---

## 권장 Obsidian 플러그인

- **Templates** (코어) → `vault/99_템플릿/` 지정
- **Dataview** → MAT-001 문서관리대장 자동 수집
- **Graph view** → POL-PRO-WI-TMP 연결 시각화
