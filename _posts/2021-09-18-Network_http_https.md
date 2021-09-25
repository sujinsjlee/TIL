---
title: "Network - HTTP HTTPS"
categories:
  - Network
tags:
  - Network
---

[생활코딩 - HTTPS와 SSL 인증서](https://opentutorials.org/course/228/4894)

# HTTP
> HyperText Transfer Protocol  
HTTP는 Hypertext Transfer Protocol의 약자다. 즉 Hypertext 인 HTML을 전송하기 위한 통신규약을 의미한다. HTTPS에서 마지막의 S는 Over Secure Socket Layer의 약자로 Secure라는 말을 통해서 알 수 있듯이 보안이 강화된 HTTP라는 것을 짐작할 수 있다. HTTP는 암호화되지 않은 방법으로 데이터를 전송하기 때문에 서버와 클라이언트가 주고 받는 메시지를 감청하는 것이 매우 쉽다. 예를들어 로그인을 위해서 서버로 비밀번호를 전송하거나, 또는 중요한 기밀 문서를 열람하는 과정에서 악의적인 감청이나 데이터의 변조등이 일어날 수 있다는 것이다. 이를 보안한 것이 HTTPS다.


# HTTPS
HTTP**S**와 SSL를 같은 의미로 이해하고 있는 경우가 많다. 이것은 맞기도 틀리기도 하다. 그것은 마치 인터넷과 웹을 같은 의미로 이해하는 것과 같다. 결론적으로 말하면 웹이 인터넷 위에서 돌아가는 서비스 중의 하나인 것처럼 HTTPS도 SSL 프로토콜 위에서 돌아가는 프로토콜이다.


# POST 방식
[GET 방식 vs POST방식](https://opentutorials.org/module/6/5125)

- HTML 문서에서 method 필드를 "POST"나 "GET"을 입력해야함
- POST 방식으로 데이터를 전송하는 것은 무엇이지..?
  - POST방식은 GET 방식보다 보안성이 뛰어난 방법
  - GET 방식으로하면 url내부에 모든 정보가 포함됨 (ID/PWD)
    - GET방식의 특징으로는 URL에 Parameter를 붙여서 전송
  - POST방식은 일부 정보들을 제외하고 url이 구성됨
    - url에 모든정보를 노출하지 않음
  - get 방식으로 데이터를 전송할 때 URL에 데이터를 포함시키는 것이 비해서 POST 방식으로 데이터를 전송할 때는 전송하는 데이터를 URL에 포함시키지 않고 전송 할 수 있다. 이러한 차이로 인해서 GET 방식은 정보에 대한 링크로 많이 사용되고, POST 방식은 사용자의 아이디나 비밀번호와 같은 데이터를 전송하는 방식으로 주로 사용한다.


```html
<html>
<body>
    <form method="POST" action="4.php">
        id :  <input type="text" name="id" />
        password :  <input type="text" name="password" />
        <input type="submit" />
    </form>
</body>
</html>
```


```php
<?php
echo $_POST['id'].','.$_POST['password'];
?> 
```
