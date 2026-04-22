---
type: MAT
doc_id: MAT-004
title: RACI 통합표
version: "0.3"
owner: "PSO"
status: draft
created: 2026-04-16
updated: 2026-04-22
retention: "상시"
tags: [MAT, raci]
---

# MAT-004 RACI 통합표

> 전사 PRO 별 책임 분담을 단일 표로 집계. 역할 중복·공백 탐지용.

## 역할 리스트
- 경영진(CEO / CISO / CPO / VP of R&D)
- 프로세스 오너 (PSO, CSIRT 리더, DPO, IAM·SBOM·KMS 관리자 등)
- 실무 담당자 (개발·QA·SecOps·인프라·네트워크·RA·홍보/CS)
- 내부심사팀
- 외부 이해관계자 (식약처, 의료서비스제공자, 제품 이용자)

## RACI 매트릭스 (PRO 수준 종합)

### QMS (샘플)

| PRO | 활동 | CEO | CISO | Owner | 담당 | QA |
|---|---|---|---|---|---|---|
| PRO-QMS-101 | 경영검토 | A | C | R |  | I |

### SaMD-CSMS — PRO 11종 (Owner = Accountable)

| PRO | 활동(대표) | CEO | CISO | Owner | R&D | SecOps | DPO | CSIRT | PSO | RA |
|---|---|---|---|---|---|---|---|---|---|---|
| PRO-MDCS-101 (문서화) | 보안문서 관리 | I | C | **A**/R (PSO) | — | — | — | — | **A**/R | — |
| PRO-MDCS-401 (접근통제) | 계정·MFA·원격접속 | I | **A** | R (IAM 관리자) | — | C | — | — | C | — |
| PRO-MDCS-402 (통신·암호) | TLS·키관리·HSM | I | **A** | R (네트워크·인프라 팀장) | — | C | — | — | C | — |
| PRO-MDCS-403 (데이터·파일) | 업로드검증·비식별화·DB | I | C | **A**/R (DPO) | C | — | R | — | C | — |
| PRO-MDCS-501 (모니터링·로그·물리) | SIEM·백업·출입통제 | I | C | **A**/R (SecOps 팀장) | — | R | — | C | C | — |
| PRO-MDCS-502 (침해대응) | CSIRT·신고·복구 | A (Critical) | **A** | R (CSIRT 리더) | — | R | C | R | C | R |
| PRO-MDCS-601 (취약점 관리) | 감시·공개·조치 | I | C | **A**/R (PSO) | R | — | — | — | R | C |
| PRO-MDCS-301 (SDLC) | 보안 코딩·SAST/DAST·게이트 | I | C | **A**/R (R&D Lead) | R | — | — | — | C | — |
| PRO-MDCS-302 (SBOM) | 생성·CVE·공개 | I | C | **A**/R (SBOM 관리자) | R | — | — | — | C | — |
| PRO-MDCS-303 (레거시) | EOS·안전삭제 | I | C | **A**/R (Product Manager) | C | — | R | — | C | — |
| PRO-MDCS-201 (위험관리·AI 통합) | STRIDE·평가·시판후 | I | **A** | R (PSO) | C | — | — | — | R | — |

> 각 셀: R(Responsible), A(Accountable, 최대 1명), C(Consulted), I(Informed). 공란은 무관여.

## 공백·중복 알림

### Accountable 누락 PRO
- **없음** (전 11개 PRO 모두 Accountable 명시)

### Accountable 중복·모호 PRO (2명 이상 할당 또는 역할 경합)
- ⚠️ **PRO-MDCS-401**: CISO 단독 Accountable — IAM 실무 Accountable 명확 (IAM 관리자는 R)
- ⚠️ **PRO-MDCS-502**: CEO(Critical 등급만) + CISO 중첩 할당 — 침해 등급별 Accountable 분기 규정화 필요
- ⚠️ **PRO-MDCS-201**: CISO(전사 위험) + PSO(제품 위험) 경합 소지 — 본 표상 CISO Accountable, PSO Responsible 로 명시했으나 위험 수용 기준 레벨별 재확인 필요

### Consulted 누락 권고
- **DPO**: PRO-MDCS-502 (침해 시 개인정보 유출 가능) → 현재 Consulted 반영됨
- **RA Lead**: PRO-MDCS-601 (취약점 통보 시 RA 필수) → 현재 Consulted 반영됨
- **홍보/CS**: PRO-MDCS-502 (대외 공지) — 현행 표에 표기 누락 → 차후 v0.3 에서 열 추가 권장

### Informed 누락 권고
- **이사회/감사실**: PRO-MDCS-502 (Critical 등급) — 현재 미표기 → 거버넌스 레벨에서 추가 검토

## 개정 이력

| 버전 | 일자 | 변경 내용 | 승인자 |
|---|---|---|---|
| 0.1 | 2026-04-16 | 초안 (구조만) | (draft) |
| 0.2 | 2026-04-17 | trace — SaMD-CSMS 11개 PRO RACI 요약 반영, Accountable 중복 경고 3건 등록 | (draft) |
| 0.3 | 2026-04-22 | PRO 번호체계 검증 완료 (현행 일치), 날짜 갱신 | (draft) |
