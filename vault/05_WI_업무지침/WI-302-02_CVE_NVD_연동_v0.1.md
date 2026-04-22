---
type: WI
doc_id: "WI-302-02"
title: "CVE·NVD 연동 업무지침"
version: "0.1"
owner: "SBOM 관리자"
reviewer: "PSO"
approver: "CISO"
scope: "SBOM 기반 CVE/NVD 주기적 조회, 매칭 시 영향 제품·컴포넌트 식별 및 조치 티켓 연계"
parent_pro: "[[PRO-MDCS-302_SBOM_관리_절차_v1.0]]"
related_tmp: []
standards: ["SaMD-CSMS"]
status: draft
created: "2026-04-17"
updated: "2026-04-17"
tags: [WI, MDCS, SaMD-CSMS, SBOM, CVE]
---

# CVE·NVD 연동 업무지침 (WI-302-02)

> 상위 절차: [[PRO-MDCS-302_SBOM_관리_절차_v1.0]] · §5 단계 5~7

## 1. 업무 목적

SBOM 에 포함된 구성요소를 CVE/NVD·CISA KEV 와 주기적으로 매칭하여 신규 취약점을 조기 식별하고, 영향 받는 제품·컴포넌트·버전을 특정하여 패치·업데이트 절차로 연계한다.

## 2. 수행 주체

- **주 수행자**: SBOM 관리자
- **검토자**: PSO, 개발팀
- **승인자**: CISO

## 3. 범위

- 활성 릴리스의 SBOM
- 레거시(지원 중) 제품의 SBOM
- 내부 개발·시험 환경

## 4. 입력 자료 / 산출물

- **Input**
  - SBOM JSON/YAML
  - CVE/NVD 피드·CISA KEV·벤더 공지
- **Output**
  - 매칭 리포트(VUL 티켓)
  - 영향 분석 결과

## 5. 수행 절차

### 5.1 사전 준비

1. Dependency-Track·Trivy 등 자동 매칭 도구를 운영.
2. CVE 피드를 일일 동기화.
3. False Positive 억제 규칙을 관리.

### 5.2 수행 단계

1. **자동 매칭 (주 1회 이상)**
   - 모든 활성 SBOM 에 대해 CVE 매칭 잡 실행.
2. **신규 매칭 처리**
   - 신규 매칭 결과에 대해 [[WI-601-01_취약점_감시_및_접수_v0.1]] 경로로 VUL ID 발행.
3. **영향 식별**
   - 영향 받는 제품·버전·설치 MSP 를 식별.
   - 임상 영향 초기 평가.
4. **트리아지**
   - 악용 가능성(Exploitable)·KEV 등재 여부·CVSS·임상 영향으로 우선순위 결정.
   - False Positive 는 근거·기간 명시하고 억제.
5. **조치 연계**
   - [[PRO-MDCS-601_취약점_감시_공개_조치_절차_v1.0]] 의 조치 SLA 로 이관.
6. **재연동**
   - 패치 후 재스캔하여 해소 확인.

### 5.3 완료 조건

- [ ] CVE 매칭이 주 1회 이상 자동 실행된다
- [ ] 신규 매칭이 24시간 이내 VUL 티켓으로 발행된다
- [ ] 영향 제품·버전·MSP 식별이 수행된다
- [ ] KEV 등재·Exploitable 여부가 우선순위에 반영된다
- [ ] False Positive 억제 기록이 유지된다
- [ ] 패치 후 재스캔으로 해소가 확인된다

## 6. 인터페이스 부서

- **PSO**: 우선순위 리뷰
- **CSIRT**: KEV·악용 중 취약점의 IR 연계
- **개발팀**: 영향 확정

## 7. 주의사항 / 예외 처리

### 7.1 CVE 피드 지연

NVD 지연 시 CISA KEV·벤더 공지 병행 활용. 자체 위협 인텔 신규 소스 추가 검토.

### 7.2 매칭 오탐

패키지명·버전 오인식으로 오탐 발생 시 매칭 규칙 수정, PURL 정확도 개선. 억제는 근거 필수.

### 7.3 레거시 제품

EOS 전 레거시 제품도 주기 매칭 대상. 패치 불가 시 [[WI-303-03_레거시_취약점_패치_협력_v0.1]] 로 이관.

### 7.4 오픈소스 maintainer 패치 미제공

유지보수 중단된 오픈소스는 포크·자체 패치 또는 교체 평가. 결정 기록 필수.

## 8. 연계 템플릿 / 기록

- 작성예시: [[EX-SBOM-002_CVE매칭_리포트_작성예시]]
- 기록 폴더: `08_REC_기록/` (REC-SBOM-{YYYY}-{###})

## 9. 출처 (source_citation)

```yaml
- type: guide
  file: "_inputs/01_표준원문/제16조 소프트웨어 구성요소 명세서(SBOM) 관리 활동.pdf"
  locator: "p.42 §2"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
```

## 10. 개정 이력

| 버전 | 일자 | 변경내용 | 승인자 |
|---|---|---|---|
| 0.1 | 2026-04-17 | 최초 초안 작성 | CISO |
