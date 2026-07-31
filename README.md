## 해당 프로젝트는 상용으로 사용 중인 소프트웨어라 코드를 공개할 수 없습니다.
# 부동산 거래 웹(개발 중)
https://sanggamarket.com/home

상가 부동산 매매를 전문으로 하는 사이트 개발 중

# 개발 인원
* 3명(기획, 백엔드, 프론트엔드)
* 나의 일 : 백엔드, mysql, 서버 인프라 구축

# 사용 기술
* 백엔드 - Kotlin

* 프론트엔드 - React

* DB - Mysql
  
* 도메인 구매 - CloudFlare

* CloudCompute - NCP(Naver Cloud Platform)

* AI - ClaudeCode, Codex

* 스토리지 - CloudFlare R2


# 목적
부동산 중개업에도 여러 분야가 있음.
여러 웹 사이트에서 이미 부동산을 웹으로 나타내고 있지만 그중에 상가를 전문으로 하는 웹 사이트는 없고 홍보를 하기에도 어려움이 있음.
건물주, 임대인, 임차인들 서로 건물을 매매하거나 임대할 사이트를 만드는 게 목표


# Overview
* access token & refresh token으로 로그인 유지
* 이메일 인증방식으로 비밀번호 및 회원가입 구현
* 네이버 지도처럼 현재 화면에 나오는 범위를 검색하는 Bounding Box Query 기법 구현
* 댓글 기능 구현
* 1대1 채팅 구현
  <img width="1779" height="928" alt="스크린샷 2026-07-02 20 41 55" src="https://github.com/user-attachments/assets/b56ebf19-bef3-4d2c-9d0b-dab2cf3f2fc7" />
1. 필터를 통해 원하는 조건의 매물들을 불러올 수 있도록 구현
2. 필터를 통해 검색하면 원하는 매물들이 나옴


<img width="1787" height="945" alt="스크린샷 2026-07-02 20 45 41" src="https://github.com/user-attachments/assets/8edc0d9a-3861-497e-8b2a-16f184f29798" />
지도를 통해 검색하는 방식 구현
휠을 올려 지도가 넓어지면 Bounding Box Query도 범위를 같이 늘려서 위도, 경도를 더 넓게 검색하도록 한다.


<img width="1787" height="939" alt="스크린샷 2026-07-03 10 52 57" src="https://github.com/user-attachments/assets/2569cdc1-667d-4893-afdb-5acc692818a9" />
<img width="1787" height="942" alt="스크린샷 2026-07-03 10 53 56" src="https://github.com/user-attachments/assets/fad93341-5da4-4724-8f8c-5e066e6a36bf" />
<img width="1794" height="941" alt="스크린샷 2026-07-03 10 54 59" src="https://github.com/user-attachments/assets/053780b0-a7f6-49dc-a882-00c7faaca6ea" />
매물을 올리는 과정.
매물을 올리면 DB에서 매물 정보를 저장한다. 임시저장 시에는 프론트앤드에서 주는 JSON을 그대로 저장하고 불러오기 할 때도 그대로 보내준다.
매물에 같이 올릴 이미지, 동영상은 서버가 아닌 CloudFlare R2 저장소에 저장한다. 서버에 요청하면 preURL을 프론트앤드에게 주고 프론트앤드는 해당 URL로 동영상 및 이미지를 저장한다.


# 장비세팅
라이브할 서버를 구하기 위해 aws, azure, GCP를 봤지만 모두 가격이 높음.
어차피 상가, 사무실은 수요와 공급 99%가 국내 한정이기 때문에 글로벌 클라우드 컴퓨팅이 필요 X. NaverCloudPlatform이라는 네이버에서 운영하는 클라우드 컴퓨팅으로 월 57,000원으로 리눅스 장비를 구함.
포트 설정 및 시스템 설정을 해 준 후에 MYSQL 을 깔고 서버를 띄워서 개발 서버로 준비.

# 구현
코틀린 선택 이유 : 추후에 다른 작업자가 이어받아도 쉽게 하기 위해 광범위하게 사용하는 언어인 kotlin으로 구현.
단순 웹사이트이기 때문에 따로 코루틴을 사용할 일은 없음
