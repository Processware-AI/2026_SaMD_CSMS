---
type: POL
doc_id: "POL-MDCS-004"
title: "기술적·물리적 보안 통제 정책"
version: "1.0"
owner: "Chief Information Security Officer (오동석)"
reviewer: "Product Security Council (PSC)"
approver: "CEO"
scope: "디지털의료기기 및 운영 환경의 물리적·네트워크·접근·데이터·암호·유지관리에 관한 기술 통제 기본 규범"
child_pro:
  - "[[PRO-MDCS-101_보안_문서화_관리_절차_v1.0]]"
  - "[[PRO-MDCS-401_접근통제_및_인증_관리_절차_v1.0]]"
  - "[[PRO-MDCS-402_보안_통신_및_암호화_관리_절차_v1.0]]"
  - "[[PRO-MDCS-403_데이터_및_파일_보안_관리_절차_v1.0]]"
standards: ["SaMD-CSMS", "ISO/IEC 27001", "ISO/IEC 27002"]
related_standards: ["NIST SP 800-53", "개인정보보호법", "PIMS (ISO/IEC 27701)"]
reuses: ["ISO/IEC 27001 A.7 (물리보안)", "ISO/IEC 27001 A.8 (기술통제)", "ISO/IEC 27001 A.5.15-18 (접근통제)", "ISO/IEC 27001 A.13 (통신보안)"]
status: draft
created: "2026-04-17"
updated: "2026-04-17"
retention: "상시"
tags: [POL, MDCS, SaMD-CSMS, access-control, crypto, tier-S]
tier: "S"
---

# 기술적·물리적 보안 통제 정책 (POL-MDCS-004)

> 상위 방침: [[POL-MDCS-001_의료기기_사이버보안_기본방침_v1.0]]
> ISMS 를 이미 운용 중인 조직은 본 정책을 ISO/IEC 27001 A.7·A.8·A.13 통제와 **통합 적용** 가능.

## 1. 목적

본 정책은 디지털의료기기 및 운영 환경에 적용되는 **물리적·기술적 보안 통제**의 기본 규범을 정의하여, 비인가 접근·데이터 유출·통신 가로채기·악성코드·무결성 훼손을 예방·탐지·대응한다.

## 2. 적용 범위

- 디지털의료기기 본체 및 연관 구성요소(서버, 클라이언트, 네트워크 장비, 저장매체)
- 개발·검증·운영 환경(전산실, 서버실, 클라우드 인프라 포함)
- 기기와 송수신되는 **데이터**(개인정보·의료영상·진단결과 등 포함)
- 기기 및 연관 소프트웨어의 **유지관리 활동**(업데이트·패치·구성 변경)

## 3. 정책 원칙

1. **최소권한과 제로트러스트(Least Privilege & Zero Trust)** — 사용자·계정·서비스는 업무 수행에 필요한 최소 권한만 부여하며, 내·외부를 막론하고 명시적 인증·인가를 거친다.
2. **다층 방어(Defense in Depth)** — 물리(구역·CCTV) → 네트워크(분리·방화벽) → 시스템(하드닝·AV) → 데이터(암호화·FIM) → 애플리케이션(입력 검증) 계층으로 중첩 방어한다.
3. **승인된 강암호만 사용** — AES-256, SHA-256/512 등 업계 표준 알고리즘만 허용하며 DES·MD5·SHA-1 등 취약 알고리즘을 금지한다.
4. **무결성 우선(Integrity First)** — 의료기기의 소프트웨어·펌웨어·주요 데이터는 디지털 서명·해시·FIM 으로 상시 무결성을 검증한다.
5. **개인정보 보호 우선(Privacy by Default)** — 개인정보 수집 최소화·암호화·비식별화·접근 통제·보존 기간 준수를 기본값으로 설계한다.

## 4. 역할과 책임

| 역할 | 책임 |
|---|---|
| **CEO** | 본 정책 승인 |
| **오동석** | 본 정책 유지, 기술 통제 표준·가이드라인 승인 |
| **SecOps / 보안운영팀** | 통제 운영, 모니터링, 사고 탐지 |
| **시설 관리팀 (Facility)** | 물리 보안(출입·CCTV·UPS·항온항습) 운영 |
| **네트워크·인프라팀** | 네트워크 분리·방화벽·VPN·NAC 운영 |
| **IAM 관리자** | 계정 생명주기, MFA, 권한 검토 |
| **암호키 관리자 (KMS Admin)** | 키 생성·로테이션·백업·폐기 |
| **Privacy Officer (DPO)** | 개인정보 암호화·비식별화·보존 관리 |

## 5. 준수 기준

- **물리 보안**: 보안구역 지정, 출입 기록 관리, CCTV·UPS·소화·침입감지 설비 운영; 전산실·서버실은 이중 잠금·다단계 출입·항온항습을 적용한다.
- **네트워크 보안**: 네트워크 분리/VLAN, 방화벽·IPS, 포트 보안, NAC, WPA3 이상 무선 보안; 이동식 매체는 물리적 제한·화이트리스트로 통제한다.
- **암호화 통신**: 내·외부 통신은 HTTPS/TLS, VPN/IPsec, SSH 로 암호화; API 보안·보안 게이트웨이를 운영한다.
- **접근 통제**: RBAC·MFA·강력 패스워드·세션 자동종료·원격 접속 기본 차단을 적용한다.
- **데이터 보안**: 개인정보·민감 데이터는 암호화·비식별화·전송 시 이중 보안; DB 는 최소 권한·주기적 계정 점검.
- **암호키 관리**: 키·데이터 분리 저장, 주기적 로테이션, MFA 기반 접근, HSM/TPM/KMS 사용, 보안 부팅·펌웨어 무결성.
- **유지관리**: 업데이트는 공식 채널·디지털 서명·해시·보안 테스트 후 배포, 실패 대비 롤백·백업·복원 기능 제공, 변경 로그 관리.
- **개인정보**: 수집·보관 시 암호화, 민감 데이터 접근 이력 관리, 보존기간 경과 시 영구 삭제.

## 6. 관련 하위 절차 (PRO)

- [[PRO-MDCS-101_보안_문서화_관리_절차_v1.0]] — 보안 활동 문서화·증적
- [[PRO-MDCS-401_접근통제_및_인증_관리_절차_v1.0]] — 계정·권한·세션·원격접속 (제05조 중심)
- [[PRO-MDCS-402_보안_통신_및_암호화_관리_절차_v1.0]] — 네트워크·암호화 키 (제04·09조)
- [[PRO-MDCS-403_데이터_및_파일_보안_관리_절차_v1.0]] — 파일 유효성·DB·전송·비식별화 (제07·08조)

## 7. 표준 매핑 (Traceability)

| 표준 조항 | Req-ID | 반영 위치 |
|---|---|---|
| SaMD-CSMS 제03조 (물리보안) | MDCS-R-031~034 | §5 물리 보안 |
| SaMD-CSMS 제04조 (보안 통신) | MDCS-R-041~043 | §5 네트워크·암호화 통신 |
| SaMD-CSMS 제05조 (권한·인증) | MDCS-R-051~054 | §5 접근 통제 |
| SaMD-CSMS 제06조 (기술적 보안·개인정보) | MDCS-R-061~064 | §3-4, §5 개인정보 |
| SaMD-CSMS 제07조 (파일·입력 유효성) | MDCS-R-071~074 | §5 데이터 보안 |
| SaMD-CSMS 제08조 (데이터 보안) | MDCS-R-081~084 | §5 데이터 보안, §3-3 |
| SaMD-CSMS 제09조 (암호화 키) | MDCS-R-091~093 | §5 암호키 관리 |
| SaMD-CSMS 제10조 (유지 관리) | MDCS-R-101~103 | §5 유지관리 |
| SaMD-CSMS 제12조 (AI 데이터·모델 보안) | MDCS-R-121~123 | §5 데이터 보안 (AI 확장) |

## 8. 출처 (source_citation)

```yaml
- type: guide
  file: "_inputs/01_표준원문/제03조 물리적 보안.pdf"
  locator: "pp.16-17"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제04조 보안 통신.pdf"
  locator: "pp.18-19"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제05조 권한 및 인증.pdf"
  locator: "pp.20-21"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제06조 기술적 보안.pdf"
  locator: "pp.22-23"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제07조 파일 및 입력 유효성.pdf"
  locator: "pp.24-25"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제08조 데이터 보안.pdf"
  locator: "pp.26-27"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제09조 암호화 키 관리.pdf"
  locator: "pp.28-29"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제10조 유지 관리.pdf"
  locator: "pp.30-31"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
```

## 9. 개정 이력

| 버전 | 일자 | 변경내용 | 승인자 |
|---|---|---|---|
| 1.0 | 2026-04-17 | 최초 제정 (SaMD-CSMS 제03~10조 통합) | CEO |
