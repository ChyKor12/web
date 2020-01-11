---
typora-root-url: old-15\img
---

# [WriteUp]Webhacking.kr - old-15

:black_nib:ChyKor12(sjjo0225@gmail.com)

---

![Access_Denied](/Access_Denied.png)

챌린지에 들어가면 위와 같이 Access_Denied라는 창이 뜨면서 바로 홈 화면으로 돌아간다. 도메인 앞에 `view-source:`를 붙여서 해당 페이지의 소스 코드를 보자.

```html
<!-- view-source:https://webhacking.kr/challenge/js-2/ -->
<html>
<head>
<title>Challenge 15</title>
</head>
<body>
<script>
  alert("Access_Denied");
  location.href='/';
  document.write("<a href=?getFlag>[Get Flag]</a>");
</script>
</body>
```

href는 hypertext reference의 약자로, 연결할 주소를 지정하는 속성이다. `location.href;`라고 쓰면 현재 페이지를 확인할 수 있고, `location.href="페이지 주소"`라고 쓰면 그 페이지로 이동하게 된다. 따라서 `location.href='/'`는 `'/'`라는 페이지로 이동하겠다는 뜻이다. 홈 화면이 해당 디렉토리에 해당하는 것 같다. 그리고 `<a>` 태그는 하이퍼링크를 걸어 주는 태그인데, `<a href="페이지 주소">Hyperlink</a>`라고 하면 그 하이퍼링크를 페이지 주소와 연결시켜 준다. 그러면 문제의 도메인에 `?getFlag`를 붙이면 플래그를 얻을 수 있을 것 같다.

```
https://webhacking.kr/challenge/js-2/?getFlag
```

---

- 크롬 설정으로 자바스크립트를 우회하는 방법도 있다. 설정 - 고급 - 개인정보 및 보안 - 사이트 설정 - 자바스크립트에서 문제의 사이트를 차단 목록에 추가하면 홈 화면으로 돌아가는 자바스크립트가 실행되지 않아서 해당 사이트에서 관리자 도구로 소스 코드를 볼 수 있다.