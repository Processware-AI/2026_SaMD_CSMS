---
type: REF
doc_id: "REF-012"
title: "MDCG 2019-16 EU 의료기기 사이버보안 가이드 요약"
version: "0.1"
source: "MDCG 2019-16 Rev.1 — Guidance on Cybersecurity for medical devices"
source_date: "2020-07 (Rev.1)"
source_url: "https://health.ec.europa.eu/system/files/2022-01/md_cybersecurity_en.pdf"
author: "EU Medical Device Coordination Group (MDCG)"
license: "EU public document — 인용 가능 (출처 표기 필수)"
status: draft
created: "2026-04-17"
updated: "2026-04-17"
tags: [REF, MDCG, EU-MDR, cybersecurity, medical-device]
source_citation:
  - type: industry
    file: "N/A — EU MDCG 공개 문서 요약"
    locator: "MDCG 2019-16 Rev.1 전체 Section"
    retrieved_at: "2026-04-17"
    license: "EU public — 인용 가능"
    paraphrase_only: false
    note: "`[_inputs/05_산업가이드/ 미제공 — LLM 메모리 기반 요약]`. 공식 PDF 배치 후 검증 필요"
---

# MDCG 2019-16 요약 (REF-012)

> 원문 출처: MDCG 2019-16 Rev.1 — Guidance on Cybersecurity for medical devices
> 발행일자: 2019년 12월 (Rev.0) / 2020년 7월 (Rev.1)
> 최종 확인일: 2026-04-17 (메모리 기반 요약)
> **경고**: `[_inputs 미제공 — LLM 요약]` — `_inputs/05_산업가이드/` 배치 후 검증 필요

## 1. 요약

**EU MDR (Regulation 2017/745)** 및 **IVDR (Regulation 2017/746)** 부속서 I (일반 안전 및 성능 요구사항, Annex I §17.2, 17.4, 18, 23.4) 의 **사이버보안 기본 요구사항(Basic UR)** 을 어떻게 충족할지 가이드. EU Notified Body 심사 기준.

**원칙**:
- **Security by Design**
- **Defense in Depth** (다계층 방어)
- **IT Security + Physical Security**
- **Pre/Post-market 전 주기 관리**

## 2. 주요 Section 구조

| Section | 제목 | 요지 |
|---|---|---|
| 3 | Secure design & manufacture | 설계·제조 단계 보안 요구 |
| 4 | Documentation & Instructions for Use | 보안 문서화·사용설명 |
| 5 | Post-market surveillance | 시판 후 감시 |
| 6 | Vulnerability disclosure | 취약점 공개 |
| 7 | Integration of legacy devices | 레거시 기기 통합 |
| 8 | Trust between stakeholders | 이해관계자 간 신뢰(제조·의료기관·환자) |

## 3. 본 표준(SaMD-CSMS)과의 대응

| MDCG Section | 본 표준 조항 | 대응 Req |
|---|---|---|
| Secure design & manufacture | 제06조 기술적 보안, 제13조 위험 관리, 제14조 개발·검증 | MDCS-R-061~064, R-131~134, R-141~144 |
| Documentation & IFU | 제02조 문서화, 제15조 EOS 공지 | MDCS-R-021~023, R-152 |
| Post-market surveillance | 제13조 시판후 감시, 제20조 취약점 감시 | MDCS-R-135, R-201 |
| Vulnerability disclosure | 제21조 취약점 공개 | MDCS-R-211~213 |
| Legacy devices | 제15조 레거시 관리 | MDCS-R-151~154 |
| Trust between stakeholders | 전반 (MSP 협력 조항들) | MDCS-R-136, R-163, R-194, R-202, R-205 |

## 4. EU MDR 부속서 I 의 사이버보안 관련 요구 (요지)

- **§17.1**: 제조업자는 제품이 안전하고 효과적으로 작동하도록 개발·제조.
- **§17.2**: SW의 repeatability, reliability, performance 요구.
- **§17.4**: 상호운용 환경에서의 IT 보안 — **최소 정보 보안 요구사항(Minimum IT Requirements)** 명시.
- **§18.8**: 의도된 수명주기 동안 안전하게 작동.
- **§23.4**: 사용설명서에 필요한 IT 보안 조치 명시.

## 5. 핵심 권고 사항

### 5.1 Minimum IT Requirements
제조업자는 제품이 정상 작동하기 위한 **최소 IT 환경 요구사항** 을 IFU(Instructions for Use)에 명시:
- OS 버전, 네트워크 프로토콜, 방화벽 설정
- 사용자 인증·MFA
- 백업·로그·모니터링

### 5.2 Coordinated Vulnerability Disclosure (CVD)
- ISO/IEC 29147 Vulnerability Disclosure
- ISO/IEC 30111 Vulnerability Handling
- 발견 → 검증 → 수정 → 통지 → 공개 단계

### 5.3 Risk Management
- EN ISO 14971 (의료기기 위험관리) + 보안 위험 통합
- Safety ↔ Security 상호작용 평가

## 6. 관련 내부 문서

- [[POL-MDCS-001 사이버보안 방침]]
- [[PRO-MDCS-403 위협 모델링]]
- [[PRO-MDCS-502 시판후 감시]]
- [[PRO-MDCS-601 제품 수명주기(EOS)]]
- [[PRO-MDCS-402 취약점 공개 (VDP)]]

## 7. 원문 인용 (허용)

EU 공공문서로 인용 가능. 단 번역은 원문 링크·출처 표기 필수.

## 8. 글로벌 조화

- **US FDA**: [[REF-011_FDA_Premarket_Cybersecurity_2023_요약_v0.1]] (거의 동일 구조)
- **한국**: 본 표준 (SaMD-CSMS)
- **국제**: IMDRF WG-Cybersecurity N60, IEC 81001-5-1 ([[REF-010_IEC_81001-5-1_요약_v0.1]])

## 9. 오픈 이슈

- [ ] `_inputs/05_산업가이드/` 에 MDCG 2019-16 공식 PDF 배치
- [ ] EU MDR 부속서 I 의 §17.4 "Minimum IT Requirements" 의 본 표준 대응 Req 확정
- [ ] CVD (Coordinated Vulnerability Disclosure) 정책 수립 (ISO/IEC 29147, 30111 준거)
