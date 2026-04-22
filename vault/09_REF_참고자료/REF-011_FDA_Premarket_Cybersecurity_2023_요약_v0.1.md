---
type: REF
doc_id: "REF-011"
title: "FDA Premarket Cybersecurity Guidance (2023) 요약"
version: "0.1"
source: "US FDA — Cybersecurity in Medical Devices: Quality System Considerations and Content of Premarket Submissions (2023-09-27)"
source_date: "2023-09-27"
source_url: "https://www.fda.gov/regulatory-information/search-fda-guidance-documents/cybersecurity-medical-devices-quality-system-considerations-and-content-premarket-submissions"
author: "US Food and Drug Administration (FDA) CDRH"
license: "US Federal Government work — 공공저작물 (public domain)"
status: draft
created: "2026-04-17"
updated: "2026-04-17"
tags: [REF, FDA, premarket, cybersecurity, medical-device, SBOM]
source_citation:
  - type: industry
    file: "N/A — FDA 공개 가이드 요약 (public domain)"
    locator: "2023 Final Guidance Document 전체"
    retrieved_at: "2026-04-17"
    license: "US Federal — public domain (인용 자유)"
    paraphrase_only: false
    note: "`[_inputs/05_산업가이드/ 미제공 — LLM 메모리 기반 요약]`. 공식 PDF 배치 후 검증 필요"
---

# FDA Premarket Cybersecurity Guidance (2023) 요약 (REF-011)

> 원문 출처: FDA Guidance — "Cybersecurity in Medical Devices: Quality System Considerations and Content of Premarket Submissions"
> 발행일자: 2023년 9월 27일 (Final)
> 최종 확인일: 2026-04-17 (메모리 기반 요약)
> **경고**: `[_inputs 미제공 — LLM 요약]` — `_inputs/05_산업가이드/` 배치 후 검증 필요

## 1. 요약

**FDA 21 CFR Part 820 QSR** 및 2022년 **Omnibus 법** (FDORA §524B Cybersecurity for cyber devices) 을 근거로, **Cyber Device**로 분류되는 의료기기 제조업자가 **premarket submission**(510(k), PMA, De Novo, HDE)에 포함해야 할 사이버보안 산출물을 규정.

**핵심 개념**:
- **SPDF (Secure Product Development Framework)**: 보안 개발 프로세스 전체
- **Cyber Device**: ①소프트웨어 포함 ②인터넷 연결 ③사이버보안 취약점 가능성
- **TPLC (Total Product Life Cycle)**: 시판 전 ~ 시판 후 ~ EOS 전체

## 2. 주요 Premarket 제출 산출물

| FDA 요구 산출물 | 설명 |
|---|---|
| **Threat Modeling** | 제품 아키텍처 기반 위협 식별 (STRIDE/PASTA 등) |
| **Cybersecurity Risk Assessment** | 보안 위험 평가 (Safety+Security 융합, AAMI TIR57 참조) |
| **SBOM** | Software Bill of Materials (CBOM 포함) |
| **Vulnerability Assessment** | 알려진 취약점 (CVE) 평가 |
| **Security Architecture Views** | Global System View, Multi-Patient Harm View, Updatability View 등 |
| **Security Testing** | SAST/DAST/펜테스트/퍼징 결과 |
| **Cybersecurity Labeling** | 사용자 대상 보안 지침 |
| **Postmarket Cybersecurity Management Plan** | 시판 후 관리 계획 (취약점 감시·공개·패치) |

## 3. 본 표준(SaMD-CSMS)과의 대응

| FDA 항목 | 본 표준 조항 | 대응 Req |
|---|---|---|
| Threat Modeling | 제13조 위험 관리 | MDCS-R-131 |
| Cybersecurity Risk Assessment | 제13조 위험 관리 | MDCS-R-132~134 |
| SBOM | 제16조 SBOM 관리 | MDCS-R-161~165 |
| Vulnerability Assessment | 제13·20조 | MDCS-R-132, R-201~204 |
| Security Testing | 제14조 개발 및 검증 | MDCS-R-141~143 |
| Postmarket Management | 제13·17~22조 | MDCS-R-135, R-171~, R-201~224 |
| Coordinated Vulnerability Disclosure | 제21조 | MDCS-R-211~213 |
| Cybersecurity Labeling | 제15조 (EOS 공지 등) | MDCS-R-152 |

## 4. FDA SPDF 4단계

1. **Security Risk Management** — 위험 식별·평가·대응 (제13조)
2. **Secure Product Development** — SDLC 내 보안 활동 (제14조)
3. **Security Architecture** — 보안 아키텍처 설계 (제06조, 제13조)
4. **Transparency** — SBOM·Labeling·VDP 투명성 (제16·21조)

## 5. 핵심 용어

- **SPDF**: Secure Product Development Framework
- **CBOM**: Cryptographic Bill of Materials (암호 자산 명세)
- **CVSS**: Common Vulnerability Scoring System (취약점 심각도)
- **CVE**: Common Vulnerabilities and Exposures
- **Coordinated Disclosure**: 조정 공개 (CVD) — 취약점 공개 시점 협의

## 6. 관련 내부 문서

- [[POL-MDCS-002 제품 보안 거버넌스]]
- [[PRO-MDCS-403 위협 모델링]]
- [[PRO-MDCS-108 SBOM 관리]]
- [[PRO-MDCS-401 취약점 관리]]
- [[PRO-MDCS-402 취약점 공개 (VDP)]]

## 7. 원문 인용 (허용 — FDA 공공저작물)

FDA 가이드는 **US Federal public domain** 으로 인용 자유. 단, 번역본은 저작권 주의.

## 8. 글로벌 조화 (대응 가이드)

- **EU**: MDCG 2019-16 Rev.1 — 유사 구조
- **한국**: 본 표준 SaMD-CSMS — 대응
- **Japan**: PMDA 의료기기 사이버보안 가이드라인 — 참고
- **IMDRF**: WG-Cybersecurity N60 문서 — 국제 조화

## 9. 오픈 이슈

- [ ] `_inputs/05_산업가이드/` 에 FDA 2023 공식 PDF 배치
- [ ] 본 표준의 "제품 출시 시점 공지" 와 FDA "Cybersecurity Labeling" 대응 심화 분석
- [ ] SBOM 포맷 (SPDX, CycloneDX, SWID) 선정 결정
