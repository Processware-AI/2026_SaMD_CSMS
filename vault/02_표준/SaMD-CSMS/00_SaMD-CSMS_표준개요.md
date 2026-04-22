---
type: standard-overview
standard: "SaMD-CSMS"
title: "디지털 의료기기 사이버보안 관리 체계 (SaMD Cybersecurity Management System)"
version: "2025"
scope_code: "MDCS"
domain: "MDCS"
status: draft
created: "2026-04-17"
updated: "2026-04-17"
tags: [standard, SaMD-CSMS, MDCS, cybersecurity, medical-device]
source_citation:
  - type: guide
    file: "_inputs/01_표준원문/디지털 의료기기 사이버보안 관리 체계.pdf"
    locator: "전체 (pp.1-7)"
    retrieved_at: "2026-04-17"
    license: "공공저작물 추정 — 확인 필요"
    paraphrase_only: true
  - type: guide
    file: "_inputs/01_표준원문/디지털 의료기기 전자적 침해행위 보안 지침 실행방안.pdf"
    locator: "전체 (22개 조항별 실행방안)"
    retrieved_at: "2026-04-17"
    license: "공공저작물 추정 — 확인 필요"
    paraphrase_only: true
---

# SaMD-CSMS 표준 개요

> 상위 기준: [[표준프로세스_구성원칙]] · 문서체계: [[01_문서체계]] · 번호체계: [[02_문서번호체계]]

## 1. 표준 식별

| 항목 | 내용 |
|---|---|
| **표준 코드** | SaMD-CSMS |
| **정식 명칭** | 디지털 의료기기 사이버보안 관리 체계 |
| **영문 약칭** | SaMD Cybersecurity Management System |
| **발행기관** | 식품의약품안전처 / 식품의약품안전평가원 (추정) `[확인 필요]` |
| **발행 시점** | 2025년 추정 (문서 수령 2025-06-11) `[확인 필요]` |
| **버전** | 본 분석 기준 초판 |
| **성격** | 공공 가이드 (디지털의료제품법 이행 지침) |
| **영역 코드** | MDCS — [[02_문서번호체계]] |
| **근거 법령** | 디지털의료제품법 제14조, 제32조 |
| **라이선스 상태** | 공공저작물 추정 (`_inputs/README.md` 기록, 공공누리 유형 확인 필요) |

## 2. 적용 범위 (Scope)

### 2.1 대상
- **디지털의료기기** 제조업자등 (주된 책임주체)
- 액세서리, 전자 인터페이스, 구성품 포함
- **인공지능 기술이 적용된 디지털의료기기**는 제12조가 추가 적용됨
- **의료서비스제공자**는 선택 실행 지침(협력·통보·훈련) 대상

### 2.2 수명주기 범위
디지털의료기기의 **생명 주기 전반**:
- 설계 → 개발 → 검증 → 배포 → 운영 → 유지보수 → 수명 종료(EOS) → 레거시 → 폐기

### 2.3 관리 범위
- 물리적 보안 (설치·운영 환경)
- 기술적 보안 (SW·네트워크·데이터)
- 보안 통신·접근통제·암호화·무결성
- 전자적 침해행위 대응 및 취약점 관리

(출처: `_inputs/01_표준원문/디지털 의료기기 사이버보안 관리 체계.pdf` pp.1-2)

## 3. 핵심 구조 (5개 영역 × 22조)

본 표준은 전통적 HLS 구조가 아닌 **5개 관리영역(I~V) + 22개 조문** 로 구성되어 있음.

### I. 총괄 책임 및 문서화 (Overall Responsibility & Documentation)
- **제01조** 디지털 의료기기 전자적 침해행위 보안 대응 전략 (목적·전략 총괄)
- **제02조** 보안 활동의 문서화 (전 영역 문서화 의무)
  - 제02조-1 보안 문서화 지침 (부속서)
  - 제02조-2 보안 문서 목록 (부속서)

### II. 보안 체계 구축 (Security System Establishment)
#### 물리적 보안
- **제03조** 물리적 보안

#### 네트워크·통신·접근통제
- **제04조** 보안 통신
- **제05조** 권한 및 인증

#### 기술적 보안
- **제06조** 기술적 보안
- **제07조** 파일 및 입력 유효성
- **제08조** 데이터 보안
- **제09조** 암호화 키 관리
- **제10조** 유지 관리
- **제11조** 보안 모니터링 및 대응
- **제12조** 인공지능 보안 (AI 적용 기기에 한함)

### III. 위험 관리 활동 (Risk Management Activities)
- **제13조** 위험 관리 활동
- **제14조** 개발 및 검증 활동
- **제15조** 레거시 디지털의료기기 관리 활동
- **제16조** 소프트웨어 구성요소 명세서(SBOM) 관리 활동

### IV. 전자적 침해행위 대응 (Electronic Intrusion Response)
- **제17조** 침해행위 대응 계획 등
- **제18조** 침해행위 신고
- **제19조** 침해행위 발생 이후의 조치

### V. 취약점 감시 및 대응 (Vulnerability Monitoring & Response)
- **제20조** 취약점 감시
- **제21조** 취약점 공개
- **제22조** 취약점 조치

## 4. 준거 법규 매핑

| 국내 법규 | 관련 조항 / 내용 | 본 표준과의 대응 |
|---|---|---|
| **디지털의료제품법** | 제14조 (보안 업무 수행·문서화), 제32조 (취약점 감시·대응) | 본 표준의 직접 근거 법률 |
| **개인정보보호법** | 제29조(안전조치의무), 제23조(민감정보) 등 | 제06조 개인정보 조치, 제08조 데이터 비식별화 |
| **의료법 / 의료기기법** | 의료기기 허가·안전관리 | 제품 전체 수명주기 관리 |
| **정보통신망법** | 침해사고 대응·신고 | 제18조 침해행위 신고와 연계 가능 |
| **전자금융감독규정** (해당 시) | 보안관리 일반 | 참고 |

(`[_inputs 미제공 — LLM 추정]` 법규 원문이 `_inputs/02_법규/` 에 없음 — 향후 확인 필요)

## 5. 관련 국제 표준 (교차 매핑 초안)

| 국제 표준 / 가이드 | 발행처 | 대응 조항(본 표준) |
|---|---|---|
| **IEC 81001-5-1** — Health software and health IT systems safety, effectiveness and security | IEC | 제13조(위험관리), 제14조(개발검증), 제22조(취약점조치) 전반 |
| **FDA Premarket Cybersecurity Guidance (2023)** | US FDA | 제13조~제16조 (위험관리·SBOM·레거시) |
| **MDCG 2019-16** — Cybersecurity for medical devices | EU MDCG | 제01조~제22조 전반 (유사 구조) |
| **NIST SP 800-53** | NIST | 제03조~제11조 (기술통제 일반) |
| **NIST Cybersecurity Framework** | NIST | 전체 5영역 대응 (Identify-Protect-Detect-Respond-Recover) |
| **ISO/IEC 27001** | ISO/IEC | 정보보호관리체계 전반 (POL/PRO 구조 재사용 가능) |
| **IEC 62443** (시리즈) | IEC | OT/산업제어 — 참고 |
| **AAMI TIR57** — Principles for medical device security (risk management) | AAMI | 제13조 위험관리 |
| **CISA/FDA SBOM 지침** | CISA, FDA | 제16조 SBOM 관리 |

> 교차 매핑은 [[MAT-002_규제요구사항_대조표]] 에서 Req-ID 단위로 상세 관리.

## 6. 입력자료(_inputs) 인벤토리

| 구분 | 파일 수 | 라이선스 상태 | 비고 |
|---|---|---|---|
| 01_표준원문 | 25개 PDF | 공공저작물(추정) | 본체 1 + 실행방안 1 + 제01~22조(부속서 2) |
| 02_법규 | 0 | — | 디지털의료제품법 PDF 배치 권장 |
| 03_해설서 | 0 | — | IEC 81001-5-1, FDA 가이드 등 |
| 04_AsIs | 0 | — | 고객사 기존 SOP 있을 시 |
| 05_산업가이드 | 0 | — | MDCG 2019-16, NIST SP 800-53 |

상세: [[_inputs/README|_inputs/README.md]]

## 7. 산출물 링크

| 산출물 | 문서 |
|---|---|
| 요구사항 분해 | [[01_SaMD-CSMS_요구사항분해]] |
| 작업 노트 | [[02_SaMD-CSMS_작업노트]] |
| 정책(POL) | (설계단계에서 생성 — process-designer) |
| 절차(PRO) | (설계단계) |
| 업무지침(WI) | (작성단계 — wi-tmp-writer) |
| 추적성(MAT) | [[MAT-002_규제요구사항_대조표]] → MDCS 섹션 |
| 참고자료(REF) | [[REF-010_IEC_81001-5-1_요약_v0.1]] · [[REF-011_FDA_Premarket_Cybersecurity_2023_요약_v0.1]] · [[REF-012_MDCG_2019-16_Cybersecurity_요약_v0.1]] |

## 8. 설계 방향 힌트 (3-Tier 프로세스 배치)

본 표준의 22조를 전사 3-Tier 프로세스 아키텍처에 배치한 추천안 (구체 설계는 [[process-designer]] 담당):

| Tier | 포함 조항 | 추천 POL/PRO |
|---|---|---|
| **[M] 경영** (Management) | 제01조(전략), 제02조(문서화 총괄), 제13조(위험관리) | POL-MDCS-001 사이버보안 방침, POL-MDCS-002 제품 보안 거버넌스 |
| **[C] 핵심** (Core/Value Chain) | 제14조(개발·검증), 제15조(레거시), 제16조(SBOM) | PRO-MDCS-101 보안 SDLC 절차, PRO-MDCS-401 SBOM 관리 절차 |
| **[S] 지원** (Support) | 제03~12조(물리·기술 통제), 제17~22조(IR·VM) | PRO-MDCS-301 보안운영 절차, PRO-MDCS-302 침해대응 절차, PRO-MDCS-303 취약점 감시·공개·조치 절차 |

### 우선순위 Top 5 조항 (설계 착수 순)
1. **제02조 보안 활동의 문서화** — 모든 조항의 상위 기반, 문서체계 정의
2. **제13조 위험 관리 활동** — 보안 설계의 입력, STRIDE·SBOM 연계
3. **제17조 침해행위 대응 계획** — 6개 하위 요구(신고·조치·대응팀·BCP·훈련) 구조화
4. **제14조 개발 및 검증 활동** — 보안 SDLC, SAST/DAST/펜테스트
5. **제22조 취약점 조치** + 제20·21조 (VDP 일체) — 패치·공개·모니터링 라이프사이클

## 9. 저작권 가드레일

- 본 표준 원문은 `content_mode: paraphrase` 로 취급 (`_inputs/README.md`)
- 20단어 이상 연속 일치 금지 — QA 검사 대상
- 조항 번호·제목은 공식 인용 가능
- 본 개요 및 요구사항분해는 **요지 재진술(paraphrase)** 기반

## 10. 참고 문헌

- 디지털의료제품법 (법제처 law.go.kr) `[확인 필요 — _inputs/02_법규/ 에 원문 미배치]`
- 식품의약품안전처 디지털의료기기 전자적 침해행위 보안 지침 (공공가이드, 2025년 추정)
- IEC 81001-5-1:2021 Health software security
- FDA Premarket Cybersecurity Guidance (2023)
- MDCG 2019-16 Rev.1 Cybersecurity for medical devices (EU)
- NIST SP 800-53 Rev.5
- IEC 62443 (시리즈)
