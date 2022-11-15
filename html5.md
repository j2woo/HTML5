# HTML5
## 1. Geo Location
### 1) 개요
- 디바이스의 물리적 위치 정보를 파악하기 위한 Javascript API
- 위치 정보

### 2) 위치 정보 사용 가능 여부 확인
- navigator.geolocation의 값 확인

### 3) 위치 정보를 가져와서 한 번만 사용하기
- navigator.geolocation.getCurrentPosition(위치 정보를 가져오는데 성공했을 때 호출되는 함수, 위치 정보를 가져오는데 실패했을 때 호출되는 함수, 옵션)

- 위치 정보를 가져오는데 성공했을 때 호출되는 함수에는 매개변수로 위치 정보와 관련된 객체가 전달됩니다.  
이 객체가 저장하고 있는 정보는 jacascript 뿐 아니라 모바일 API에서도 동일  
coords: latitude(위도), logitude(경도), altitude(고도- GPS가 아니면 없음), accuracy(정확도), altitudeAccuracy(고도의 정확도), heading(방향), speed(속도)  
timestamp: 위치 정보를 가져온 시간

- 위치 정보를 가져오는데 실패했을 때 호출되는 함수에도 매개변수가 넘어가는데 이 경우에는 에러 객체가 전달되고 code 속성을 확인하면 실패한 이유를 알 수 있습니다.

> location.html

### 4) 위치 정보를 계속 가져와서 사용하기
- let 변수 = navaigetor.geolocation.watchPosition(위치 정보를 가져오는데 성공했을 때 호출되는 함수, 위치 정보를 가져오는데 실패했을 때 호출되는 함수, 옵션)로 위치 정보를 계속해서 파악하고 clearWatch(변수)를 호출하면 더 이상 위치 정보를 가져오지 않습니다.

### 5) 옵션
- 객체 형태로 대입
``` javascript
{
    enableHighAccuracy //정확도가 높은 위치 정보를 사용하도록 하는 옵션인데 기본값은 false
    time
}
```

### 6) 웹화면에 현재 위치에 해당하는 카카오 맵을 이용
> kakaomap.html  
> https://apis.map.kakao.com/web/guide/
> Kako Open API: https://developers.kakao.com/  
data.go.kr
- 애플리케이션 생성하고 javascript 키 복사: f2e17aeed3c1967e0b52038107786813  
키는 바로 사용이 불가능- 플랫폼을 등록해야 한다.  
네이티브 앱은 앱의 패키지 이름을 등록해야 휍의 경우는 도메인을 등록해야 합니다.  
연습할 때는 웹으 경우는 http://localhost:포트번호 형태로 등록하고 실제 서비스에 사용을 할 때는 localhost:포트번호 대신에 등록한 도메인이나 실 사용이 가능한 공인 IP 형태로 변경을 해야합니다.

## 2. File API
- File을 읽고 쓰기 위한 API
- input 타입의 file에 multiple 속성이 추가되서 이 속성의 값을 설정하면 여러 개의 파일을 선택하는 것이 가능
- 텍스트 파일을 읽을 때는 인코딩 설정에 주의해야 합니다.
- 일반 파일을 읽을 때는 FileReader 객체를 생성한 후 reader.readAdDataURL(파일 객체)를 호출하고 load 이벤트와 error 이벤트를 처리합니다.  
***load***는 전부 읽었을 때 FileReader 객체의 result에 읽은 내용을 저장하고 ***error*** 이벤트는 읽기에 실패했을 때 실패한 이유를 저장하고 있는 객체를 넘겨줍니다.
<br/><br/>
- 이미지 미리보기
>imagepreview.html

## 3. Drag And Drop API
- 브라우저 내에서 사용할 수도 있고 외부 프로그램과 브라우저 사이에서도 사용할 수 있음  
외부 프로그램과 사용할 때는 외부 프로그램에서 드래그를 하고 브라우저에 드랍을 해야합니다.  
파일을 첨부할 때 많이 

## 4. 브라우저에 데이터를 저장
### 1) 브라우저에 데이터를 저장하는 이유
- 불필요한 트래픽을 줄이기 위해서  
메일 앱의 경우 매번 서버에 접속해서 서버의 데이터를 받아노는 것은 자원의 낭비가 될 수 있습니다.  
맨 처음 접속을 할 때는 데이터를 다운로드 받고(파일의 존재 여부를 확인) 다음 부터는 마지막 업테이트 된 시간을 비교해서 양쪽의 시간이 다르면 데이터가 수정된 것이므로 다운로드를 받고 양쪽의 시간이 같다면 업데이트 된 내용이 없으므로 다운로드를 받지 않도록 구현  
<br/><br/>
- offline 상태에서도 데이터를 사용할 수 있도록 하기 위해서

### 2) 브라우저에 데이터를 저장하는 방법
- Web Storage: Map의 형태로 저장
- Web SQL: 관계형 데이터베이서(SQLites3- 외부에서는 접속이 불가능한 저용량 데이터베이스, 사용법은 MySQL과 유사) 이용
- Indexed DB: 자바스크립트 객체 형태로 저장- NoSQL과 유사  

<br/>
- 기존에는 Cookie를 사용했는데 Cookie 사용하게 되면 문자열만 저장할 수 있고 서버에게 매 번 전송됩니다.  
전송 여부를 클라이언트가 결정할 수 없습니다.

### 3) Web Storage
=> 종류는 2가지
LocalStorage: 브라우저에 저장해서 지우지 않는한 절대 삭제가 되지 않는 저장소  
<br/>
SessionStorage:  현재 접속 중인 브라우저에 해당하는 저장소 접속이 종료되면 소멸

- 데이터 저장과 가져오기 그리고 삭제  
저장  
        스토리지.키 이름= 데이터  
        스토리지.["키이름"]=데이터  
        스토리지.setItem("키이름",데이터);  
가져오기   
        스토리지.키 이름  
        스토리지.["키이름"]
        스토리지.getItem("키이름") 
삭제  
        delete 스토리지.키 이름  
        delete 스토리지.["키이름"]
        스토리지.removeItem("키이름")  

- 저장소에 데이터가 변경되면 window 객체에 storage 이벤트가 발생하고 이벤트 객체에는 key, oldValue, newValue, url, storageArea 같은 속성이 만들어집이다.

- Local Storage는 전역 변수 localStorage로 사용할 수 있고 Session Storage는 sessionStorage로 사용할 수 있습니다.

- 저장된 내용을 확인하는 방법은 브라우저의 검사 창에서 application을 확인하면 됩니다.

- 세션 스토리지 - 브라우저를 종료했을 때 내용이 소멸되는지와 현재 창에서 새창을 출력했을 때 내용이 복제가 되는지 확인
> sessionstorage.html

- 로컬 스토리지 - id 저장을 구현하는데 브라우저를 종료하고 다시 연결했을 때 내용이 존재하는지 여부를 확인
> localstorage.html

- 로컬 스토리지는 보안이 중요하지 않은 많지 않은 양의 데이터를 저장하는데 용이  
장바구니 구현이나 아이디 저장에 유용하게 사용할 수 있습니다.

- 동일한 패턴의 데이터가 많은 경우는 로컬 스토리지 보다는 Web SQL이나 Indexed DB를 권장

## 5. Web Worker
>webworker.html
>worker.js
- javascript를 이용한 백그라운드 처리(스레드)
- Javascript에서는 Thread 표현 대신에 Worker라는 표현을 사용  
- HTML과 함꼐 있는 Javascript 코드에서 긴 작업을 수행하게 되면 작업이 끝날때까지 다른 작업을 수행할 수 없음(UI는 아무것도 할 수 없는 상태)
- Web Worker는 UI 변경을 하지 못하고 DOM 객체 제어를 할 수 없지만 localStorage와 XMLHttpRequest(ajax) 사용은 가능
- Web Worker 생성  
let 변수= new Worker("자바스크립트 파일 경로"); // 워커는 별도의 스크립트 파일에 만들어야 함
- 워커와 브라우저 사이의 메세지 전송 
워커변수.postMessage("메세지") -> 워커에서는 message 이벤트 발생  
워커 파일에서는 postMessage("메세지") => 워커 변수에 message가 발생함
- sendMessage는 바로 처리해달라는 요청이고 postMessage는 다른 작업이 없으면 처리해달라고 하는 요청입니다.
- message 이벤트가 발생하면 매개변수에 data와 error를 가진 객체가 전달됩니다.  
data는 data이고 error는 에러가 발생했을 때 에러에 대한 정보를 가진 객체입니다.
- 워커는 terminate()를 호출해서 중지가 가능


## 6. Application Cache
- 리소스의 일부분을 로컬에 저장하기 위한 기능
- 오픈소스 브라우징이 가능해지고 리소스를 빠르게 로드할 수 있고 서버 부하를 감소시킬 수 있습니다.  
css나 js 그리고 이미지 파일등을 캐싱

## 7. Web Push
- Server Sent Events: 클라이언트의 요청 없이 서버가 클라이언트에게 메세지를 전송하는 것  
사용하는 이유는 알림  
Apple Server가 보내는 Push를 APNS(Apple Push Notification Service)라고 하고 Google Server가 보내는 Push를 FCM(Firebase Cloud Message)라고 합니다.

## 8. WebSocket
- Web에서의 T6
- 일반적인 Web 요청의 처리 방식은 Client가 Server에게 접속을 한 후 하나의 request를 전송하고 그 request를 server가 받으면 처리를 하고 response를 Client에게 전송하고 접속이 끊어집니다.  
연속되는 작업을 처리하기 위해서 Cookie(클라이언트의 브라우저에 저장)와 Session(서버에 저장)이라는 개념을 도입  
일반적인 Web 요청(HTTP나 HTTPS)은 본문 이외에 헤더 정보를 같이 전송해야 합니다.  
작은 사이즈의 데이터를 보내는 경우 오버헤드가 너무 큽니다.  
Web Socket을 이용하면 헤더가 거의 없기 때문에 이러한 오버헤드를 줄일 수 있음
- 작은 양의 메세지를 자주 주고 받는 경우는 ajax나 Fetch API 보다는 Web Socket을 사용하는 것을 권장 

---
# XHTML, CSS, Javascript, HTML%
- 웹 브라우저에 무엇인가를 출력하고 제어하기 위한 기본 기술  

화면 출력: XHTML, HTML5  
출력된 화면에 디자인을 적용: CSS  
출력된 화면의 요소들을 동적으로 제어: JavaScript  
서버에서 데이터를 받아오는 기술: Javascript에서도 ajax와 fetch API  

이 기술 만으로 웹의 모든 화면을 만들 수 있는데 그렇게하면 소스 코드가 길이가 길어지고 비효율적인 코딩을 할 수도 있음  
대부분의 경우는 이러한 작업을 간결한 코드로 어느 정도 효율이 보장된 형태로 할 수 있는 프레임워크나 라이브러리를 많이 이용합니다.

jQuery: 속도가 느리다는 단점이 있지만 크로스 브라우징을 쉽게 구현하고 다양한 플로그인을 제공해서 UI를 쉽게 구현하도록 해줍니다.  
얼마전까지 가장 많이 사용되던 라이브러리 중 하나  

bootstrap: 반응형 웹 구현을 쉽게 해주는 라이브러리, 모바일 웹을 구현할 때 많이 사용함.

react, vue, SPA(Single Page Application):ㄴ 많은 웹 개발자들이 지금은 react나 vue 플로그인으로 다양한 기능을 제공

axios: 서버에서 데이터를 받오는 것을 쉽게 구현할 수 있도록 해주는 라이브러리

> 버튼으로 css, js 불러오기 

