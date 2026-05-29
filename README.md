# 📚 Pullit — T셀파 문제은행 서비스

> OCR 엔진을 통한 효율적인 문제 등록과 자동 출제 시스템을 바탕으로, 교육 현장의 업무 생산성을 혁신하는 문제은행 플랫폼


[![Java](https://img.shields.io/badge/Java-007396?style=flat&logo=java&logoColor=white)](https://java.com)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=flat&logo=vue.js&logoColor=white)](https://vuejs.org)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white)](https://mysql.com)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)](https://docker.com)

---

## 📌 프로젝트 개요

교사와 관리자의 시험 출제 업무 부담을 줄이기 위해 개발한 문제은행 플랫폼입니다.
OCR로 문항을 디지털 자산화하고, 과목·단원·난이도 기반 자동 출제 및 실시간 CBT 환경을 제공합니다.

- **개발 기간**: 2025.08 ~ 2025.09 (2개월)
- **개발 인원**: 6명 (풀스택)
- **역할**: 시험 관리, 시험 결과 리포트, 데이터 시각화, PDF 다운로드

---

## ✨ 주요 기능

- 📝 **문제은행**: 과목·단원·난이도 설정 기반 시험지 자동 생성 및 출력
- 💻 **실시간 CBT**: Computer Based Testing 환경 제공
- 📊 **성취도 분석**: Chart.js 기반 통계 시각화 대시보드
- 📄 **PDF 리포트**: 상세 성적 리포트 다운로드
- 🔢 **수식 렌더링**: KaTeX 기반 수학 수식 정확 출력

---

## 🛠️ 기술 스택

| 분류 | 기술 |
|------|------|
| Frontend | Vue.js, JavaScript, HTML5, CSS3, Bootstrap, Chart.js, KaTeX |
| Backend | Java, Spring Boot, Spring Framework, JPA |
| Database | MySQL |
| DevOps | AWS EC2, Docker, GitHub Actions, Nginx |

---

## 👤 본인 기여 (오상진)

| 분류 | 담당 내용 |
|------|-----------|
| **시험 관리 페이지** | 진행중/완료된 시험 리스트 조회, 과목 코드 → 한글 과목명 변환, 과목별 필터링 탭 구성 |
| **시험 결과 리포트** | `attempt_id` 기반 응시 기록 조회, 시험지·정답·사용자 답변 데이터 출력 |
| **문항 상세 조회** | `question_id` 기반 문항 상세보기, 기본/상세 리포트 공통 모달 컴포넌트 설계 |
| **수식 렌더링** | KaTeX 연동 + 정규식 기반 파싱으로 수학 기호·수식 웹 환경에서 정확 출력 |
| **데이터 시각화** | Chart.js 기반 성취도 분석 차트, API 데이터 → Vue 반응형 → Chart 데이터 변환 파이프라인 구성 |
| **렌더링 최적화** | `watch` + 디바운싱 적용으로 불필요한 차트 렌더링 최소화 |
| **PDF 리포트** | `html2canvas` + `jsPDF` 기반 상세 리포트 PDF 생성, 차트 이미지 변환 삽입으로 품질 보완 |
| **PDF UX** | 파일명 자동 생성 및 스타일 최적화, 비동기 다운로드로 속도 약 30% 향상 |

---

## 🔥 트러블슈팅

### 1. 수식 포함 문항 렌더링 깨짐

**문제 상황**
수학 기호와 수식이 포함된 문항이 일반 텍스트로 출력되거나 깨지는 문제 발생

**해결 방법**
KaTeX 라이브러리 연동 후 정규식 기반 파싱으로 수식 구간을 감지해 렌더링 처리

**결과**
수식·기호 포함 문항이 웹 환경에서 정확하고 끊김 없이 출력

---

### 2. 차트 불필요한 재렌더링으로 성능 저하

**문제 상황**
API 데이터 변경 시마다 차트가 재렌더링되어 성능 저하 발생

**해결 방법**
Vue `watch` + 디바운싱 적용으로 데이터 변경 감지 후 일정 시간 내 추가 변경이 없을 때만 차트 업데이트

**결과**
불필요한 렌더링 제거, 대용량 데이터 환경에서도 끊김 없는 사용자 경험 확보

---

### 3. PDF 내 차트 이미지 품질 저하

**문제 상황**
Chart.js 차트를 PDF로 변환 시 해상도가 낮아 데이터가 흐릿하게 출력되는 문제

**해결 방법**
차트를 `html2canvas`로 고해상도 이미지로 먼저 변환 후 `jsPDF`에 삽입, 크기·해상도 조건 최적화

**결과**
대용량 성적 데이터도 해상도 저하 없이 안정적으로 출력

---

## 🏗️ 시스템 아키텍처

```
[사용자 (교사/학생)]
   │
   ▼
[Vue.js Frontend]
   ├── 시험 관리 (과목별 필터링)
   ├── 성취도 차트 (Chart.js + 디바운싱)
   ├── 수식 렌더링 (KaTeX + 정규식 파싱)
   └── PDF 다운로드 (html2canvas + jsPDF)
   │  REST API
   ▼
[Spring Boot Backend]
   ├── 시험 관리 API
   ├── 응시 기록 조회 (attempt_id 기반)
   ├── 문항 상세 조회 (question_id 기반)
   └── JPA (MySQL)
```

---


## 🎬 데모 영상

- [YouTube 데모 영상](https://youtu.be/94fo7PGZqq8)

---

## 📎 관련 링크

- 🔗 [Backend GitHub](https://github.com/ProblematicDevelopers/pullit-backend)
- 🔗 [Frontend GitHub](https://github.com/ProblematicDevelopers/pullit-frontend)
- 📓 [Notion 프로젝트 문서](https://granite-engineer-6d1.notion.site/T-Fullit-2706f9ef939f8113bd5ff6a081bb3ea3)

---

> 이 README는 본인 기여 범위를 중심으로 작성되었습니다.
