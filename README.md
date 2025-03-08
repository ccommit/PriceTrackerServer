# PriceTrackerServer
상품 가격 변동 추적 및 알림 서비스
- PriceTrackerServer는 사용자가 관심 있는 상품의 가격 변동을 추적하고, 변동 내역을 시각적으로 제공하는 서비스입니다. 또한, 사용자가 설정한 조건에 따라 가격이 변동할 때 알림을 받을 수 있습니다.
- 참고 : https://shopping.google.com/?nord=1&pli=1

# 목적
- **객체지향적 설계**를 통해 유지보수가 용이하게 개발, **클린 코드**를 구현하여 가독성을 높임
- 상품의 가격 추적 및 알림 시스템의 신뢰성 높은 구현
- 사용자 맞춤형 가격 알림 및 통계성 데이터 관리

# 사용기술
- JAVA23, Spring Boot 3.2, JPA, MySQL, Elasticsearch, Redis, Docker, Locust, JUnit5, Spring Batch

# 주요 기능
- 상품 데이터 및 가격 추적
  - Google Shopping API를 활용하여 데이터 수집
  - 상품의 가격 변동을 추적 및 저장
  - ko 기준 1차 카테고리: 휴대폰
    - (2차카테고리: 갤럭시, 아이폰, 3차카테고리: 갤럭시21, 아이폰15 ...)
  - 3차 카테고리 상품 별 할인율, 가격 통계(최대 1년까지 제공)
    - 시간별
    - 일별
    - 주별
    - 월별
- 통계 및 시각화
  - 프론트엔드 데모 페이지 제공
  - 상품별 리뷰 점수 데이터 (3차 카테고리별 평균 리뷰점수 제공 ex갤럭시 21 4.0)
  - 2차 카테고리별 트랜드 데이터 제공(pc, 모바일, 전체)
    - 연령대별 클릭 수
    - 성별 클릭 수
- 알림 기능
  - 이메일, SMS등 알림 지원
  - 유저 입장에서 알람을 받을수 있는 기준
    - 유저가 정한 상품의 가격 기준이 범위일 때 알림
    - 유저가 정한 키워드 신규 상품 등록 알림
    - 2차 카테고리별 신규 상품 등록 알림
- 상품 검색
  - 상품명, 카테고리별(1, 2, 3차), 가격 범위등 검색
  - 정렬 옵션 제공(최신순(default), 인기순, 가격 낮은순, 가격 높은순 등)
- 회원관리
  - 회원가입 기능, 회원 수정, 회원탈퇴
  - 아이디 중복 체크
  - 비밀번호 암호화
  - 로그인, 로그아웃
  - 사용자 상태 관리(일반회원, 게스트, 관리자)
  - 이메일 본인 인증
  - 비밀번호 복구 기능 추가
- 관리자 기능
  - 사용자 및 상품 관리
  - 가격 변동 추적에 대한 관리 및 모니터링
  - 시스템 이상 발생 시 알림 기능
  - 로그 및 통계 관리
- 로그인 이력 기록
  - 사용자 로그인 시 LoginHistory 테이블에 로그인 시간 및 로그인 성공 여부가 기록된다.
  - 로그인 실패 시, 실패 이유와 함께 로그인 실패 횟수가 LoginHistory 테이블에 저장된다.
- 세션 관리
  - 세션의 상태는 active, expired, terminated(활성화, 만료, 종료)로 관리된다.
  - 만료된 세션은 일정 시간이 지난 후 삭제된다.
  
# 확장 계획
- 상품 범위 확대: 전자제품뿐만 아니라 의류, 가전, 도서 등 다양한 카테고리 추가
- 해외 시장 확대: 다국어 지원 및 글로벌 쇼핑몰(아마존, 이베이 등)과 연계하여 글로벌 가격 비교 기능 추가

# ERD
![PriceTracker_ERD](https://github.com/user-attachments/assets/70e545a3-711f-4c2b-952a-b2a0c7f4a98a)

<details>
  <summary><h1>Elasticsearch</h1></summary>

  <img src="https://github.com/user-attachments/assets/a0b626e7-15a4-4709-b103-1d5684f2aec3" alt="price_tracking_server_elasticsearch_productId" />
  <img src="https://github.com/user-attachments/assets/866fbee9-2d69-4934-8503-0aabe9fc8a64" alt="price_tracking_server_elasticsearch_trackingId" />
  <img src="https://github.com/user-attachments/assets/8c9d62a3-06a0-4a41-923d-0564ee610f5a" alt="price_tracking_server_elasticsearch_product-price-rollup-daily" />
  <img src="https://github.com/user-attachments/assets/bd2240dd-74e6-4427-96b4-a26ca59ec9fa" alt="price_tracking_server_elasticsearch_product-price-rollup-weekly" />
  <img src="https://github.com/user-attachments/assets/f8000879-899a-4025-8279-147d6917ace1" alt="price_tracking_server_elasticsearch_product-price-rollup-monthly" />
  <img src="https://github.com/user-attachments/assets/6baf88bc-f253-4d32-9740-5cadff2b0ee4" alt="price_tracking_server_elasticsearch_product-price-rollup-yearly" />

</details>

