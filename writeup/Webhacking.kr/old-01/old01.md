# [WriteUp]Webhacking.kr - old01

:black_nib:ChyKor12(sjjo0225@gmail.com)

---

```php+HTML
<?php
  include "../../config.php";
  if($_GET['view-source'] == 1){ view_source(); }
  if(!$_COOKIE['user_lv']){
    SetCookie("user_lv","1",time()+86400*30,"/challenge/web-01/");
    echo("<meta http-equiv=refresh content=0>");
  }
?>
<html>
<head>
<title>Challenge 1</title>
</head>
<body bgcolor=black>
<center>
<br><br><br><br><br>
<font color=white>
---------------------<br>
<?php
  if(!is_numeric($_COOKIE['user_lv'])) $_COOKIE['user_lv']=1;
  if($_COOKIE['user_lv']>=6) $_COOKIE['user_lv']=1;
  if($_COOKIE['user_lv']>5) solve(1);
  echo "<br>level : {$_COOKIE['user_lv']}";
?>
<br>
<a href=./?view-source=1>view-source</a>
</body>
</html>
```

먼저 `SetCookie()`로 쿠키를 생성한다.

> 쿠키 생성 함수는 `setcookie(name, value, expire, path, domain, secure, httponly)`의 형태를 가진다. name을 제외한 매개변수들은 옵션이다.

`SetCookie("user_lv","1",time()+86400*30,"/challenge/web-01/");`는, user_lv라는 이름의 쿠키를 생성하는데 1이란 값을 가지고 현재 시간으로부터 30일 뒤(86400sec = 1day)에 만료되며, `"/challenge/web-01/"`이라는 경로에 존재하게 된다. 생성된 쿠키에 접근할 때는 `$_COOKIE["name"]`으로 접근할 수 있다. 아래쪽의 php문을 보면, user_lv라는 이름을 가진 쿠키가 6 이상이면 1로 바꾸고, 5 초과이면 `solve(1);`를 실행한다. 즉 쿠키의 값이 5 초과 6 미만이면 문제가 풀릴 것이다. 다시 문제 페이지(`https://webhacking.kr/challenge/web-01/`)로 돌아가서, 크롬의 관리자 도구(F12) - Application - Cookies - https://webhacking.kr에서 user_lv의 값을 5.5로 바꿔 보자.

![change cookie](https://user-images.githubusercontent.com/57470479/72200420-aa924580-348c-11ea-8cf7-fd6e1e828ef3.png)

새로고침.

![clear](https://user-images.githubusercontent.com/57470479/72200419-aa924580-348c-11ea-8a56-a2680e5d21ed.png)

level : 5.5가 뜨면서 문제가 풀린다.
