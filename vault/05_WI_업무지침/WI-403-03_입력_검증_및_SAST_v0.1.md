---
type: WI
doc_id: "WI-403-03"
title: "입력 검증 및 SAST 운영 업무지침"
version: "0.1"
owner: "개발팀장"
reviewer: "QA 리드"
approver: "오동석"
scope: "입력 데이터 화이트리스트·타입·길이·범위 검증, SQL Injection·XSS·BOF 방어, SAST 도구 운영"
parent_pro: "[[PRO-MDCS-403_데이터_및_파일_보안_관리_절차_v1.0]]"
related_tmp: []
standards: ["SaMD-CSMS", "OWASP Top 10", "CWE Top 25"]
status: draft
created: "2026-04-17"
updated: "2026-04-17"
tags: [WI, MDCS, SaMD-CSMS, input-validation, SAST]
---

# 입력 검증 및 SAST 운영 업무지침 (WI-403-03)

> 상위 절차: [[PRO-MDCS-403_데이터_및_파일_보안_관리_절차_v1.0]] · §5 단계 4
> 연계: [[WI-201-03_SAST_DAST_운영_v0.1]]

## 1. 업무 목적

디지털의료기기 애플리케이션의 입력 구간(폼·API·CLI)에서 화이트리스트·타입·길이·범위 검증을 강제하고, SAST 를 통해 SQL Injection·XSS·버퍼 오버플로우(BOF) 등 OWASP Top 10/CWE Top 25 결함을 출시 전 차단한다.

## 2. 수행 주체

- **주 수행자**: 개발팀 개발자
- **검토자**: QA 리드, PSO
- **승인자**: 오동석 (보안 게이트)

## 3. 범위

- 모든 사용자 입력 구간(웹/모바일 폼, REST/gRPC API, CLI, 파일 입력)
- 제3자·오픈소스 구성요소 통합 지점
- 데이터베이스 파라미터 바인딩 구간

## 4. 입력 자료 / 산출물

- **Input**
  - 기능 명세의 입력 필드 정의
  - SAST 도구 라이선스·룰셋
- **Output**
  - 입력 검증 함수·라이브러리 적용 결과
  - SAST 리포트(Critical/High/Medium 분류)
  - 조치 계획·잔여 위험 기록

## 5. 수행 절차

### 5.1 사전 준비

1. 개발팀이 각 입력 필드의 허용 타입·길이·범위·정규식 패턴을 명세에 기재한다.
2. SAST 도구를 CI 파이프라인에 통합한다(예: SonarQube·Semgrep·CodeQL).
3. 심각도별 출시 차단 기준을 확정한다: Critical 0건, High 3건 이하(완화 계획 포함), Medium 이하 백로그.

### 5.2 수행 단계

1. **입력 검증 구현**
   - 클라이언트와 서버 양단에서 검증을 수행하되 서버를 신뢰 경계로 둔다.
   - 화이트리스트 우선, 블랙리스트는 보조 수단으로만 사용.
   - SQL: Prepared Statement/ORM 파라미터 바인딩만 허용. 문자열 연결 쿼리 금지.
   - XSS: 출력 인코딩(HTML·URL·JS Context 별), CSP 헤더 적용.
   - BOF: 안전 언어·라이브러리(Rust·Go·C++ modern safe patterns), 경계 검사 필수.
2. **SAST 실행**
   - 매 Pull Request 에서 Diff 스캔을 수행한다.
   - Main 브랜치에서는 전체 스캔을 일일 실행한다.
3. **결함 트리아지**
   - PSO 와 개발 리드가 스캔 결과를 주 1회 트리아지한다.
   - False Positive 는 근거와 함께 억제(Suppression) 기록한다.
4. **조치**
   - Critical 은 릴리스 차단, 즉시 수정.
   - High 는 30일 이내 수정 또는 완화 계획 승인.
   - Medium/Low 는 백로그 관리.
5. **교육·재사용**
   - 반복되는 결함 유형에 대해 분기별 개발자 교육을 실시한다.
   - 공통 검증 라이브러리를 팀 간 공유한다.
6. **릴리스 게이트 증빙**
   - 릴리스 시 SAST 최종 리포트와 잔여 위험 기록을 [[WI-201-07_릴리스_보안_게이트_v0.1]] 에 제출한다.

### 5.3 완료 조건

- [ ] 모든 입력 필드에 서버 측 화이트리스트 검증이 구현되었다
- [ ] SQL 은 Prepared Statement/ORM 파라미터 바인딩으로만 처리된다
- [ ] XSS 출력 인코딩·CSP 가 적용되었다
- [ ] SAST 가 CI 에 통합되어 PR 단위 스캔이 수행된다
- [ ] Critical SAST 결함이 0건이고 High 는 승인 계획으로 관리된다
- [ ] SAST 리포트·잔여 위험 기록이 릴리스 게이트에 제출되었다

## 6. 인터페이스 부서

- **QA**: DAST·펜테스트 결과와 SAST 교차 확인
- **PSO**: 트리아지 참여·예외 승인
- **DevOps**: CI 파이프라인 운영

## 7. 주의사항 / 예외 처리

### 7.1 레거시 코드 대규모 결함

초기 SAST 도입 시 다수 결함이 발견되는 경우, PSO 승인 아래 베이스라인(baseline) 설정으로 신규 결함만 게이트에 반영한다. 베이스라인은 12개월 이내 50% 이상 축소 목표로 관리한다.

### 7.2 제3자 라이브러리 결함

오픈소스 라이브러리 취약점은 [[WI-302-02_CVE_NVD_연동_v0.1]] 경로로 분리 관리한다. SAST 결과와 중복되는 경우 SBOM 기반 관리 쪽으로 통합한다.

### 7.3 False Positive 대량 발생

새 룰셋 도입으로 False Positive 가 10% 초과 시 룰셋 튜닝을 수행한다. 튜닝 동안 해당 룰은 경고 모드로 운영하며 Critical 판정은 유지.

### 7.4 긴급 핫픽스 SAST 스킵 요청

환자 안전 긴급 핫픽스에서 SAST 통과 불가 시 PSO + 오동석 공동 승인으로 예외 배포한다. 배포 직후 48시간 이내 SAST 통과 확인 재배포를 계획한다.

## 8. 연계 템플릿 / 기록

- 작성예시: [[EX-SDLC-002_SAST_트리아지_회의록_작성예시]]
- 기록 폴더: `08_REC_기록/` (REC-SDLC-{YYYY}-{###})

## 9. 출처 (source_citation)

```yaml
- type: guide
  file: "_inputs/01_표준원문/제07조 파일 및 입력 유효성.pdf"
  locator: "p.25 §4"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
- type: guide
  file: "_inputs/01_표준원문/제14조 개발 및 검증 활동.pdf"
  locator: "p.39 §2"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
```

## 10. 개정 이력

| 버전 | 일자 | 변경내용 | 승인자 |
|---|---|---|---|
| 0.1 | 2026-04-17 | 최초 초안 작성 | 오동석 |
