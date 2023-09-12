# HTTP 보안 헤더

### X-XSS-Protection 헤더

- X-XSS-Protection HTTP 헤더는 XSS 공격을 감지 했을 때 브라우저가 페이지 로드를 중지하도록 하는 헤더입니다. 최신 브라우저에서는 Inline Javascript 사용을 못하게 하는 CSP (Content-Security-Policy) 보호기능이 있는데, 해당 기능을 지원하지 않는 구형 웹브라우저에서 사용자를 보호 할수 있는 기능을 제공할 수 있습니다.

- 1; mode=block: XSS 필터링을 사용합니다. 공격이 탐지되면 페이지 렌더링을 중단합니다.
- 1: 공격이 감지되면 브라우저가 안전하지 않은 영역을 제거한 후 렌더링 합니다.

<br />

### X-Frame-Options 헤더

- X-Frame-Options HTTP 헤더는 해당 페이지를 <frame>, <iframe>, <object> 에서 렌더링할 수 있는지 여부를 나타내는데 사용됩니다. 사이트 내 콘텐츠들이 다른 사이트에 포함되지 않도록 하여 Clickjacking 공격을 막기 위해 이 헤더를 사용합니다.

- deny: 어떠한 사이트에서도 frame 내의 src로 포함될 수 없습니다.
- sameorigin: 동일한 Origin을 가진 사이트 내 frame 에서는 보여질 수 있습니다.

<br />

### Strict-Transport-Security 헤더

- Strict-Transport-Security 헤더는 해당 사이트가 HTTPS를 통해서만 접근되어야 하며 향후 HTTP를 사용하여 사이트에 접근하려는 모든 시도는 자동으로 HTTPS로 변환되어야 함을 브라우저에 알리는데 사용됩니다.

- max-age=<expire-time>
  - HTTPS를 통해서만 사이트에 접근할 수 있음을 브라우저가 기억해야 하는 시간을 지정합니다.
  - 참고로 31536000 → 1년, 63072000 → 2년 입니다.

<br />

### X-Content-Type-Options 헤더

- X-Content-Type-Options HTTP 헤더는 서버가 Content-Type 헤더에서 선언한 MIME 타입을 따라야 하며 변경하면 안 된다는 것을 나타내는데 사용됩니다. MIME 타입이 의도적으로 설정되었음을 알려주어 MIME 타입 스니핑을 피할 수 있습니다.

- MIME 타입: MIME 타입은 내려받은 문서나 파일의 특성과 형식을 나타내게 됩니다. 브라우저들은 리소스를 내려받았을 때 해야 할 기본 동작이 무엇인지를 결정하기 위해 MIME 타입을 사용합니다. 예를 들어 text/csv, image/gif, image/x-icon (.ico 파일), application/pdf, application/vnd.openxmlformats-officedocument.spreadsheetml.sheet (.xlsx 파일) 같은 타입이 있습니다.

- MIME 타입 스니핑: MIME 타입이 불명확할 때 브라우저는 MIME 타입 스니핑하여 MIME 타입을 추론하게 됩니다. (Sniff: 코를 킁킁 거리다.) 이때 몇몇 MIME 타입을 실행 가능한 타입으로 읽을 때 보안 문제가 발생할 수 있기에 X-Content-Type-Options 헤더를 통해 브라우저에게 MIME 타입 스니핑을 하지 말라고 알려줄 수 있습니다.

<br />

- 출처
  - [X-XSS-Protection - HTTP|MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection)
  - [X-Frame-Options - HTTP|MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)
  - [Strict-Transport-Security - HTTP|MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)
  - [X-Content-Type-Options - HTTP|MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Content-Type-Options)
