# Architecture

오르락(UpTheRock)은 **위치 기반 등산 서비스**에 적합하도록 클라이언트와 서버의 역할을 명확히 분리한 아키텍처로 설계되었습니다.

지도 시각화와 사용자 경험(UI/UX)은 클라이언트에 집중하고, 데이터 관리와 비즈니스 로직은 서버에서 일관되게 처리합니다.

<img width="5044" height="2524" alt="system-architecture" src="https://github.com/user-attachments/assets/446c3a25-72d8-4967-be97-c4c59f2022a2" />

---

## 시스템 구성 개요

오르락의 시스템은 다음과 같은 구성 요소로 이루어져 있습니다.

- **Native (iOS / Android)**  
- **Client (React Native + Unity + Mapbox)**  
- **API Gateway (NGINX)**  
- **Backend Server (Spring Boot)**  
- **Database (MySQL)**  

각 구성 요소는 독립적인 책임을 가지며, 확장성과 유지보수를 고려한 구조를 목표로 설계되었습니다.

---

## Native 영역 (Android)

- 각 플랫폼의 **네이티브 위치 서비스(GPS)**를 사용합니다.
- 위치 정보는 OS 레벨에서 수집되며,
  React Native 클라이언트와 네이티브 브릿지를 통해 전달됩니다.

---

## Client 영역

클라이언트는 **사용자 경험과 시각화**에 집중합니다.

### React Native
- 애플리케이션 전반의 UI와 사용자 흐름을 담당합니다.
- 주요 역할
  - 화면 전환 및 사용자 인터랙션 처리
  - 서버 API 호출
  - 운동 정보 및 커뮤니티 데이터 표시

### Unity
- 등산 경험을 시각적으로 표현하기 위한 **3D 지도 요소**를 담당합니다.
- 캐릭터 및 시각적 연출 요소를 독립적으로 확장할 수 있도록 구성했습니다.

### Mapbox
- 지도 렌더링 및 경로 시각화를 담당합니다.
- 실제 등산 경로와 이동 기록을 지도 위에 표현합니다.

---

## API Gateway (NGINX)

- 클라이언트와 서버 사이의 **단일 진입점** 역할을 합니다.
- 주요 역할
  - API 요청 라우팅
  - 서버 접근 제어
  - 향후 트래픽 증가에 대비한 확장 포인트 제공

---

## Backend Server (Spring Boot)

Spring Boot 서버는 **서비스의 핵심 비즈니스 로직**을 담당합니다.

### 주요 기능
- 사용자 관리
- 운동 기록 저장
- 피드 생성 및 조회
- 댓글 및 좋아요 기능

모든 핵심 규칙과 데이터 처리는 서버에서 수행하여,  
클라이언트 의존도를 최소화하고  
로직 변경 시 앱 업데이트 부담을 줄이는 구조를 선택했습니다.

---

## Database (MySQL)

- 서비스의 핵심 데이터를 저장합니다.
  - 사용자 정보
  - 운동 기록
  - 코스 데이터
  - 커뮤니티 데이터

MVP 단계에서는 운영 안정성과 관리 효율을 고려하여 **MySQL**을 사용했습니다.

---

## 설계 방향 요약

- 클라이언트는 가볍게, 서버는 명확하게
- 위치 기반 서비스에 적합한 역할 분리
- 지도·시각화는 전문 도구 활용
- 향후 기능 확장을 고려한 구조

이 아키텍처는  
단순한 등산 기록 앱이 아닌,  
**등산 경험을 디지털 콘텐츠로 확장하기 위한 기반 구조**를 목표로 설계되었습니다.

---

## ⚙️ 기술 스택

오르락은 MVP 단계에서 **안정성과 구현 효율**을 우선하여  
검증된 기술 스택을 중심으로 구성했습니다.

<table>
  <thead>
    <tr>
      <th>분류</th>
      <th>기술 스택</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>프론트엔드</td>
      <td>
        <img src="https://img.shields.io/badge/React_Native-%2320232a.svg?logo=react&logoColor=%2361DAFB"/>
        <img src="https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=000"/>
        <img src="https://img.shields.io/badge/styled--components-DB7093?logo=styledcomponents&logoColor=fff"/>
      </td>
    </tr>
    <tr>
      <td>백엔드</td>
      <td>
        <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat&logo=spring-boot&logoColor=white"/>
        <img src="https://img.shields.io/badge/Java-007396?style=flat&logo=openjdk&logoColor=white"/>
        <img src="https://img.shields.io/badge/Gradle-02303A?style=flat&logo=gradle&logoColor=white"/>
      </td>
    </tr>
    <tr>
      <td>데이터베이스</td>
      <td>
        <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white"/>
        <img src="https://img.shields.io/badge/Redis-%23DD0031.svg?logo=redis&logoColor=white"/>
      </td>
    </tr>
    <tr>
      <td>인프라</td>
      <td>
        <img src="https://custom-icon-badges.demolab.com/badge/AWS-%23FF9900.svg?logo=aws&logoColor=white"/>
        <img src="https://img.shields.io/badge/NGINX-009639?logo=nginx&logoColor=white"/>
      </td>
    </tr>
  </tbody>
</table>
