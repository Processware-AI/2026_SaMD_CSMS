---
type: TMP
doc_id: "TMP-SBOM-001"
title: "SBOM 검증 체크리스트"
version: "0.1"
owner: "SBOM 관리자"
parent_wi: "[[WI-302-01_SBOM_생성_및_포맷_v0.1]]"
related_ex: "[[EX-SBOM-001_SBOM_검증_체크리스트_작성예시_v0.1]]"
standards: ["SaMD-CSMS", "SPDX", "CycloneDX", "CISA SBOM Minimum Elements"]
status: draft
created: "2026-04-17"
updated: "2026-04-17"
tags: [TMP, MDCS, SaMD-CSMS, SBOM]
---

# SBOM 검증 체크리스트 (TMP-SBOM-001)

> 상위 업무지침: [[WI-302-01_SBOM_생성_및_포맷_v0.1]] · 작성예시: [[EX-SBOM-001_SBOM_검증_체크리스트_작성예시_v0.1]]

> 이 파일은 **빈 양식** 입니다.

## 1. SBOM 개요

| 항목 | 내용 |
|---|---|
| 제품·버전 |  |
| 빌드 ID |  |
| 생성 일시 |  |
| 포맷 | `<SPDX 2.3/CycloneDX 1.5>` |
| 생성 도구 | `<Syft/Trivy/기타>` |

## 2. 필수 필드 체크 (CISA 최소 요소)

| 필드 | 충족 | 비고 |
|---|---|---|
| 구성요소명 |  |  |
| 버전 |  |  |
| 공급자 |  |  |
| 라이선스 |  |  |
| 출처(URL/PURL) |  |  |
| 해시 |  |  |
| 의존성 관계 |  |  |
| 작성자 정보 |  |  |
| 타임스탬프 |  |  |

## 3. 서명·저장

- [ ] 디지털 서명 추가
- [ ] Artifact Registry 저장 경로:
- [ ] 무결성 해시 동반 공개

## 4. 이전 릴리스 대비 Diff

| 구분 | 수 |
|---|---|
| 신규 추가 컴포넌트 |  |
| 제거된 컴포넌트 |  |
| 버전 변경 컴포넌트 |  |
| 라이선스 변경 |  |

## 5. 초기 CVE 매칭

| 심각도 | 건수 | 추가 조치 필요 |
|---|---|---|
| Critical |  |  |
| High |  |  |

## 6. 승인

| 단계 | 역할 | 성명 | 일자 |
|---|---|---|---|
| 필드 검증 | SBOM 관리자 |  |  |
| 기술 검토 | PSO |  |  |
| 라이선스 검토 | 법무 |  |  |

---

작성예시: [[EX-SBOM-001_SBOM_검증_체크리스트_작성예시_v0.1]]
