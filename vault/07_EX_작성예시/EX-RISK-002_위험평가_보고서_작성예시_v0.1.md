---
type: EX
doc_id: "EX-RISK-002"
title: "위험평가 보고서 작성예시"
version: "0.1"
parent_tmp: "[[TMP-RISK-002_위험평가_보고서_v0.1]]"
scope: "SaMD 사이버보안 가상 사례"
status: draft
created: "2026-04-22"
updated: "2026-04-22"
tags: [EX, MDCS, SaMD-CSMS, sample]
---

# 위험평가 보고서 작성예시 (EX-RISK-002)

> 원본 양식: [[TMP-RISK-002_위험평가_보고서_v0.1]]

> **이 문서는 교육용 예시로, 실제 기록(REC)이 아닙니다.**

---

## 1. 개요

| 항목 | 내용 |
|---|---|
| 제품·버전 | MediGuard CGM App v2.3.0 (혈당 연속 모니터링 SaMD) |
| 평가 범위 | 클라이언트 앱(iOS/Android) + 클라우드 API 서버 + BLE 통신 구간 |
| 평가 기간 | 2026-03-10 ~ 2026-04-05 |
| 참여자 | 김보안(PSO), 이개발(Lead Dev), 박임상(Safety Engineer), 정QA(QA팀장) |
| 변경 이력 | v1.0 초안(2026-04-05), v1.1 PSC 심의 반영(2026-04-12) |

## 2. 자산·공격 표면

| 자산 | 민감도 | 진입점 | 신뢰경계 |
|---|---|---|---|
| CGM 센서 데이터 (실시간 혈당값) | 매우 높음 | BLE 패킷, API /v2/glucose | 기기 ↔ 앱, 앱 ↔ 클라우드 |
| 사용자 인증 토큰 (JWT) | 높음 | 앱 로컬 스토리지, API 헤더 | 앱 내부, TLS 터널 |
| 의사 처방 알림 채널 | 높음 | FCM Push, WebSocket | 클라우드 ↔ 의사 단말 |
| 펌웨어 업데이트 패키지 | 높음 | OTA 서버 엔드포인트 | 클라우드 ↔ 센서 |
| 관리자 콘솔 | 높음 | HTTPS 443 | 내부 VPN 전용 |

## 3. 위협 식별(STRIDE 요약)

| THR-ID | 요약 | 심각도 | 가능성 |
|---|---|---|---|
| THR-001 | BLE 스니핑으로 혈당 원시값 도청 (Disclosure) | High | Medium |
| THR-002 | JWT 만료 미검증 → 탈취 토큰 재사용 (Tampering/Elevation) | Critical | Medium |
| THR-003 | OTA 서명 검증 우회 → 악성 펌웨어 배포 (Tampering) | Critical | Low |
| THR-004 | API /glucose 엔드포인트 과부하 → 알림 지연 (Denial of Service) | High | Low |
| THR-005 | 관리자 콘솔 무차별 대입 (Elevation of Privilege) | High | Medium |

## 4. 취약점 식별

| 출처 | 항목 수 | 비고 |
|---|---|---|
| SAST | 7 | Semgrep; SQL Injection 2건(Low), 하드코딩 시크릿 1건(High) 포함 |
| DAST | 4 | OWASP ZAP; JWT 알고리즘 None 허용(Critical) 확인 |
| Fuzzing | 3 | AFL++; API 파서 크래시 2건(High), 경계값 오류 1건(Medium) |
| 펜테스트 | 5 | 외부 보안업체; BLE 재전송 공격 실증(High) 포함 |
| SBOM-CVE | 6 | log4j-core 1.2.17 CVE-2021-44228(Critical), OpenSSL 1.0.2 다수 |

## 5. 통제 조치

| THR-ID/VUL-ID | 통제 유형 | 구현 상태 | 검증 상태 |
|---|---|---|---|
| THR-001 | BLE AES-128 암호화 적용 | 완료 | 펜테스트 재검증 통과 |
| THR-002 / DAST-01 | JWT 만료 15분·서명 알고리즘 HS256 고정 | 완료 | DAST 재스캔 통과 |
| THR-003 | OTA 패키지 RSA-PSS 서명 검증 로직 추가 | 완료 | 코드리뷰 + 단위 테스트 |
| THR-004 | API Rate Limiting 100 req/min/IP | 완료 | 부하 테스트 통과 |
| THR-005 | MFA 강제 + 계정 잠금(5회 실패) | 완료 | 수동 검증 완료 |
| SBOM-CVE-01 | log4j-core → 2.20.0 업그레이드 | 완료 | SCA 재스캔 통과 |
| SBOM-CVE-02 | OpenSSL → 3.0.x 업그레이드 | 진행 중 | 미완료(목표: 2026-05-15) |

## 6. 잔여 위험·수용

| ID | 통제 후 점수 | 수용자 | 수용 조건 | 모니터링 방안 |
|---|---|---|---|---|
| RES-001 (OpenSSL 구버전) | Medium (CVSS 5.3) | PSC | 2026-05-15까지 완료 예정; 운영 환경 격리 유지 | 주간 SCA 재스캔, SBOM 변경 알림 |
| RES-002 (BLE 거리 제한 미구현) | Low (CVSS 3.1) | PSO | 사용 환경(병원)에서 물리적 근접 공격 가능성 매우 낮음 | 분기별 재평가 |

## 7. 종합 결론

- 릴리스 가능 여부: **조건부 릴리스 가능** (OpenSSL 업그레이드 완료 후 운영 배포)
- 주요 권고 사항: ① OpenSSL 3.0.x 업그레이드 2026-05-15까지 완료 ② SBOM 자동 모니터링 파이프라인 구축 ③ BLE 펌웨어 업데이트 주기 분기 → 월간 전환 검토

## 8. 승인

| 단계 | 역할 | 성명 | 일자 |
|---|---|---|---|
| 내부 검토 | Safety/QA | 박임상 / 정QA | 2026-04-12 |
| 심의 | PSC | 김보안 (위원장) | 2026-04-14 |
| Critical 수용 | CEO | 한대표 | — (Critical 없음, 불필요) |
| 최종 승인 | 오동석 | 오동석 | 2026-04-15 |

---

## 작성 요령

- **자산·공격 표면**: 모든 데이터 흐름 경계(신뢰경계)를 명시한다. DFD(데이터 흐름도) 기준 Trust Boundary를 식별하면 누락을 방지할 수 있다.
- **위협 식별**: STRIDE 범주(Spoofing/Tampering/Repudiation/Disclosure/DoS/Elevation)별로 최소 1건 이상 식별하며, THR-ID는 추적 매트릭스와 연결 가능하도록 일관되게 부여한다.
- **취약점 식별**: 도구별 항목 수를 기재하되, 주요 CVE·결함은 별도 번호(예: DAST-01)를 부여하여 섹션5 통제 조치와 연결한다.
- **잔여 위험**: '수용 조건'은 기간·환경·모니터링 방안을 포함해야 하며, 단순 '수용함'만 기재 시 감사 지적 사항이 된다.

---

## 잘못된 기재 사례

### NG 사례 — 위협 식별 과소·통제 검증 누락

| THR-ID | 요약 | 심각도 | 가능성 |
|---|---|---|---|
| THR-001 | 인증 취약점 | High | Medium |

통제 조치: 패치 적용 완료

**문제점**: 위협 ID가 1건만 식별되어 STRIDE 전체 범주 미커버. 통제 조치에 구현 상태와 검증 상태가 없어 실제 이행 여부 확인 불가. ISO 14971 §10 요구사항 미충족.

**올바른 예시**: STRIDE 6개 범주를 모두 검토하고, 각 통제 조치에 구현 상태(완료/진행 중)와 검증 방법(DAST 재스캔/코드리뷰 등)을 명기한다.
