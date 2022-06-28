# Artipul project (2022.3.17 ~ 2022.4.4)
write by backend main 개발자 이재후
<h3>&nbsp;목차</h3>
  
  &nbsp;&nbsp;&nbsp;[1. 프로젝트 개요 및 사용 기술스택](#1-프로젝트-개요-및-사용-기술스택)<br>
  &nbsp;&nbsp;&nbsp;[2. Flow chart & ERD](#2-flow-chart--erd)<br>
  &nbsp;&nbsp;&nbsp;[3. Data pipeline](#3-data-pipeline)<br>
  &nbsp;&nbsp;&nbsp;[4. api 개발 및 배포](#4-api-개발-및-배포)<br><br>
  
## 1. 프로젝트 개요 및 사용 기술스택
* Artipul은 미대생들을 위한 온라인 작품 경매 플랫폼입니다. <br><br>
  멀고 험한 예술의 길을 걷고 있는 미대생들에게 작품을 사고 팔 수 있는 플랫폼을 제공함으로써, 학업과 작품활동에 활력을 불어넣어 주는 온라인 공간을 컨셉으로 개발되었습니다.
  미대생(작가)들은 작품 장르와 등록 기간 등을 선택해 작품을 판매할 수 있으며, 구매자들은 작품 장르로 원하는 작품들을 검색해 실시간 경매에 참여하거나, 
  즉시 구매가를 지불하여 작품을 즉시 구매할 수 있습니다. 즉시구매가 이루어지지 않았을 경우, 작가가 설정한 등록 기간이 마감되었을 때 가장 높은 금액으로 입찰한 구매자가 낙찰받게 됩니다. <br><br>
* 사용 기술스택 <br><br>
  <img src="https://img.shields.io/badge/JavaScript-FFF064?style=for-the-badge&logo=JavaScript&logoColor=black">
  <img src="https://img.shields.io/badge/TypeScript-0078FF?style=for-the-badge&logo=TypeScript&logoColor=white">
  <img src="https://img.shields.io/badge/Node.js-7AF67A?style=for-the-badge&logo=Node.js&logoColor=black">
  <img src="https://img.shields.io/badge/NestJS-FF0000?style=for-the-badge&logo=NestJS&logoColor=white">
  <img src="https://img.shields.io/badge/TypefORM-FF8C0A?style=for-the-badge&logo=Typeform&logoColor=black">
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white">
  <img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=Redis&logoColor=white">
  <img src="https://img.shields.io/badge/ElasticSearch-2CE0BC?style=for-the-badge&logo=Elasticsearch&logoColor=white">
  <img src="https://img.shields.io/badge/Logstash-010101?style=for-the-badge&logo=Logstash&logoColor=white">
  <img src="https://img.shields.io/badge/Socket.io-F9FFFF?style=for-the-badge&logo=Socket.io&logoColor=black">
  <img src="https://img.shields.io/badge/GraphQL-E10098?style=for-the-badge&logo=GraphQL&logoColor=white">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white">
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=Git&logoColor=white">
  <img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=GitHub&logoColor=white">
  <img src="https://img.shields.io/badge/GCP-4285F4?style=for-the-badge&logo=Google Cloud&logoColor=white">
  <img src="https://img.shields.io/badge/Express-17202C?style=for-the-badge&logo=Express&logoColor=white">
 
## 2. Flow chart & ERD
* Flow chart <br><br>
![f](https://user-images.githubusercontent.com/81277145/169238415-f01674f0-9d00-4f5e-8b99-f4bd37f398b1.png) <br>
권한분기에 따른 서비스흐름도 입니다. 오픈 api를 사용하는 소셜로그인의 경우, 최초 1회 핸드폰 번호와 닉네임 등 추가 기입 정보를 입력해
회원가입을 거친 뒤 해당 과정을 거친 계정에 한하여 소셜로그인이 이루어지게 됩니다.
<br><br>
* ERD <br><br>
![art ERD (3)](https://user-images.githubusercontent.com/81277145/169240107-dd14c2a6-bc59-4414-9209-e5833520bfb9.png) <br>
회원은 작가와 일반 사용자로 나눠지지만 서로 중복되는 요소가 많기 때문에 작가 테이블과 일반 사용자 테이블로 분리시키지 않고 
미대생 여부 칼럼으로 둘을 구별하는 방식으로 진행하였습니다.
<br><br>
## 3. Data pipeline
![p](https://user-images.githubusercontent.com/81277145/169240966-b43b0cce-3b1d-4658-8968-b6f343c91c86.jpg)
<br><br>

## 4. api 개발 및 배포
 ### &nbsp;&nbsp;<b>USER Create</b> <br>
 * 휴대폰 번호 인증 <br><br>
 ![KakaoTalk_20220522_144838178](https://user-images.githubusercontent.com/81277145/169689266-233d1ef5-dea1-435b-a826-f726e83d2925.png)<br>
 NHN Cloude Service를 이용하였습니다. 입력 받은 핸드폰 번호로 6자리 난수 토큰이 발송되며, redis에 저장된 토큰 값과 비교하여 인증을 진행합니다. 인증을 마친 토큰은 ttl이
 남아있더라도 삭제됩니다. <br><br>
 * 비밀번호 해시 <br><br>
 ![제목 없음](https://user-images.githubusercontent.com/81277145/169691692-90c006a6-9467-4333-9697-2cd33471982d.png) <br>
 유저가 입력한 비밀번호는 bcrypt를 사용하여 해시된 형태로 DB에 저장되고, 검증됩니다. <br><br>

 ### &nbsp;&nbsp;<b>Login</b> <br>
 유저가 입력한 값과 DB에 저장되어 있던 유저의 정보가 일치할 경우, JWT형태의 accessToken과 refreshToken을 발급합니다.<br>보안을 위해 accessToken은 짧은 만료기간을 가지고 로컬 변수에 저장되며, refreshToken은 http Only Secure 쿠키에 저장됩니다.<br>이후 각 토큰에 대한 strategy와 guard를 통해 권한을 분기하고, payload 유저 정보를 사용할 수 있습니다.<br><br>
 ![162326264-91033a2b-c455-42af-9942-1c9127d83cd5](https://user-images.githubusercontent.com/81277145/169690251-046da31b-c05c-4d99-bc63-35fb5e908fdd.png)<br><br>

### &nbsp;&nbsp;<b>Logout</b> <br>
Client의 로그아웃 요청 시 요청 헤더에 포함된 accessToken과 refreshToken을 받아 verify함수를 통해 검증한 뒤, redis에 blacklist로 저장합니다. 이 때 저장되는 TTL값은 토큰의 남은 만료기간으로 설정됩니다.<br><br> 

### &nbsp;&nbsp;<b>경매 API</b> <br>
작품 등록 시 설정한 마감 시간이 지나면 작품에 따라 낙찰 또는 유찰 처리되며, 이는 nestJS의 Task Scheduling 기능을 통해 특정 시간마다 DB를 확인하는 방식으로 구현되었습니다.<br>
RDB와 비관계형 In-memory DB의 특성에 따라, Client의 첫 입찰 요청 시 사용자 별 경매 참여 중인 작품 정보는 MySQL에 저장되며<br> 이후 실시간으로 빠르게 변동되는 작품 별 최고입찰가의 경우 redis에 저장되고 갱신 값이 Client에게 실시간으로 노출됩니다.<br><br> 
![163166653-25db1000-ef26-4940-8c7f-45fe577059dd](https://user-images.githubusercontent.com/81277145/175930625-34a5734d-c7c7-406d-bb0f-6329a2eb82b7.gif)<br><br> 

### &nbsp;&nbsp;<b>서버 배포</b> <br>
* GCP를 이용하였으며, 다음은 개발 시 수동테스트 수행을 위한 서버 배포 형태입니다.
* ㅁ(이미지)
* 구글에서 지원하는 SSL 인증서를 이용하여 보안을 강화하고, 서버 부하 분산을 통한 안정성을 높이기 위해<br>로드밸런서와 인스턴스 그룹을 연결한 뒤 주기적으로 health-checking 하도록 설정하였습니다. 
* 로드밸런서의 static IP는 DNS를 통해 도메인과 연결되어, 클라이언트로부터 받아오는 트래픽을<br>인스턴스 그룹에 부하분산 하도록 설정하였으며 http요청도 https로 리다이렉션됩니다.
