# IP (인터넷 프로토콜)

## 역할
* 지정한 IP 주소에 데이터 전달합니다. (패킷에 IP 정보를 담음)
* 패킷 이라는 통신 단위로 데이터 전달합니다.

## 한계
* 비연결성
  * 패킷을 받을 대상이 없거나 대상이 서비스 불능 상태여도 패킷 전송합니다.
* 비신뢰성
  * 중간에 패킷이 사라질 경우 해결방법이 없습니다.
  * 패킷의 순서가 변경될 수 있습니다.
* 프로그램 구분
  * 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 다수의 경우 구분이 안됩니다.

---

# TCP, UDP
TCP - 전송 제어 프로토콜(Transmission Control Protocol)
UDP - 사용자 데이터그램 프로토콜(User Datagram Protocol)

## 인터넷 프로토콜 스택의 4계층
* 애플리케이션 계층 - HTTP, FTP
* 전송 계층 - TCP, UDP
* 인터넷 계층 - IP
* 네트워크 인터페이스 계층

## TCP 특징
* 연결 지향 - TCP 3 way handshake (가상 연결)
  1. SYN (클라이언트)
  2. SYN/ACK (서버)
  3. ACK (클라이언트)
* 데이터 전달 보증
  - 서버는 클라이언트에게 요청에 대한 응답을 보내줌
* 순서 보장
* 신뢰할 수 있는 프로토콜
* 현재는 대부분 TCP 사용

## UDP 특징
* 기능이 거의 없음
* 연결지향 - TCP 3 way handshake X
* 데이터 전달 보증 X
* 순서 보장 X
* 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
* 정리
  * IP와 거의 같다. (port와 체크섬 정도만 추가됨)
  * 애플리케이션에서 추가적인 작업(기능) 필요
* http3에서 UDP 프로토콜을 사용

---

# PORT
여러 패킷이 각자 어떤 애플리케이션(프로세스)에서 사용하는지 알려주는 정보.
하나의 포트는 하나의 애플리케이션(프로세스)에만 할당.

* 0 ~ 65535 - 할당 가능
* 0 ~ 1023 - 잘 알려진 포트, 사용하지 않는것이 좋음
  * FTP - 20, 21
  * TELNET - 23
  * HTTP - 80
  * HTTPS - 443
  
--- 
  
# DNS
도메인 네임 시스템(Domain Name System)

## 기능
* 도메인 명을 IP 주소로 변환
* IP를 기억하기 어려운 문제를 해결
* IP가 바뀌어도 관리가 쉬움

---

# URI(Uniform Resource Identifier)
URI는 URL, URN을 포괄하는 개념.

* Uniform - 리소스를 식별하는 통일된 방식
* Resource - 자원, URI로 식별할 수 있는 모든 것(제한 없음)
* Identifier - 다른 항목과 구분하는데 필요한 정보

## URL(Uniform Resource Locator)
[scheme](#scheme)://[[userInfo@]host](#host)[[:port]](#port)[[/path]](#path)[[?query]](#query)[[#fragment]](#fragment)
(foo://example.com:8042/over/there?name=ferret#nose)

* Locator - 리소스가 있는 위치를 지정

### scheme
* 주로 프로토콜 사용
  * 프로토콜 - 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙 (http, https, ftp 등)
  
### host
* 호스트명
* 도메인명 또는 IP 주소를 직접 사용 가능

### port
* 접속 포트
* 일반적으로 생략(http: 80, https: 443)

### path
* 리소스 경로, 계층적 구조
* 예시
  * /home/file1.jpg
  * /members
  * /members/1000
  
### query
* key=value 형태
* ?로 시작, &로 추가
* query parameter, query string 등으로 불림.

### fragment
* html 내부 북마크 등에 사용
* 서버에 전송하는 정보 아님

### 문법
예시: https://www.google.com:443/search?q=hello&hl=ko
* 프로토콜 (https)
* 호스트명 (www.google.com)
* 포트 (443)
* 패스 (/search)
* 쿼리 파라미터(q=hello&hl=ko)

## URN(Uniform Resource Name)
(urn:example:animal:ferret:nose)

* Name - 리소스에 이름을 부여

---

# HTTP

HyperText Transfer Protocol
HTML, TEXT, 파일, JSON, XML 등 거의 모든 형태의 데이터 전송 가능

## 요청 흐름
1. 웹 브라우저가 HTTP 메시지 생성
2. socket 라이브러리를 통해 전달
    - A: TCP/IP 연결(IP, PORT)
    - B: 데이터 전달
3. TCP/IP 패킷 생성, HTTP 메시지 포함

## 특징
* [클라이언트 서버 구조](#클라이언트-서버-구조)
* [무상태 프로토콜](#무상태-프로토콜), [비연결성](#비연결성)
* [HTTP 메시지](#http-메시지)
* [단순함, 확장 가능](#)

## 클라이언트 서버 구조
* Request Response 구조
* 클라이언트는 서버에 요청을 보내고 응답을 대기
* 서버가 요청에 대한 결과를 만들어서 응답

## 무상태 프로토콜
* 스테이트리스(Stateless)
  * 서버가 클라이언트의 상태를 보존하지 않음
  * 장점: 서버 확장성 높음(스케일 아웃)
  * 단점: 클라이언트가 추가 데이터 전송
  
## 비연결성
- HTTP는 기본이 연결을 유지하지 않는 모델
- 일반적으로 초단위 이하의 빠른 속도로 응답
  - 실제 서버에서 동시에 처리하는 요청은 수십개 이하
- 서버 자원을 매우 효율적으로 사용할 수 있음

### 한계
- TCP/IP 연결을 새로 맺어야 함 (3 way handshake 시간 추가)
- 사이트를 요청하면 HTML, JS, CSS, 추가 파일 등등 많은 자원이 함께 다운로드 되는데 그때마다 새로 연결 해야함
- 지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결

## HTTP 메시지

### 구조
- [start-line](#start-line)
- [header](#header)
- empty line(CRLFF)
- [message body](#message-body)

### Start Line
start-line = request-line/status-line
- request-line
  - method SP(공백) request-target SP HTTP-version CRLF (엔터)
- status-line
  - HTTP-version SP status-code SP reason-phrase CRLF
  
### Header
- HTTP 전송에 필요한 모든 부가정보
  - 예) 메시지 바디의 내용/크기, 요청 클라이언트 정보 등
- 필요시 임의의 헤더 추가

### Message Body
- 실제 전송할 데이터
- HTML, 이미지, 영상, JSON 등 byte로 표현할 수 있는 모든 데이터 전송 가능

## 메서드

### 종류
- [GET](#get): 리소스 조회
- [POST](#post): 요청 데이터 처리, 주로 등록에 사용
- [PUT](#put): 리소스를 대체, 해당 리소스가 없으면 생성
- [PATCH](#patch): 리소스 부분 변경
- [DELETE](#delete): 리소스 삭제
- 기타
  - HEAD: GET 이랑 동일하지만 메시지 부분을 제외하고 상태줄과 헤더만 반환
  - OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)
  - CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정
  - TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

### GET
- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query를 통해 전달
- 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

### POST
- 요청 데이터 처리
  - HTMl-form 에 입력된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공
  - 메시지 게시 (예 : 게시판 글쓰기, 댓글 달기)
  - 서버가 아직 식별하지 않은 새 리소스 생성 (예: 신규 주문 생성)
  - 기존 자원에 데이터 추가 (예: 한 문서 끝에 내용 추가하기)
  - 다른 메서드로 처리하기 애매한 경우
- 메시지 바디를 통해 서버로 요청 데이터 전달
- 서버는 요청 데이터를 처리
  - 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용

### PUT
- 리소스를 완전히 대체
  - 리소스가 있으면 대체/없으면 생성
- **클라이언트가 리소스를 식별**
  - 클라이언트가 리소스 위치를 알고 URI 지정(POST와 차이점)
  
### PATCH
- 리소스를 부분 변경

### DELETE
- 리소스 제거

## API 설계 개념

### 문서 (document)
- 단일 개념 (파일 하나, 객체 인스턴스, 데이터베이서 row)
- 예) /members/100, files/start.jpg

### 컬렉션 (collection)
- 서버가 관리하는 리소스 디렉터리
- 서버가 리소스의 URI를 생성하고 관리
- 예) /members

### 스토어 (store)
- 클라이언트가 관리하는 자원 저장소
- 클라이언트가 리소스의 URI를 알고 관리
- 예) /files

### 컨트롤러 (controller), 컨트롤 URI
- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
- 동사를 직접 사용
- 예) /members/{id}/delete

## 상태 코드

### 1XX
- 요청이 수신되어 처리중
- 거의 사용하지 않음

### 2XX
- Successful
- 클라이언트의 요청을 성공적으로 처리
- 대표 코드
  - 200: OK
  - 201: Created (새로운 리소스 생성)
  - 202: Accepted
  - 204: No Countent

### 3XX
- Redirection
  - 영구 리다이렉션: 특정 리소스의 URI가 영구적으로 이동(301, 308)
  - 일시 리다이렉션: 일시적 변경(302, 307, 303)
    - 예: 주문 완료 후 주문 내역 화면으로 이동
    - PRG: Post/Redirect/Get
  - 특수 리다이렉션: 결과 대신 캐시를 사용(300, 304)
- 요청을 완료하기 위해 유저 에이전트의 추가 조치 필요
- 대표 코드
  - 300: Multiple Choices
  - 301: Moved Permanently
  - 302: Found(GET으로 변경하여 리다이렉트할 수 있음)
  - 303: See Other(GET으로 변경하여 리다이렉트)
  - 304: Not Modified(수정사항이 없으니 캐시를 이용하라 코드)
  - 307: Temporary Redirect(Method를 변경하면 안됨)
  - 308: Permanent Redirect
  
### 4XX
- Client Error
- 클라이언트의 요청에 잘못된 문법등으로 서버가 요청을 수행할 수 없음
- 오류의 원인이 클라이언트에 있음
- **클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실패함**
- 대표 코드
  - 400: Bad Request(요청 파라미터가 잘못되거나 API 스펙이 맞지 않음)
  - 401: Unauthorized(클라이언트가 해당 리소스에 대한 인증이 필요함)
  - 403: Forbidden(서버가 승인을 거부함)
  - 404: Not Found(요청 리소스를 찾을 수 없음)
  
### 5XX
- Server Error
- 서버 문제로 오류 발생
- 대표 코드
  - 500: Internal Server Error(서버 문제로 오류 발생)
  - 503: Service Unavailable(서비스 이용 불가)
  
## Header

### 표현(Representation)
- Content-Type: 표현 데이터의 형식
  - 미디어 타입, 문자 인코딩
  - 예)
    - text/html; charet=utf-8
    - application/json
    - image/png
- Content-Encoding: 표현 데이터의 압축 방식
  - 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
  - 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
- Content-Language: 표현 데이터의 자연 언어
  - 예)
    - ko
    - en
    - en-US
- Content-Length: 표현 데이터의 길이
  - 바이트 단위
  - Transfer-Encoding을 사용하면 Content-Length를 사용하면 안됨

### 협상(콘텐츠 네고시에이션)
클라이언트가 선호하는 표현 요청
- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어
- 협상 헤더는 요청시에만 사용

#### 협상과 우선순위
Quality Vaules(q)

1. 0~1, 클수록 우선순위
   - 생략하면 1
   - Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
     1. ko-KR;q=1(생략)
     2. ko;q=0.9
     3. en-US;q=0.8
     4. en;q=0.7
 2. 구체적인것이 우선
    - Accept: text/* text/plain, text/plain;format=flowed, \*/\*
      1. text/plain;format=flowed
      2. text/plain
      3. text/*
      4. \*/\*
 3. 구체적인것을 미디어타입을 맞춘다
    - Accept: text/\*;q=0.3, text/html;q=0.7, text/html;level=1, text/html;level=2;q=0.4, \*/\*;q=0.5
    
### 전송 방식
- 단순 전송
- 압축 전송
- 분할 전송
- 범위 전송
  
  
---

# 배운점
처음 보는 코드들이 많았고, 세션 적용할때 코드를 잘못 적용했음.

# 추가로 공부해야할 내용
- 이더넷 프레임
- 서버 확장성 높음(스케일 아웃)
 
