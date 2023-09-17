# Strict-Transport-Security 헤더

- Strict-Transport-Security 헤더는 해당 사이트가 HTTPS를 통해서만 접근되어야 하며 향후 HTTP를 사용하여 사이트에 접근하려는 모든 시도는 자동으로 HTTPS로 변환되어야 함을 브라우저에 알리는데 사용됩니다.

<br />

- 즉, 사용자가 특정 사이트에 HTTP를 사용하여 요청을 보내려 할 때 브라우저가 선제적으로 HTTPS로 요청하게끔 리다이렉트 시키는 변환 작업을 해달라고 지정 및 요청하는 것을 말합니다.

<br />

- 클라이언트가 한 페이지에 처음으로 접근하고 HTTP로 요청을 보냈을 때, 서버가 HTTPS로 301 Moved Permanently 상태 코드로 리다이렉트 시킵니다. (이 때의 리다이렉트는 보통 AWS가 해주는 것이죠.) 이때 Strict-Transport-Security 헤더에 값이 함께 넘어오게 되고, 이 값을 브라우저가 기억하게 됩니다. 이렇게 되면 같은 클라이언트가 또 다시 해당 서비스에 HTTP로 요청을 보낼 경우, 이번에는 서버가 아니라 브라우저단에서 HTTPS로 요청을 보내게끔 307 Internal Redirect로 리다이렉트 시킵니다. 즉, 두 번째 접근부터는 HTTPS를 사용하게끔 강제한다는 것이죠. 아래 그림이 이를 잘 표현합니다.

<br />

<img src="" width=750 />

<br />
<br />

- 이 시나리오를 잘 보면 첫 번째 접속 시에는 HTTP 요청을 막을 수 없고 두 번째 요청에서 부터만 막을 수 있다는 한계가 있습니다. 그렇기에 첫 번째 접근에의 대응을 위하여 AWS 혹은 별도의 다른 방법을 통해 서버가 HTTPS 요청으로 리다이렉트 하도록 하는 처리가 필요합니다.

<br />

---

- Strict-Transport-Security 헤더를 세팅한 사이트인 네이버를 http://www.naver.com URL을 사용하여 의도적으로 HTTP를 사용하여 접근 시 위와 같은 순서로 상태코드가 나오게 됩니다.

<br />

- 시크릿 모드 브라우저를 사용하여 첫 번째로 HTTP를 명시한 네이버의 URL (http://www.naver.com) 에 접근 시 아래와 같이 302 Moved Temporarily 가 나오며 HTTPS 요청으로 강제하게 됩니다. (두 번째 www.naver.com이 HTTPS 요청입니다.)

<br />

<img src="" width=750 />

<br />
<br />

- 그 후 같은 브라우저로 다시 HTTP를 명시한 네이버의 URL (http://www.naver.com) 에 접근하면 아래와 같이 307 Internal Redirect 상태코드를 받으며 HTTPS 요청으로 리다이렉트 됩니다. 위의 순서도와 일치하죠.

<br />

<img src="" width=750 />

<br />
<br />

- 이와 달리 Strict-Transport-Security 헤더가 설정되지 않은 사이트에 HTTP 요청으로 접근하면 여러 번 반복 접근하여도 항상 301 Moved Permanently 상태코드가 나오며 리다이렉트 됩니다. 물론 캐시가 되기에 “307 Moved Permanently (from disk cache)” 상태 코드가 나오고 있습니다. (어찌 보면 이것도 브라우저 단에서 막은 거라고 볼 수도 있기는 합니다.)

<br />

- 출처
  - [What Is HSTS and Why Should I Use It? | Acunetix](https://www.acunetix.com/blog/articles/what-is-hsts-why-use-it/)
