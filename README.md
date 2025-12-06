# 🏫 Everytime Clone Project (에브리타임 클론 코딩)
> **대학생 필수 커뮤니티 '에브리타임'의 핵심 기능을 구현한 백엔드 중심 프로젝트**
> Spring Legacy와 MyBatis 환경에서 Oracle DB를 활용하여 안정적인 데이터 처리 로직을 구현했습니다.

<br>

## 🛠️ Tech Stack
![Java](https://img.shields.io/badge/Java-007396?style=flat-square&logo=java&logoColor=white)
![Spring](https://img.shields.io/badge/Spring%20Legacy-6DB33F?style=flat-square&logo=Spring&logoColor=white)
![MyBatis](https://img.shields.io/badge/MyBatis-000000?style=flat-square&logo=MyBatis&logoColor=white)
![Oracle](https://img.shields.io/badge/Oracle-F80000?style=flat-square&logo=Oracle&logoColor=white)
<br>

## 📝 Project Overview
- **개발 기간:** 2024.06 ~ 2024.08 (2개월)
- **팀 구성:** Backend 3명
- **기획 의도:**
    - 대학생들이 가장 많이 사용하는 서비스의 데이터 모델링을 직접 분석하고 구현해보고자 함.
    - Legacy 환경에서의 안정적인 MVC 패턴 설계와 MyBatis를 활용한 효율적인 SQL 매핑 학습.

<br>

## 💻 My Contributions (담당 기능)
저는 팀 내에서 **사용자 상호작용(Interaction)**과 **친구 관리 시스템**을 전담했습니다.

### 1. 좋아요(Like) 기능 (비동기 처리)
- **기능:** 게시글 및 댓글 좋아요 토글(Toggle).
- **구현 내용:** 좋아요 버튼 클릭 시 페이지 전체가 새로고침 되지 않도록 **AJAX를 활용해 비동기 통신**으로 구현하여 사용자 경험(UX)을 개선했습니다.

### 2. 친구 추가 및 관리 (Friendship)
- **기능:** 친구 요청, 수락, 차단 및 삭제 관리.
- **구현 내용:** 친구 관계의 상태(대기, 수락, 차단)를 DB 컬럼으로 관리하여 복잡한 사용자 간의 관계를 체계적으로 제어했습니다.

### 3. 강의평 검색
- **기능:** 강의명, 교수명 등을 키워드로 조회.
- **구현 내용:** MyBatis의 동적 쿼리(`if`, `choose` 태그)를 활용하여 다양한 검색 조건에 유연하게 대응하도록 구현했습니다.

### 4. 학점 계산기
- **기능:** 개인 활동 내역 조회 및 학점 계산 기능.
- **구현 내용:** 사용자 ID를 기반으로 여러 테이블에 흩어진 활동 데이터를 효율적으로 조인(Join)하여 조회했습니다.

<br>

## 🚀 Key Features Demo (핵심 기능 시연)
> 사용자의 편의성을 고려하여 비동기 처리 및 상태 관리에 집중한 기능들입니다.

| 좋아요 (비동기 통신) | 친구 추가/관리 |
| :---: | :---: |
| ![좋아요GIF](https://github.com/KwonGreenTea/IotProJect/issues/6#issue-3701348176) | ![친구GIF](https://github.com/KwonGreenTea/IotProJect/issues/5#issue-3701348049) |
| AJAX로 새로고침 없이 즉시 반영 | 친구 상태(대기/수락/차단) 변경 프로세스 |

<br>

## 🎨 UI Implementation
> 백엔드 팀이지만 실제 사용감을 위해 에브리타임의 CSS를 직접 분석하여 적용했습니다.

| 메인(홈) 화면 | 강의평 리스트 | 학점 계산기 |
| :---: | :---: | :---: |
| ![홈화면](https://github.com/KwonGreenTea/IotProJect/issues/2#issue-3701338567) | ![강의평](https://github.com/KwonGreenTea/IotProJect/issues/4#issue-3701338769) | ![학점계산](https://github.com/KwonGreenTea/IotProJect/issues/3#issue-3701338689) |

<br>

## 💾 ERD (Entity Relationship Diagram)
> Oracle DB를 기반으로 관계형 데이터 모델링을 진행했습니다.
![ERD이미지](https://github.com/KwonGreenTea/IotProJect/issues/1#issue-3701331210)

<br>

## 🔥 Troubleshooting (성장 경험)
> 프로젝트 진행 중 마주한 고민과 해결 과정을 기록했습니다.

### 1. 친구 데이터 삭제 방식에 대한 고찰 (Hard vs Soft Delete)
- **Problem:** 친구 삭제 기능을 구현할 때, `DELETE` 문으로 DB에서 데이터를 완전히 지워버리면(Hard Delete) 추후 사용자가 다시 친구 요청을 하거나 차단을 할 때 과거의 상태를 추적하기 어려웠습니다.
- **Solution:** 데이터를 삭제하는 대신 **'상태 코드(Status)' 컬럼을 업데이트하는 방식(Soft Delete)**을 택했습니다. (예: 1=친구, 2=차단, 3=삭제됨)
- **Effect:** 데이터의 이력을 보존할 수 있었고, 잘못된 요청이나 중복 요청을 상태 코드를 통해 효과적으로 제어할 수 있었습니다.

### 2. 좋아요 기능의 UX 개선 (비동기 처리)
- **Problem:** 처음에는 좋아요 버튼을 누를 때마다 `Form` 태그로 전송하여 페이지 전체가 새로고침(Reload) 되었습니다. 이는 스크롤 위치를 놓치게 하여 사용자 경험을 저해했습니다.
- **Solution:** **AJAX(Asynchronous JavaScript and XML)**를 도입하여 서버와 백그라운드에서 통신하도록 변경했습니다.
- **Effect:** 페이지 새로고침 없이 즉각적으로 하트가 채워지고 숫자가 올라가는 부드러운 UI를 구현했습니다.
