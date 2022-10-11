# 제 19회 임베디드 소프트웨어 경진대회 webOS 부문 최우수상 수상_삼아아팀

![image](https://user-images.githubusercontent.com/29484377/195158289-6f2d7a70-60d3-45a6-87a4-7d48f4177d5d.png)
**🔗  Links**
- [팀 Git 주소](https://github.com/ThreeAmericano)
- [안드로이드 Git 주소](https://github.com/ThreeAmericano/Android)
- [webOS 공식홈페이지 소개 글](https://www.webosose.org/blog/2022/02/08/vehicle-to-smart-home-solution/)

# 📺 시연 영상
- [시연 영상](https://www.youtube.com/watch?v=ZO1fI2EKnug)

## 📜 작품 소개

- LG전자의 webOS를 주제로 차량에서 스마트홈을 제어할 수 있는 솔루션을 개발하였습니다.
- 사용자는 차량과 스마트폰을 통해 언제 어디서든 집안의 상황과 가전제어가 가능합니다.
- TTS를 통한 음성 안내와 구글 어시스턴트를 이용하여 음성 제어 기능을 제공합니다.

## ⛳ 맡은 역할

1. 안드로이드 앱 개발
2. 스마트홈 제어 보드 펌웨어 개발
3. 구글 어시스턴트를 활용한 음성 제어 기능

## 📅개발 기간

- **2021.08.01 ~ 2021.11.20**

## 🛖 전체 구조
![image](https://user-images.githubusercontent.com/29484377/195157607-e63d8330-f6ad-4458-91f5-121eba29bd21.png)

## ✍️ 기술스택

- **Language** : `Kotlin`
- **Architecture** : `MVC`
- **Network** : `RabbitMQ`

## 🤔 고민한점

### 1. 차량 특성상 네트워크가 불안정한데 이를 보완할 수 있을까?

- Topic에 따라 Queue를 구분하고, 해당 Queue를 구독하고 있는 Client들이 메시지를 소비하는 방식인 MQTT 프로토콜 적용
- 네트워크 불안정으로 TCP 연결이 끊기더라도 queue에 메시지가 남아있기때문에 다시 연결 후 Queue의 메시지를 확인하고 동작 수행 가능

### 2. 가전 상태를 UI에 어떻게 즉각적으로 반영할지?

- 가전의 ON/OFF 여부가 토글버튼에 즉각적으로 반영하고자 함.
- 이를 구현하기 위해 서버에 주기적으로 가전 상태를 체크해야 했는데 비효율적이고 속도가 느린 것 같아 다른 방법을 고민
- Firebase의 EventListener를 활용하여, Firebase에 저장된 가전의 상태가 변경된 경우 안드로이드 앱의 콜백 함수에서 토글 버튼 상태를 업데이트 하도록 함.

## 📚 배운점

1. 처음으로 Kotlin을 사용하여 개발하면서 이를 익혀볼 수 있었습니다.
2. Android 기본 컴포넌트들을 공부해볼 수 있었습니다. (`Fragment`, `RecyclerView` 등)
    
# ⭐️ 주요 기능
- **사용자 구분을 위한 로그인 / 회원가입 기능 구현**
    - 로그인 완료시 MQTT와 FireStore에 접근하여 필요한 데이터를 불러옵니다.
    - 이메일형식의 ID를 입력받으며, Firebase의 Authentication을 통해 회원가입이 진행됩니다.

![image](https://user-images.githubusercontent.com/29484377/195160733-1599e202-3726-49c8-93c5-98754cfcfbfe.png)
![image](https://user-images.githubusercontent.com/29484377/195160749-8e89d4d8-e684-4f7d-aacc-8bbc9f01f9f9.png)

- **메인화면**
    - 파이어베이스 리스너를 통해 현재 집의 온습도와 가전의 동작 상태가 UI에 실시간으로 반영되도록 하였습니다.
    - 모드 제어 버튼이나 개별 가전 버튼을 눌러 가전 제어 명령을 내릴 수 있습니다.
    
![image](https://user-images.githubusercontent.com/29484377/195160767-cdbac8ea-6838-4eb5-966e-eb11343ee72e.png)
    
- **제어모드 설정**
    - 실내모드, 외출모드, 슬립모드, 에코모드 4가지 모드를 사용자가 직접 편집할 수 있으며 FireStore에 저장됩니다.
    - 가전의 ON/OFF 및 밝기, 모드 등의 상세한 옵션까지 제어할 수 있도록 구성하였습니다.
    
![image](https://user-images.githubusercontent.com/29484377/195160837-08057ff0-170e-4f5b-941c-2a44ffb741e4.png)
    
- **스케줄 기능**
    - 알림처럼 원하는 시간에 모드나 가전의 동작 수행을 반복적으로 수행할 수 있는 기능입니다.
    - ON / OFF 버튼으로 활성 / 비활성화가 가능하며, 새로운 스케줄 추가가 가능합니다.
    - 스케줄은 한번 반복하는 단발성, 계속 반복되는 반복성 스케줄로 나누어 설정이 가능합니다.
    
![image](https://user-images.githubusercontent.com/29484377/195160871-29b63887-77dd-40c0-8e7f-ab1ee12be221.png)

- **가전 상세 제어**
    - 메인화면에서 제어할 수없는 바람세기, 무드등 밝기, 색상, 모드 제어가 가능합니다.  
  
![image](https://user-images.githubusercontent.com/29484377/195161190-ee430108-5ccf-420b-a28c-63293cf78db8.png)


- **히스토리**
    - 다른 거주자와 본인이 제어한 모드나 가전의 제어 수행 이력을 볼 수 있습니다.
    
![image](https://user-images.githubusercontent.com/29484377/195160892-ee1fb4fa-ce89-452f-9be4-673c515da6cd.png)
    

## 🏆 수상

- 최우수상 (LG전자 사장상) 수상
  
![image](https://user-images.githubusercontent.com/29484377/195161570-fb1bb347-1283-417b-a2a5-1a7d0def9d41.png)
