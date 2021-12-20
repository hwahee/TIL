# 와이어샤크 이용기

## 사용 계기
- [HTTP.md](../4.%20Web%20misc/HTTP.md) 작성 중 실제로 평문으로 보내면 감청이 될까 궁금해서 


## 목적
'HTTP://'로 시작하는 서버에 접속하여 wireshark로부터 패킷을 평문으로 읽히기


## 방법
- 라즈베리파이에 express 서버 세팅
- 서버는 http(평문)를 사용하여 "Hello world from raspberry" 문자열 send
- 노트북으로 192.168.ser.ver:8080 접속
- 와이어샤크에서 위 문자열이 포착됐는지 확인


## 장치 구성
- LAN으로 연결되는 공유기
- 공유기에 와이파이로 연결된 라즈베리파이 4 - 라즈베리파이 OS
- 공유기에 와이파이로 연결된 노트북 - windows10


## wireshark 설치 
ref. from [unboxing tomorrow](https://unboxing-tomorrow.com/project-installing-wireshark-on-raspberry-pi/)



