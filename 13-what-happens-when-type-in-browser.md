# What happens when you type google.com in your browser

1. Browser는 캐싱된 DNS 기록을 조회하여 www.google.com에 대응되는 IP 주소가 있는지 확인합니다.

2. 요청한 URL이 캐시에 없으면 DNS query를 날려서 www.google.com을 호스팅하고 있는 서버의 IP 주소를 찾습니다.

3. Browser가 웹 서버에 HTTP 요청을 합니다.

4. 서버가 요청을 처리하고 HTTP response (index.html) 을 보냅니다.

5. Browser가 HTML, CSS, JS를 해석하여 컨텐츠를 보여줍니다.

<br />

- 출처
  - [Browser에 www.google.com을 검색하면 어떤 일이 일어날까?](https://devjin-blog.com/what-happen-browser-search/)
