---
title: "System Design - Authentification (Cookie, Session, Token)"
categories:
  - System Design
tags:
  - System Design
---



## Cookie

- Cookie
    - 서버는 쿠키를 이용해서 브라우저에 사용자에대한 데이터를 넣을 수 있음 
- Cookie 동작
    - 사이트에 방문하면 브라우저는 서버에 Request 를 보냄
    - Server 는 Browser 에 요청에 응답할텐데
    - 해당 Response에는 모든 데이터와 사용자가 찾던 페이지 정보가 있음
    - 또한 그곳에는 브라우저에 저장하고자하는 쿠키가 있을 수 있음
    - From now on, 사용자가 브라우저에 쿠키를 저장한 후 해당 브라우저에 방문할 때마다 브라우저는 해당 쿠키도 요청과 함께 보내게 됨
- Cookie 특징
    - Domain specific : 유투브가 준 쿠키는 유투브에만 보내지게됨
    - Expiration Data : 쿠키는 서버가 정한 기간에따라 유효
    - 쿠키는 인증정보뿐만이 아니라 여러가지 정보를 저장할 수 있음 (ex, 웹사이트 언어설정)
    - Automatically sent

## Stateless
- **Stateless** : 서버로 가는 모든 요청이 이전 request 와 독립적으로 다뤄짐
- Request 끼리 연결이 없음
- 메모리가 없음
- Reqeust가 끝나면 서버는 사용자에대해서 잊어버림



## Session
- HTTP 는 Stateless Request / Response 동작을 하기 때문에 요청할때마다 우리가 누군지 알려줘야함
- 이를 하는 방법 중 하나가 **Session**

- Session 동작
    - User name + Password를 서버에 보냈는데 비밀번호가 맞다면 서버는 Session DB에 해당 User record를 생성
    - 해당 세션은 Unique ID를 가지고 있음 해당 세션 ID는 쿠키를 통해 브라우저로 돌아오고 저장됨
    - 따라서 같은 웹사이트의 다른 페이지로 이동하면 브라우저는 세션 ID를 갖고있는 쿠키를 서버에게 보낼 것임
    - 서버는 요청에 담긴 쿠키에 달린 세션 ID를 확인하고 세션 DB에서 해당 ID를 확인해봄
    - 거기서 해당 ID는 특정 User것이라는 것을 알게되고 그 때 서버는 사용자를 알게됨
    - 즉, 중요한 모든 정보는 Server 쪽에 있는 것
    - User는 Session ID만 갖고있는 것
    - Cookie 는 Session ID를 전달하기 위한 매개체
    - Cookie 는 브라우저용
    - 네이티브용 앱에서는 Cookie 대신 Token을 사용

- Session 특징
    - 현재 로그인한 유저들의 모든 세션ID를 DB에 저장해야함
    - 유저가 늘어날수록 DB도 커져야함 --> **Redis** (해당 목적을 수행하기 위한 빠르고 저렴한 DB)

## Token
- String type
- 서버에 Token을 보냄
- 서버는 세션 DB에서 해당 토큰과 일치하는 유저를 찾게됨

## JWT
> DB없이 유저 인증


- Token 형식
- JWT로 유저인증을 처리하면 세션 DB를 갖출 필요가 없음
- DB에 저장하지 않는 대신 정보에 사인하고 USer에게 다시 전달 

- 이후 User가 Server에 Reqeust를 할때 해당 '사인된 정보Signed Info'혹은 '토큰'을 서버에 요청과 같이 보냄
- 페이지 요청시에 서버는 해당 토큰이 유효한지만 검증

- DB 관리 안함
- 암호화불가능 (보안성이 높은 자료는 JWT 로관리하면 안됨)


<!--

## Cookies

- Cookies
     - The server can use cookies to manage data about the user in the browser.
- Cookie behavior
     - When you visit a browser, your browser sends a **Request** to the server.
     - The server will respond to the browser.
     - The response contains all data and page information the user was looking for
     - There may also be cookies that you wish to store in your browser
     - From now on, the user saves a cookie in the browser and whenever the user visits the browser, the browser also sends the cookie along with the request.
- Cookie Features
     - Domain specific: Cookies given by YouTube are sent only to YouTube
     - Expiration Data: Cookies are valid according to the period set by the server
     - Cookies can store various information as well as authentication information (ex, website language setting)
     - Automatically sent

## Stateless
- **Stateless** : All requests to the server are handled independently of previous requests.
- No connection between requests
- No memory
- When the process of the request is finished, the server forgets about the user.

## Session
- HTTP has a stateless request / response operation, so we have to tell who we are every time we make a request.
- One way to handle this is **Session**

- Session operation
    - If the user name + password is sent to the server and the password is correct, the server creates the corresponding user record in the session DB.
    - The session has a unique ID. The session ID is saved and returned to the browser via a cookie.
    - So, when you navigate to another page on the same website, the browser will send a cookie with the session ID to the server.
    - The server checks the session ID attached to the cookie in the request and checks the ID in the session DB
    - From there, it knows that the ID is for a specific User, and then the server knows the user.
    - That is, all important information is on the server side.
    - User has only Session ID
    - Cookie is a medium for passing Session ID
    - Cookie is for browser
    - In native apps, use tokens instead of cookies

- Session Features
    - All session IDs of currently logged in users should be stored in the DB
    - As the number of users increases, the DB should also grow -> **Redis** (a fast and cheap DB to fulfill the purpose)
    
## Token
- String type
- Send Token to server
- The server finds the user matching the corresponding token in the session DB.

## JWT
> User authentication without DB


- Token format
- If user authentication is processed with JWT, there is no need to have a session DB
- Sign the information instead of storing it in the DB and pass it back to the USer

- Afterwards, when the user makes a request to the server, the corresponding 'Signed Info' or 'token' is sent to the server as a request.
- When requesting a page, the server verifies that the token is valid

- No DB management
- Impossible to encrypt (Data with high security should not be managed with JWT)

-->