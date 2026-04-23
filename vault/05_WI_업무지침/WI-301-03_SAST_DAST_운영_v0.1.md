---
type: WI
doc_id: "WI-301-03"
title: "SAST·DAST 운영 업무지침"
version: "0.1"
owner: "QA 리드"
reviewer: "PSO"
approver: "오동석"
scope: "CI 파이프라인에서 SAST·DAST 실행, 결함 트리아지·수정 SLA·게이트 연동"
parent_pro: "[[PRO-MDCS-301_보안_SDLC_절차_v1.0]]"
related_tmp: []
standards: ["SaMD-CSMS", "OWASP Top 10"]
status: draft
created: "2026-04-17"
updated: "2026-04-17"
tags: [WI, MDCS, SaMD-CSMS, SAST, DAST]
---

# SAST·DAST 운영 업무지침 (WI-201-03)

> 상위 절차: [[PRO-MDCS-301_보안_SDLC_절차_v1.0]] · §5 단계 6~7
> 연계: [[WI-403-03_입력_검증_및_SAST_v0.1]]

## 1. 업무 목적

SAST(정적 분석) 와 DAST(동적 분석) 를 CI 파이프라인과 QA 환경에 통합·운영하여 릴리스 전 Critical·High 취약점의 소스·실행 환경 결함을 조기 검출한다.

## 2. 수행 주체

- **주 수행자**: QA 엔지니어
- **검토자**: PSO, 개발팀
- **승인자**: 오동석 (릴리스 게이트)

## 3. 범위

- 소스 리포지토리 전체
- QA·스테이징 환경의 실행 애플리케이션
- API·웹·모바일 대상 DAST

## 4. 입력 자료 / 산출물

- **Input**
  - SAST/DAST 도구 라이선스 및 룰셋
  - 릴리스 게이트 기준
- **Output**
  - SAST·DAST 스캔 리포트
  - 트리아지·조치 이력

## 5. 수행 절차

### 5.1 사전 준비

1. QA 리드가 SAST·DAST 도구를 선정·라이선스 관리한다.
2. CI 파이프라인에 SAST 실행 단계(PR·Main) 를 추가.
3. DAST 대상 URL·인증 방법을 사전 등록.

### 5.2 수행 단계

1. **SAST 실행**
   - PR 에서 변경 파일 대상 Diff 스캔.
   - Main 에서 전체 스캔 일일 실행.
   - 결과를 심각도로 분류(Critical·High·Medium·Low).
2. **DAST 실행**
   - QA·스테이징 환경에 주간 전체 스캔.
   - API 스캔은 OpenAPI 스펙 기반 자동 생성.
3. **트리아지**
   - PSO + 개발 리드가 주 1회 결과 검토.
   - False Positive 는 억제 근거·기간 명시해 기록.
   - 진성 결함은 티켓 발행.
4. **수정 SLA**
   - Critical: 릴리스 차단, 즉시 수정.
   - High: 30일 이내.
   - Medium: 90일 이내.
   - Low: 백로그.
5. **재검증**
   - 수정 완료 후 재스캔으로 해소 확인.
6. **게이트 연동**
   - [[WI-201-07_릴리스_보안_게이트_v0.1]] 에 최신 리포트·잔여 위험 제출.

### 5.3 완료 조건

- [ ] SAST 가 PR·Main CI 에 통합되어 있다
- [ ] DAST 주간 스캔이 QA·스테이징에 실행된다
- [ ] 주 1회 트리아지가 수행된다
- [ ] Critical 결함이 릴리스 차단 기준에 반영된다
- [ ] False Positive 억제가 근거와 함께 기록된다
- [ ] 최신 리포트가 릴리스 게이트에 제출된다

## 6. 인터페이스 부서

- **개발팀**: 결함 수정
- **PSO**: 트리아지 참여·예외 승인
- **DevOps**: CI 파이프라인 운영

## 7. 주의사항 / 예외 처리

### 7.1 도구 라이선스 만료

라이선스 만료로 스캔 중단 위험 시 QA 리드가 30일 전 갱신 요청. 만료 발생 시 무료·오픈소스 도구(Semgrep·ZAP) 로 임시 대체.

### 7.2 False Positive 대량 발생

룰셋 업데이트로 False Positive 가 급증하면 해당 룰 경고 모드로 전환하고 튜닝 진행. 베이스라인 재설정은 PSO 승인.

### 7.3 DAST 환경 의존성 장애

스테이징 환경 장애로 DAST 불가 시 컨테이너 기반 임시 환경 구성. 복구 후 누락 기간 보충 스캔.

### 7.4 비공개 API

인증·시간 기반 접근 제한으로 DAST 커버가 어려운 API 는 QA 계정 전용 스캔 경로 설정. 프로덕션 자격증명 사용 절대 금지.

## 8. 연계 템플릿 / 기록

- 작성예시: [[EX-SDLC-002_SAST_트리아지_회의록_작성예시]]
- 기록 폴더: `08_REC_기록/` (REC-SDLC-{YYYY}-{###})

## 9. 출처 (source_citation)

```yaml
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
