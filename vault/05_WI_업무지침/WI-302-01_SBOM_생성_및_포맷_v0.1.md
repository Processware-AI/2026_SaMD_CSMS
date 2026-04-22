---
type: WI
doc_id: "WI-302-01"
title: "SBOM 생성 및 포맷 업무지침"
version: "0.1"
owner: "SBOM 관리자"
reviewer: "PSO"
approver: "CISO"
scope: "빌드 파이프라인에서 SPDX·CycloneDX 포맷의 SBOM 자동 생성 및 필수 필드 검증"
parent_pro: "[[PRO-MDCS-302_SBOM_관리_절차_v1.0]]"
related_tmp:
  - "[[TMP-SBOM-001_SBOM_검증_체크리스트_v0.1]]"
standards: ["SaMD-CSMS", "SPDX 2.3", "CycloneDX 1.5", "CISA SBOM Minimum Elements"]
status: draft
created: "2026-04-17"
updated: "2026-04-17"
tags: [WI, MDCS, SaMD-CSMS, SBOM, top10]
---

# SBOM 생성 및 포맷 업무지침 (WI-302-01)

> 상위 절차: [[PRO-MDCS-302_SBOM_관리_절차_v1.0]] · §5 단계 1~2

## 1. 업무 목적

모든 릴리스에 대해 SPDX 또는 CycloneDX 표준 포맷의 SBOM 을 빌드 파이프라인에서 자동 생성하고, CISA 최소 필수 필드(구성요소명·버전·라이선스·출처·해시) 를 충족시켜 취약점 추적·규제 대응·침해 영향 식별의 기반을 마련한다.

## 2. 수행 주체

- **주 수행자**: SBOM 관리자
- **검토자**: R&D 리드, PSO
- **승인자**: CISO

## 3. 범위

- 자사 개발 소스·바이너리
- 제3자·오픈소스 구성요소
- 컨테이너 이미지·기반 OS 패키지

## 4. 입력 자료 / 산출물

- **Input**
  - 빌드 아티팩트·매니페스트 파일
  - SBOM 생성 도구(Syft·Trivy·Dependency-Track)
- **Output**
  - SPDX/CycloneDX JSON 또는 YAML
  - [[TMP-SBOM-001_SBOM_검증_체크리스트_v0.1]] 완료본

## 5. 수행 절차

### 5.1 사전 준비

1. SBOM 관리자가 조직 표준 포맷을 확정한다(기본 CycloneDX JSON, 규제 제출용 SPDX 동시 제공).
2. 빌드 파이프라인(GitHub Actions·GitLab CI 등) 에 SBOM 생성 단계를 추가.
3. CISA 최소 필드 7종 체크리스트를 유지.

### 5.2 수행 단계

1. **자동 생성**
   - 빌드 완료 시 Syft·Trivy 등이 SBOM 을 생성.
   - 컨테이너 이미지는 레이어별로 스캔 후 병합.
2. **필드 검증**
   - 구성요소명·버전·공급자·라이선스·출처(URL/PURL)·해시·의존성 관계·작성자 정보 확인.
   - 누락 시 빌드 실패 처리.
3. **서명·저장**
   - SBOM 파일에 디지털 서명 추가.
   - 안전한 저장소(Artifact Registry) 에 버전 태그와 함께 저장.
4. **배포 패키지 포함**
   - 릴리스 아티팩트와 함께 SBOM 을 배포.
5. **변경 감지**
   - 이전 릴리스 대비 추가·제거·변경 컴포넌트를 Diff 로 자동 계산.
6. **검증 체크리스트**
   - [[TMP-SBOM-001_SBOM_검증_체크리스트_v0.1]] 작성·승인.

### 5.3 완료 조건

- [ ] 모든 릴리스에 SPDX 또는 CycloneDX SBOM 이 동반된다
- [ ] CISA 최소 7개 필드가 모두 충족된다
- [ ] 컨테이너 이미지가 레이어별로 병합 스캔되었다
- [ ] SBOM 파일에 디지털 서명이 추가되었다
- [ ] 이전 릴리스 대비 Diff 가 산출된다
- [ ] 검증 체크리스트가 승인되었다

## 6. 인터페이스 부서

- **DevOps**: CI 파이프라인 SBOM 단계 유지
- **PSO**: 필수 필드 검증 기준 갱신
- **법무**: 라이선스 호환성 검토

## 7. 주의사항 / 예외 처리

### 7.1 상용 SDK 의 SBOM 부재

상용 SDK 가 SBOM 을 제공하지 않는 경우 SBOM 관리자가 공급사에 공식 요청하고, 미제공 시 리스크를 [[WI-301-03_위험_평가_보고서_작성_v0.1]] 에 등록. 대안 제품 평가.

### 7.2 동적 의존성

런타임 동적 로딩 의존성은 정적 SBOM 에 포함되지 않으므로 런타임 SBOM(RTSBOM) 또는 관찰 로그로 보완한다.

### 7.3 대용량 SBOM 성능 이슈

SBOM 크기가 수십 MB 를 초과하면 조회 성능을 위해 데이터베이스 기반 SBOM 저장소(Dependency-Track) 에 적재하고 파일은 보조로 유지.

### 7.4 포맷 버전 변경

SPDX·CycloneDX 메이저 버전 업그레이드 시 기존 SBOM 의 마이그레이션·호환성 검증. 6개월 병행 제공 기간 운영.

## 8. 연계 템플릿 / 기록

- 템플릿: [[TMP-SBOM-001_SBOM_검증_체크리스트_v0.1]]
- 작성예시: [[EX-SBOM-001_SBOM_검증_체크리스트_작성예시]]
- 기록 폴더: `08_REC_기록/` (REC-SBOM-{YYYY}-{###})

## 9. 출처 (source_citation)

```yaml
- type: guide
  file: "_inputs/01_표준원문/제16조 소프트웨어 구성요소 명세서(SBOM) 관리 활동.pdf"
  locator: "p.42 §1"
  retrieved_at: "2026-04-17"
  license: "공공저작물 추정 — 확인 필요"
  paraphrase_only: true
```

## 10. 개정 이력

| 버전 | 일자 | 변경내용 | 승인자 |
|---|---|---|---|
| 0.1 | 2026-04-17 | 최초 초안 작성 (Top10 5위 WI) | CISO |
