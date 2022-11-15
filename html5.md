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
