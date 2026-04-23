---
type: work-note
standard: "SaMD-CSMS"
scope_code: "MDCS"
phase: "qa"
status: in-progress
created: "2026-04-17"
updated: "2026-04-17"
tags: [worknote, SaMD-CSMS, MDCS]
---

# SaMD-CSMS 작업 노트

## 기계 상태 (machine state)
실제 실행 상태는 [[_state.yaml]] (동일 폴더). 본 체크리스트는 사람 가독용.

## 진행 체크리스트 (8종 문서유형 기반)

- [x] **Phase 0. 입력자료 Preflight** — 25개 PDF 인벤토리 완료 (`_inputs/README.md`)
- [x] **Phase 1. 표준 개요** — [[00_SaMD-CSMS_표준개요]] (v0.1)
- [x] **Phase 2. 요구사항 분해** — [[01_SaMD-CSMS_요구사항분해]] (v0.1, 95 Req)
- [x] **Phase 3. 정책(POL) 작성** — `03_POL_정책/` (process-designer 담당) — 2026-04-17 완료 (6건)
- [x] **Phase 4. 절차(PRO) 작성** — `04_PRO_절차/` (process-designer 담당) — 2026-04-17 완료 (11건)
- [x] **Phase 5. 업무지침(WI) 작성** — `05_WI_업무지침/` (wi-tmp-writer 담당) — 2026-04-17 완료 (34건)
- [x] **Phase 6. 템플릿(TMP) 작성** — `06_TMP_템플릿/` (wi-tmp-writer) — 2026-04-17 완료 (28건)
- [x] **Phase 7. 작성예시(EX) 작성** — `07_EX_작성예시/` (wi-tmp-writer) — 2026-04-17 완료 (13건, 15건 미작성 Warn)
- [x] **Phase 8. 참고자료(REF) 수집 (초안 3건)** — [[REF-010_IEC_81001-5-1_요약_v0.1]] · [[REF-011_FDA_Premarket_Cybersecurity_2023_요약_v0.1]] · [[REF-012_MDCG_2019-16_Cybersecurity_요약_v0.1]]
- [x] **Phase 9. 추적성(MAT) 갱신** — MAT-011 신규 + MAT-001~005 전 갱신 완료 (2026-04-17)
- [x] **Phase 10. QA 리뷰** — qa-reviewer 담당 — 2026-04-17 Attempt 1 완료 (QA 리포트 참조)
- [x] **Phase 11. MOC 업데이트** — MDCS 상태 🟡, MAT-011 링크 추가 완료

## 입력물 인벤토리 요약

### _inputs/01_표준원문/ (25개 PDF, 공공저작물 추정)

| 구분 | 파일 수 | 비고 |
|---|---|---|
| 본체 (관리체계 개요) | 1 | pp.1-7 전체 구조 요약 |
| 실행방안 (22조 종합) | 1 | pp.1-56 조항별 상세 이행 방안 |
| 조항별 상세 (제01~22조) | 22 | 조항별 독립 PDF |
| 부속서 (제02조-1 문서화지침, 제02조-2 문서목록) | 2 | 문서화 범위 상세 |
| **합계** | **25** | |

### 기타 _inputs/ 카테고리

| 카테고리 | 상태 | 권장 배치 |
|---|---|---|
| 02_법규/ | ⛔ 비어있음 | 디지털의료제품법, 개인정보보호법, 정보통신망법 |
| 03_해설서/ | ⛔ 비어있음 | IEC 81001-5-1 (라이선스 확인 필요) |
| 04_AsIs/ | ⛔ 비어있음 | 고객사 기존 SOP 있을 시 |
| 05_산업가이드/ | ⛔ 비어있음 | FDA 2023, MDCG 2019-16, NIST SP 800-53 |

## 라이선스 판단

| 파일군 | 판단 | 근거 | 처리 |
|---|---|---|---|
| 25개 공공가이드 PDF | **공공저작물 추정 — 확인 필요** | 발행처(식약처) 공공가이드로 추정. 공공누리 유형(1~4) 미확인 | `content_mode: paraphrase` 로 처리. 원문 20단어 이상 연속 복사 금지 유지. **라이선스 표기 확인 이슈로 등록** |

## `[_inputs 미제공 — LLM 추정]` 꼬리표 Req-ID

**없음** (모든 95개 Req 가 `_inputs/01_표준원문/` 의 공공가이드 PDF 에 직접 근거).

단, 법규(디지털의료제품법·개인정보보호법) 조항 번호 매칭은 `_inputs/02_법규/` 부재로 불가 → [[MAT-002_규제요구사항_대조표]] 에서 "법령 조항 확인 필요" 플래그.

## 설계 우선순위 추천 (process-designer 에게)

### 3-Tier 배치 추천

| Tier | 본 표준 조항 매핑 | 예상 POL/PRO 개수 |
|---|---|---|
| **[M] 경영 (Management)** | 제01조 전략, 제02조 문서화 총괄, 제13조 위험관리 | POL 2 + PRO 1 |
| **[C] 핵심 (Core/Value Chain)** | 제14조 개발·검증, 제15조 레거시, 제16조 SBOM | POL 1 + PRO 3 |
| **[S] 지원 (Support)** | 제03~12조 물리·기술 통제, 제17~22조 IR/VM | POL 3 + PRO 7 |

총 추정: **POL 6건, PRO 11건** (하위 WI 30건 이상 예상)

### 설계 우선순위 Top 5 조항

1. **제02조 보안 활동의 문서화** (Req MDCS-R-021~023)
   → 모든 조항의 기반. 제02조-2 "표준 문서 목록" 이 문서체계의 골든 인풋.
2. **제13조 위험 관리 활동** (Req MDCS-R-131~136)
   → STRIDE·SBOM·SDLC·포스트마켓을 묶는 허브.
3. **제17조 침해행위 대응 계획** (Req MDCS-R-171~178)
   → 6개 하위 요구(신고·조치·대응팀·BCP·훈련) 구조화.
4. **제14조 개발 및 검증 활동** (Req MDCS-R-141~144)
   → 보안 SDLC 의 골격. SWLC(ISO/IEC/IEEE 12207) 와 통합 포인트.
5. **제20~22조 취약점 라이프사이클** (Req MDCS-R-201~224)
   → 감시-공개-조치 3단계 일체. VDP 운영.

### 재사용 후보 (타 표준과의 중복)

| 본 표준 조항 | 재사용 가능 표준 | 재사용 대상 |
|---|---|---|
| 제03조 물리적 보안 | ISO/IEC 27001 A.7, A.11 | POL/PRO/WI 거의 그대로 테일러링 |
| 제04조 보안 통신 | ISO/IEC 27001 A.13 | 동일 |
| 제05조 권한 및 인증 | ISO/IEC 27001 A.9 / A.5.15-18 | 동일 |
| 제08조 데이터 보안, 제06조 개인정보 조치 | PIMS/ISO 27701, 개인정보보호법 | 기존 PIMS POL 재사용 + MDCS 추가 통제 |
| 제11조 보안 모니터링 | ISO/IEC 27001 A.8.16, A.8.15 | SIEM/로그관리 WI 재사용 |
| 제13조 위험 관리 | ISO 31000, AAMI TIR57 | 위험관리 PRO 재사용 + 의료기기 특화 WI 추가 |
| 제14조 개발·검증 | SWLC (ISO/IEC/IEEE 12207), ISO/IEC 27001 A.14 | SDLC에 Security Gate 삽입 |

## 결정/이슈 로그

| 일자 | 항목 | 결정/이슈 | 비고 |
|---|---|---|---|
| 2026-04-17 | 표준 코드 | `SaMD-CSMS` 로 확정 | 영역 `MDCS` 등록 완료 ([[02_문서번호체계]]) |
| 2026-04-17 | Req-ID 규칙 | `MDCS-R-{조항×10 + 호}` | 예: MDCS-R-172 = 제17조 제2항. 3자리수로 최대 조×10+9 = 229 가능 |
| 2026-04-17 | 라이선스 | 공공저작물 추정, `paraphrase` 모드 유지 | 공공누리 유형 확인 필요 — 이슈 등록 |
| 2026-04-17 | Req 권고 19건 | 설계 시 "권고 준수" 정책 권장 | FDA/MDCG/CISA 동향상 사실상 의무화 추세 |
| 2026-04-17 | 법규 근거 | 디지털의료제품법 제14조·제32조 확인 | 단, 법 원문 `_inputs/02_법규/` 부재 — 배치 필요 |
| 2026-04-17 | AI 조항 (제12조) | AI 적용 기기 한정 | 비적용 프로젝트는 MDCS-R-12x 전체 제외 가능 |
| 2026-04-17 | SBOM 조항 (제16조) | 선택 실행 지침이나 사실상 의무 격상 권장 | FDA, CISA, EU 등 글로벌 요구 수렴 |
| 2026-04-17 | trace — Unresolved WI | PRO child_wi 선언 대비 미생성 WI 26건 (P0 3건 포함) | MAT-011 §6 큐 등록. write 단계 경고 6건 외 20건 추가 발견 |
| 2026-04-17 | trace — EX 저커버 | TMP 28 중 13만 EX 보유 (15건 미작성) | IR·VDP·법적 5건 우선 작성 권고 (MAT-011 §7) |
| 2026-04-17 | trace — TMP-IR-006 CSIRT RACI | 의뢰사 지적 — 신규 TMP 필요 | MDCS-R-175 보강용, qa-reviewer 전달 |
| 2026-04-17 | trace — RACI 경고 | PRO-MDCS-502/301 Accountable 경합 (CEO-오동석, 오동석-PSO) | MAT-004 공백·중복 알림에 기록. 조직 합의 필요 |
| 2026-04-17 | qa attempt 1 — 깨진 TMP 링크 5건 | TMP-IR-003, TMP-ACC-002, TMP-NET-001, TMP-IR-006, TMP-SDLC-001 이 WI 에 선언되었으나 파일·큐 미등록 | **Major** - MAT-001 unresolved_tmp 큐 추가 필요 (traceability-mapper) · 또는 wi-tmp-writer 가 실제 TMP 생성 |
| 2026-04-17 | qa attempt 1 — WI 내 깨진 EX 참조 15건 | 작성예시 링크가 13건만 대응, 나머지 15건은 EX 미생성 | **Warn** - 기존 ex_missing_for_tmp 큐에 포함되어 있음 |
| 2026-04-17 | qa attempt 1 — 링크 버전 suffix 일관성 | 일부 WI→TMP 링크가 `_v0.1` 없이 기재됨 (Obsidian 은 prefix 매칭으로 해소되나 스타일 불일치) | **Minor** - 정식 버전 suffix 포함 표기 권장 |
| 2026-04-17 | qa attempt 1 — POL/PRO status | 전체 draft 로 유지 (승인 미완) | **정상** - 신규 빌드이므로 `draft` 유지가 원칙 |
| 2026-04-17 | qa attempt 1 — 저작권 가드 | `_inputs/01_표준원문/` PDF 만 존재 (MD 변환본 없음), 산출물 전수 `paraphrase_only: true` 플래그 일관 | **정상** - 20단어 연속 일치 검사는 MD 변환본 없어 불가 → PDF 수기 대조는 Out-of-Scope |

## QA attempt 1 이슈 로그 (2026-04-17)

| issue_id | severity | category | file | assigned_to | 요약 |
|---|---|---|---|---|---|
| QA-20260417-001 | major | traceability | vault/05_WI_업무지침/WI-502-02_대외신고_식약처_MSP_이용자_v0.1.md | traceability-mapper | TMP-IR-003 미등록 큐 필요 |
| QA-20260417-002 | major | traceability | vault/05_WI_업무지침/WI-401-01_계정_생명주기_v0.1.md | traceability-mapper | TMP-ACC-002 미등록 큐 필요 |
| QA-20260417-003 | major | traceability | vault/05_WI_업무지침/WI-402-01_네트워크_보안_설정_v0.1.md | traceability-mapper | TMP-NET-001 미등록 큐 필요 |
| QA-20260417-004 | major | traceability | vault/05_WI_업무지침/WI-502-05_CSIRT_구성_및_훈련_v0.1.md | traceability-mapper | TMP-IR-006 미등록 큐 필요 (작업노트 기존 식별됨) |
| QA-20260417-005 | major | traceability | vault/05_WI_업무지침/WI-403-01_파일_업다운로드_검증_v0.1.md | traceability-mapper | TMP-SDLC-001 미등록 큐 필요 |
| QA-20260417-006 | minor | link | vault/05_WI_업무지침/*.md (다건) | wi-tmp-writer | TMP/EX 링크 버전 suffix 누락 일관성 개선 |
| QA-20260417-007 | minor | mat | vault/90_MAT_통합매핑/MAT-004_RACI_통합표.md | traceability-mapper | RACI Accountable 경합 3건 영구 해소 방안 (조직 합의 필요 — manual 에스컬레이션 대기) |

상세: 오케스트레이터 최종 메시지(QA attempt 1 findings) 및 `_state.yaml qa_failures[]` 참조

## 오픈 이슈 (법규·해설서 부재)

- [ ] **디지털의료제품법 원문** `_inputs/02_법규/` 부재 → MAT-002 법령 조항 대조 불가 (현재 "제14조·제32조" 만 확인)
- [ ] **개인정보보호법** 제06·08조 연계 구체 조항 미확정 (제29조 안전조치의무, 제23조 민감정보, 제26조 개인정보처리 위탁 등 — `[확인 필요]`)
- [ ] **의료기기법** 연계 미확인 (허가·안전관리 등)
- [ ] **IEC 81001-5-1** 구매 라이선스 미확인 → `verbatim` 금지
- [ ] **FDA Premarket Cybersecurity Guidance (2023)** 공개 가이드 — `_inputs/05_산업가이드/` 배치 권장
- [ ] **MDCG 2019-16** 공개 가이드 — 동일
- [ ] 본 표준 PDF 의 **발행일자·발행번호·공식 시행일** 확인 필요
- [ ] **trace 추가 오픈 이슈** (2026-04-17)
  - Unresolved WI 26건 (`status: future_wi`) — P0 3건 (WI-502-04 BCP, WI-502-06 재발방지, WI-301-02 취약점평가)
  - TMP-IR-006_CSIRT_RACI_테이블 신규 필요 (MDCS-R-175)
  - EX 저커버 TMP 15건 — 법적·IR·VDP 5건 우선
  - MSP 가이드 EX 6건 (R-115, 136, 184, 194, 202, 205) 미작성
  - RACI Accountable 경합 3건 (PRO-MDCS-401, 106, 301)

## 다음 Phase (design) 전달 사항

1. [[00_SaMD-CSMS_표준개요]] 를 먼저 읽고 5개 영역/22조 구조 내재화
2. [[01_SaMD-CSMS_요구사항분해]] 의 95개 Req-ID 를 POL/PRO/WI 로 설계 분해
3. 재사용 후보 (위 표) 를 검토하여 타 표준의 기존 산출물 활용 가능 여부 판단
4. 우선순위 Top 5 조항부터 착수 (제02→제13→제17→제14→제20~22)
5. 선택 실행 지침(19건) 은 "권고 준수" 정책으로 설계하되 POL 에서 조직 레벨 선택 여지 명시
6. **골든샘플 필수 섹션 준수** (RACI, Mermaid 흐름도, KPI 등)

## 참고 자료 생성 현황 (REF)

- [x] [[REF-010_IEC_81001-5-1_요약_v0.1]] — 의료기기 SW 보안 라이프사이클
- [x] [[REF-011_FDA_Premarket_Cybersecurity_2023_요약_v0.1]] — 미국 FDA 프리마켓 사이버보안
- [x] [[REF-012_MDCG_2019-16_Cybersecurity_요약_v0.1]] — EU MDCG 의료기기 사이버보안

(REF 는 공개 가이드 기반 초안 — 공식 원문 `_inputs/` 배치 후 v1.0 승격)

## QA Attempt 1 자가수정 (2026-04-17)
- QA-20260417-001 ~ 005 (Major, traceability) 5건 해소 완료.
- 조치: MAT-001 v0.3 Unresolved TMP 큐 5행 추가, MAT-011 미생성 TMP 섹션 추가.
- 후속: P0·P1 우선 실제 TMP 파일 작성 필요 (운영 단계 과제).

## QA Attempt 2 재감사 결과 (2026-04-17)
- 리포트: [[99_QA리포트_20260417_attempt2]]
- 결과: **ALL PASS** — Fail 5→0. Critical/회귀 0.
- metrics: total 48 / pass 44 / fail 0 / warn 4.
- 해소 검증:
  - MAT-001 v0.3 §Unresolved TMP 큐 5행 확인 (TMP-IR-003/ACC-002/NET-001/IR-006/SDLC-001).
  - MAT-011 §6 미생성 TMP 섹션 5건 + 총계 WI 26+TMP 5=31 일관성 확인.
  - 5개 WI 의 `related_tmp` Obsidian unresolved 링크 유지(정상).
- Warn 유지: EX 미작성 15건 / Unresolved WI 26건 / RACI 경합 3건 / 링크 버전 suffix Minor.
- 상태: overall_status=done, current_phase=done → finalize 단계 진입 가능.
