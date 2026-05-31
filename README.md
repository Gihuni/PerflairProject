# 🏷️ Perflair: Fragrance E-Commerce Platform

> **데이터 기반의 효율적인 향수 마켓 플레이스 서비스**
>
> **Perflair**는 정교한 데이터 모델링과 안정적인 백엔드 아키텍처를 기반으로 설계된 향수 전문 이커머스 플랫폼입니다. 직관적인 상품 탐색 환경을 제공하고, 효율적인 API 통신 인프라를 구축하여 실시간 마켓 데이터를 관리합니다. 상거래 프로세스의 안정성과 사용자-운영자 간의 원활한 창구 역할을 하는 견고한 웹 애플리케이션을 지향합니다.

---

## 📖 Project Overview (프로젝트 개요)

### 🎯 기획 의도 및 목적
* **향수 특화 커머스 환경 제공:** 일반 쇼핑몰과 달리 향수 고유의 특성(브랜드, 제품 상세 등)을 기반으로 상품을 분류하고 효율적으로 제공할 수 있는 환경을 구축합니다.
* **마켓 플랫폼의 신뢰도 확보:** 공지사항(Notice) 및 Q&A 시스템을 구축하여 마켓 운영의 투명성을 높이고, 고객 문의에 신속하게 대응할 수 있는 비즈니스 환경을 조성했습니다.
* **백오피스 운영 효율화 및 데이터 확장:** 관리자 전용 페이지와 구글 시트 API 연동을 통해 데이터베이스에 직접 접근하지 않고도 입출고 현황이나 문의 내역을 외부 스프레드시트와 실시간 동기화하여 운영 업무의 효율성을 극대화했습니다.
* **안정적인 데이터 흐름 제어:** 프런트엔드와 백엔드 간의 유기적인 API 연동을 통해 대량의 마켓 콘텐츠가 끊김 없이 실시간으로 클라이언트 화면에 렌더링되도록 설계했습니다.

### 🌟 Key User Scenario (주요 서비스 시나리오)
1. **마켓 플레이스 상품 탐색:** 사용자는 메인 페이지 및 상품 목록에서 다양한 향수 라인업을 확인하고, 상세 정보를 직관적으로 조회합니다.
2. **운영 정보 및 공지 확인:** 사용자는 마켓의 공지사항(Notice) 게시판을 통해 플랫폼의 새로운 이벤트나 중요 안내 사항을 실시간으로 확인합니다.
3. **1:1 마켓 문의 (Q&A):** 상품이나 주문에 대한 문의 사항이 있을 경우, Q&A 게시판을 통해 운영자와 소통할 수 있는 피드백 창구를 이용합니다.
4. **실시간 비동기 데이터 인터랙션:** 사용자가 게시글을 작성, 수정, 삭제하거나 상품을 조회할 때 화면의 새로고침 없이 비동기 통신으로 즉각적인 피드백을 받습니다.
5. **독립된 통합 백오피스 (관리자 페이지):** 플랫폼 관리자는 전용 어드민 인터페이스를 통해 등록된 향수 상품의 재고를 관리하고, 공지사항 발행 및 고객의 Q&A 문의를 한눈에 모니터링하고 제어합니다.
6. **실시간 외부 데이터 동기화 (구글 시트 연동):** 마켓의 상품 재고 상태, 주문 현황 또는 사용자 문의 데이터를 외부 구글 스프레드시트와 실시간으로 연동(API Integration)하여, 별도의 데이터베이스 접근 없이도 운영진이 실시간으로 지표를 확인하고 엑셀 기반의 업무 프로세스를 효율적으로 처리할 수 있도록 지원합니다.

---

## 🏗️ Architecture & Directory Structure

본 프로젝트는 서비스의 확장성과 독립적인 유지보수를 확보하기 위해 백엔드(Spring Boot)와 프런트엔드(React)가 유기적으로 결합된 **Full-stack Decoupled Architecture**를 채택하였습니다.

### ⚙️ System Architecture
* **Client Side:** React SPA(Single Page Application) 기반의 프런트엔드 구조로, 사용자용 마켓 화면과 관리자용 백오피스 화면에 끊김 없는 UI/UX를 제공합니다.
* **Server Side:** Spring Boot 기반의 비즈니스 레이어를 구축하여 상품, 게시판, 어드민 기능 및 외부 API(Google API) 요청을 안전하고 정밀하게 처리합니다.
* **Database:** RDBMS(MySQL) 환경에서 JPA 엔티티 간의 유기적인 매핑을 통해 정합성이 보장된 데이터베이스 구조를 구현했습니다.

### 📁 Directory Structure

#### Backend (`/src/main/java/...`)
비즈니스 로직의 응집도를 높이고 계층 간 결합도를 낮추기 위해 표준적인 **계층형 아키텍처(Layered Architecture)**를 적용했습니다.
* `config/`: 시스템 인프라, 구글 API 연동 설정, Swagger 등 전역 설정 관리
* `controller/`: 상품(Product), 공지사항(Notice), Q&A 게시판 및 어드민 데이터 관련 REST API 엔드포인트 구현
* `service/`: 상품 조회 및 게시판 CRUD, 구글 시트 데이터 전송, 페이징 처리를 제어하는 트랜잭션 비즈니스 로직 담당
* `repository/`: Spring Data JPA를 활용한 객체 지향적 데이터베이스 접근 Layer
* `domain/entity/`: Product, Board, Member 등 마켓 핵심 도메인 객체 선언 및 매핑
* `dto/`: 계층 간 안전하고 가벼운 데이터 전송을 위한 Request/Response DTO 객체 최적화

#### Frontend (`/src/main/frontend/...`)
컴포넌트 중심의 유연한 단방향 데이터 흐름을 가지는 React 구조를 생성했습니다.
* `components/`: 상품 카드 UI, 네비게이션 바, 게시판 폼 등 재사용 가능한 UI 블록 관리
* `pages/`: 마켓 메인, 상품 상세, 공지사항 목록/상세, Q&A 작성 화면 및 **관리자 전용 대시보드 페이지** 구성
* `services/api/`: **Axios 기반 API 통신 모듈**을 통합 구축하여 백엔드 서버 및 어드민 데이터 비동기 데이터 동기화 전담

---

## 🛠️ Tech Stack

### **Backend & Database**
* **Language:** Java 17
* **Framework:** Spring Boot 3.5.4
* **Build Tool:** Gradle
* **Data Access:** Spring Data JPA (하이버네이트 기반 ORM)
* **Database:** MySQL
* **External API:** Google Sheets API / Google Drive API (외부 스프레드시트 연동)
* **API Documentation:** Swagger (Springdoc-openapi 기반 API 명세 자동화)

### **Frontend & Communication**
* **Library:** React.js
* **Language:** JavaScript (ES6+)
* **HTTP Client:** **Axios (Spring Boot REST API 비동기 통신 연동)**
* **Styling:** Styled-components / CSS

---

## ✨ Key Features & Technical Accomplishments

* **안정적인 커뮤니티 및 백오피스 지원 비즈니스 로직**
  * 마켓 운영을 뒷받침하는 핵심 기능인 공지사항과 Q&A 게시판의 CRUD를 Spring Data JPA를 통해 안정적으로 구현했습니다.
  * 대량의 데이터 요청 시 부하를 방지하고 클라이언트 화면의 성능을 보장하기 위해 `Pageable` 객체를 활용한 서버 사이드 페이징 처리를 적용했습니다.
  * 독립된 관리자 화면을 구현하여 일반 사용자 페이지와 데이터를 명확히 분리 및 관리하도록 제어했습니다.

* **구글 API 연동을 통한 운영 자동화 파이프라인**
  * 구글 시트 라이브러리를 스프링 부트에 연동하여, 로컬 DB 트랜잭션 발생 시 관련 마켓 지표 및 문의 내용이 외부 스프레드시트에 즉시 동기화되도록 연동 로직을 구축했습니다.

* **Full-stack API 데이터 통신 아키텍처 수립**
  * React(Axios)와 Spring Boot 간의 유기적인 연동을 통해 복잡한 JSON 데이터를 매끄럽게 핸들링했습니다.
  * 비동기 데이터 요청 처리 (`Async/Await`, `useEffect`) 과정에서 발생할 수 있는 네트워크 예외 및 서버 에러 상태를 고려하여 안정적인 UI 렌더링 환경을 구축했습니다.

* **RESTful 원칙에 기반한 엔드포인트 설계 및 가독성 확보**
  * 각 도메인(상품, 게시판, 어드민)의 명사형 자원과 HTTP Method(GET, POST, PUT, DELETE)를 적절히 매핑하여 직관적이고 유지보수가 용이한 API 명세를 설계했습니다.
  * 엔티티 객체의 외부 노출을 차단하고 필요한 데이터만 안전하게 전송하기 위해 DTO 패턴을 전면 도입했습니다.
