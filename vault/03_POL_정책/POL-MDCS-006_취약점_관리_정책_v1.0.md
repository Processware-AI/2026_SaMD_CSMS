---
type: POL
doc_id: "POL-MDCS-006"
title: "취약점 관리 정책 (감시·공개·조치)"
version: "1.0"
owner: "Product Security Officer (PSO)"
reviewer: "Product Security Council (PSC)"
approver: "CEO"
scope: "디지털의료기기 및 연관 소프트웨어의 취약점 감시·공개·조치 라이프사이클 (VDP 포함)"
child_pro:
  - "[[PRO-MDCS-601_취약점_감시_공개_조치_절차_v1.0]]"
  - "[[PRO-MDCS-302_SBOM_관리_절차_v1.0]]"
standards: ["SaMD-CSMS", "ISO/IEC 29147", "ISO/IEC 30111", "FDA Premarket Cybersecurity 2023"]
related_standards: ["CISA CVD Guidelines", "CVSS v3.1/v4", "ISO/IEC 27001 A.8.8 (취약점 관리)"]
reuses: ["ISO/IEC 27001 A.8.8"]
status: draft
created: "2026-04-17"
updated: "2026-04-17"
retention: "상시"
tags: [POL, MDCS, SaMD-CSMS, vulnerability, VDP, tier-S]
tier: "S"
---

# 취약점 관리 정책 (감시·공개·조치) (POL-MDCS-006)

> 상위 방침: [[POL-MDCS-001_의료기기_사이버보안_기본방침_v1.0]]

## 1. 목적

본 정책은 디지털의료기기에서 확인되는 보안 취약점을 **감시(Monitoring) → 공개(Disclosure) → 조치(Remediation)** 의 일관된 라이프사이클로 관리하여, 취약점이 침해 사고로 발전하기 전에 적시에 완화·해소하기 위한 원칙을 규정한다.

## 2. 적용 범위

- 당사 제품의 자체 개발 코드 및 **제3자·오픈소스** 구성요소
- **시판 후(Post-market)** 취약점 감시 활동 (로그 분석·SBOM 기반 CVE 조회)
- **취약점 공개 프로그램(VDP)** 운영 및 외부 연구자 접수 채널
- 식품의약품안전처·의료서비스제공자·이용자와의 통보·협력 활동
- 해당 표준의 선택 실행 지침(recommended)은 **원칙적으로 준수**하며, 예외는 PSC 가 명시적으로 결정

## 3. 정책 원칙

1. **지속 감시(Continuous Monitoring)** — 정기적 보안 모니터링·로그 분석·SBOM 연동 CVE 추적을 통해 취약점을 조기에 식별한다.
2. **조정된 공개(Coordinated Disclosure)** — ISO/IEC 29147 에 따른 취약점 공개 프로세스를 운영하며, 공개 시점은 조치 상태·심각도를 고려하여 식품의약품안전처와 협의할 수 있다.
3. **CVSS 기반 우선순위** — 취약점의 심각도는 CVSS 와 임상·운영 영향을 종합하여 판정하며, 조치 SLA 를 심각도별로 차등 적용한다.
4. **레거시 포용(Legacy Inclusion)** — 지원 종료(EOS) 제품 및 레거시 기기의 취약점도 의료서비스제공자와 협력하여 위험 관리·패치 방안을 마련한다.
5. **조치 후 검증(Verify After Fix)** — 패치·업데이트 배포 이후에도 지속 감시를 통해 재발 여부를 확인하고 조치 효과를 검증한다.

## 4. 역할과 책임

| 역할 | 책임 |
|---|---|
| **CEO** | 본 정책 승인 |
| **Product Security Officer** | 본 정책 유지, 취약점 라이프사이클 총괄 |
| **PSC** | 공개 시점·SLA 예외·레거시 조치 심의 |
| **SBOM 관리자** | CVE/NVD 연동, 영향 컴포넌트 식별 |
| **개발팀 / QA** | 패치 개발·보안 테스트·무결성 검증 |
| **Regulatory Affairs** | 식품의약품안전처 통보, 공개 자료 규제 검토 |
| **홍보/고객지원** | 외부 연구자 접수·의료서비스제공자 공지 |
| **CSIRT** | 악용 징후 발견 시 침해대응 프로세스 연계 |

## 5. 준수 기준

- **감시 활동 계획**: 정기적 보안 모니터링, 로그 분석, 시판 후 감시, SBOM 활용을 포함하여 문서화한다.
- **통보 포함 정보**: 식품의약품안전처장 통보 시 상세 내용·심각도(CVSS)·영향·대응 방안을 반드시 포함한다.
- **VDP 채널**: 외부 연구자·의료서비스제공자가 취약점을 제보할 수 있는 공개 접수 채널(예: security@도메인)을 유지한다.
- **공개 자료**: 홈페이지 등에 공개할 경우 상세 내용·영향·대응 방안을 포함한 자료를 제공한다.
- **공개 시점 조정**: 해결 여부·심각도를 고려하여 필요한 경우 식품의약품안전처장과 협의를 통해 공개 시점을 결정할 수 있다.
- **조치 SLA (권장)**:
  - Critical (CVSS ≥ 9.0): 7일 이내 긴급 패치 또는 완화 조치
  - High (7.0~8.9): 30일 이내
  - Medium (4.0~6.9): 90일 이내
  - Low (< 4.0): 다음 정기 릴리스
- **제10조 연계**: 패치·업데이트 배포 시 무결성 검증·실패 대비 롤백·비인가 변경 방지를 준수한다.
- **레거시 패치**: 제15조에 따라 의료서비스제공자와 협력 방안을 마련한다.
- **조치 이후 감시**: 지속 보안 모니터링·감시를 통해 재발 여부를 확인한다.
- **문서화**: 감시·공개·조치 전 과정을 문서화하여 보관한다.

## 6. 관련 하위 절차 (PRO)

- [[PRO-MDCS-601_취약점_감시_공개_조치_절차_v1.0]] — 감시·공개·조치 라이프사이클
- [[PRO-MDCS-302_SBOM_관리_절차_v1.0]] — SBOM·CVE 연동
- [[PRO-MDCS-502_침해사고_대응_및_신고_절차_v1.0]] — 악용 징후 시 IR 연계
- [[PRO-MDCS-303_레거시_의료기기_관리_절차_v1.0]] — 레거시 패치 협력

## 7. 표준 매핑 (Traceability)

| 표준 조항 | Req-ID | 반영 위치 |
|---|---|---|
| SaMD-CSMS 제20조 제1호 (감시 활동 계획·문서화) | MDCS-R-201 | §5 감시 활동 계획 |
| SaMD-CSMS 제20조 제2호 (MSP 통보) | MDCS-R-202 | §4 역할 |
| SaMD-CSMS 제20조 제3호 (식약처·MSP 알림) | MDCS-R-203 | §5 통보 정보 |
| SaMD-CSMS 제20조 제4호 (통보 포함 정보) | MDCS-R-204 | §5 통보 포함 정보 |
| SaMD-CSMS 제20조 제5호 (MSP 협조) | MDCS-R-205 | §4 역할 |
| SaMD-CSMS 제21조 제1호 (홈페이지 공개) | MDCS-R-211 | §5 VDP 채널·공개 자료 |
| SaMD-CSMS 제21조 제2호 (공개 자료) | MDCS-R-212 | §5 공개 자료 |
| SaMD-CSMS 제21조 제3호 (공개 시점 조정) | MDCS-R-213 | §3-2 Coordinated Disclosure |
| SaMD-CSMS 제22조 제1호 (패치·업데이트 조치) | MDCS-R-221 | §5 조치 SLA, §5 제10조 연계 |
| SaMD-CSMS 제22조 제2호 (레거시 패치) | MDCS-R-222 | §3-4 Legacy Inclusion |
| SaMD-CSMS 제22조 제3호 (조치 후 감시) | MDCS-R-223 | §3-5 |
| SaMD-CSMS 제22조 제4호 (문서화) | MDCS-R-224 | §5 문서화 |

## 8. 출처 (source_citation)

```yaml
- type: guide
  file: "_inputs/01_표준원문/제20조 취약점 감시.pdf"
  locator: "pp.50-51"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제21조 취약점 공개.pdf"
  locator: "p.53"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제22조 취약점 조치.pdf"
  locator: "pp.55-56"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
```

> 참고: ISO/IEC 29147 취약점 공개, ISO/IEC 30111 취약점 처리 프로세스는 본 정책의 국제 정렬 기준으로 사용 (해당 표준 원문 `_inputs/03_해설서/` 미배치 상태).

## 9. 개정 이력

| 버전 | 일자 | 변경내용 | 승인자 |
|---|---|---|---|
| 1.0 | 2026-04-17 | 최초 제정 (SaMD-CSMS 제20·21·22조 기반) | CEO |
