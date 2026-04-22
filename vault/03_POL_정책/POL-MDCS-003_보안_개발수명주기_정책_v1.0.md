---
type: POL
doc_id: "POL-MDCS-003"
title: "보안 개발수명주기(Secure SDLC) 정책"
version: "1.0"
owner: "VP of R&D"
reviewer: "Product Security Council (PSC)"
approver: "CEO"
scope: "디지털의료기기 소프트웨어·펌웨어의 요구·설계·구현·검증·배포·유지·레거시 단계의 보안 활동"
child_pro:
  - "[[PRO-MDCS-301_보안_SDLC_절차_v1.0]]"
  - "[[PRO-MDCS-302_SBOM_관리_절차_v1.0]]"
  - "[[PRO-MDCS-303_레거시_의료기기_관리_절차_v1.0]]"
standards: ["SaMD-CSMS", "IEC 81001-5-1", "ISO/IEC/IEEE 12207", "FDA Premarket Cybersecurity 2023"]
related_standards: ["ISO/IEC 27001 A.14", "MDCG 2019-16", "NIST SSDF (SP 800-218)"]
reuses: []
status: draft
created: "2026-04-17"
updated: "2026-04-17"
retention: "상시"
tags: [POL, MDCS, SaMD-CSMS, SDLC, SBOM, legacy, tier-C]
tier: "C"
---

# 보안 개발수명주기(Secure SDLC) 정책 (POL-MDCS-003)

> 상위 방침: [[POL-MDCS-001_의료기기_사이버보안_기본방침_v1.0]]
> 연계 정책: [[POL-MDCS-002_사이버보안_리스크관리_정책_v1.0]]

## 1. 목적

본 정책은 디지털의료기기 제품의 **개발·검증 활동에 보안을 내재화**하고, **소프트웨어 구성요소(SBOM)를 투명하게 관리**하며, **레거시·수명 종료(EOS) 단계**까지 보안 책임을 이어 가기 위한 원칙을 규정한다.

## 2. 적용 범위

- 신규 제품 및 개정·기능 추가 릴리스의 **전체 개발 수명주기**
- 자사 개발 소스 + **제3자·오픈소스** 구성요소
- 제품 출시 이후 **지원 종료(EOS) 계획 수립 및 레거시 관리**
- 수명 종료 시 **개인정보 안전 삭제 및 폐기 지침** 제공

## 3. 정책 원칙

1. **Security by Design** — 요구·설계 단계에서 보안 요구사항, 위협 모델링, 보안 설계 원칙을 의무화한다.
2. **Secure Coding & Verification** — 보안 코딩 표준을 따르고, SAST·DAST·퍼징·모의 침투 테스트를 단계별로 수행한다.
3. **SBOM 투명성** — 모든 릴리스에 대해 구성요소명·버전·라이선스·출처·해시를 포함한 SBOM 을 생성·관리·제공한다.
4. **수명 종료 설계(Design for EOS)** — 모듈화·업데이트 메커니즘·서드파티 종속 최소화 원칙에 따라 EOS 이후 위험이 최소화되도록 설계한다.
5. **MSP 정보 제공** — 보안 요구사항 정의서, 위협 모델링 보고서, 검증 결과, SBOM, 데이터 삭제 지침을 필요 시 의료서비스제공자에게 제공한다.

## 4. 역할과 책임

| 역할 | 책임 |
|---|---|
| **CEO** | 본 정책 승인 |
| **VP of R&D** | 본 정책 유지, SDLC 프로세스 자원 배정 |
| **Product Security Officer** | Secure SDLC 게이트 설계·운영 책임 |
| **개발팀 (Dev Lead)** | 보안 요구사항 충족, 보안 코딩 준수, 취약점 조치 |
| **QA / 검증팀** | SAST·DAST·퍼징·펜테스트 수행 및 도구 유효성 확인 |
| **SBOM 관리자** | SBOM 생성·갱신·배포, CVE 연계 추적 |
| **제품 관리자 (Product Manager)** | EOS 일정·지원 계획 문서화, MSP 공지 |

## 5. 준수 기준

- 모든 릴리스는 **보안 요구사항 정의서 → 위협 모델링 → 보안 설계 → 보안 코딩 → 보안 테스트 → 잔여 위험 평가** 게이트를 통과한다.
- 취약점 테스트는 **SAST, DAST, Fuzzing, Penetration Test** 최소 4종을 포함한다.
- 검증 도구는 **도구 유효성 확인(Tool Validation)** 절차에 따라 주기적으로 검증한다.
- SBOM 은 빌드 시점에 자동 생성하며 **CVE/NVD 와 주기적으로(주 1회 이상) 연동 조회**한다.
- 제품 출시 시점에 **예상 지원 종료 일정 및 EOS 이후 예상 지원 계획**을 의료서비스제공자에게 제공한다.
- 제품 폐기 시 개인정보 등 민감 데이터의 **영구 삭제 절차·도구**를 제공한다.

## 6. 관련 하위 절차 (PRO)

- [[PRO-MDCS-301_보안_SDLC_절차_v1.0]] — 단계별 보안 게이트·검증 활동
- [[PRO-MDCS-302_SBOM_관리_절차_v1.0]] — SBOM 생성·갱신·제공·CVE 연계
- [[PRO-MDCS-303_레거시_의료기기_관리_절차_v1.0]] — EOS 계획·레거시 패치·폐기

## 7. 표준 매핑 (Traceability)

| 표준 조항 | Req-ID | 반영 위치 |
|---|---|---|
| SaMD-CSMS 제14조 제1호 (보안 요구·설계·테스트) | MDCS-R-141 | §3-1, §3-2 |
| SaMD-CSMS 제14조 제2호 (SAST/DAST/Fuzzing/Pentest) | MDCS-R-142 | §5 준수 기준 |
| SaMD-CSMS 제14조 제3호 (도구 유효성·교육) | MDCS-R-143 | §5 준수 기준 |
| SaMD-CSMS 제14조 제4호 (MSP 문서 제공) | MDCS-R-144 | §3-5 |
| SaMD-CSMS 제15조 제1호 (EOS 설계) | MDCS-R-151 | §3-4 |
| SaMD-CSMS 제15조 제2호 (EOS 일정·지원 계획) | MDCS-R-152 | §5 준수 기준 |
| SaMD-CSMS 제15조 제3호 (레거시 협력 해결) | MDCS-R-153 | §6 하위 PRO |
| SaMD-CSMS 제15조 제4호 (폐기·데이터 삭제) | MDCS-R-154 | §5 준수 기준 |
| SaMD-CSMS 제16조 제1~5호 (SBOM) | MDCS-R-161~165 | §3-3, §6 |

## 8. 출처 (source_citation)

```yaml
- type: guide
  file: "_inputs/01_표준원문/제14조 개발 및 검증 활동.pdf"
  locator: "p.39 전체"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제15조 레거시 디지털의료기기 관리 활동.pdf"
  locator: "pp.40-41"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제16조 소프트웨어 구성요소 명세서(SBOM) 관리 활동.pdf"
  locator: "pp.42-43"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
```

## 9. 개정 이력

| 버전 | 일자 | 변경내용 | 승인자 |
|---|---|---|---|
| 1.0 | 2026-04-17 | 최초 제정 (SaMD-CSMS 제14·15·16조 기반) | CEO |
