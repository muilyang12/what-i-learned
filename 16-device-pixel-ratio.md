# Device Pixel Ratio

- Physical pixels and Logical pixels
  - Physical pixels: 단말이 실제로 표현할 수 있는 물리적인 화소(pixel) 기본 단위.
  - Logical pixels: HTML/CSS에서 논리적으로 표현할 수 있는 화소 기본 단위.

<br />
 
- DPR (device-pixel-ratio): The ratio between physical pixels and logical pixels
  - 뷰포트는 CSS 픽셀을 단위로 가지지만, 기기는 물리적 픽셀을 단위로 가집니다.
  - 어떤 기기에서는 물리적 픽셀이 CSS 픽셀보다 4배 작기도 하고, 어떤건 9배 작기도 합니다.
  - 높은 해상도의 기기일수록, 높은 DPR을 가지고 있다고 합니다. 즉, 하나의 CSS 픽셀 안에 많은 물리적 픽셀이 들어가 있는 것이죠.

<br />
 
<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/7aacc71e-4fe5-450c-a45f-c26f5e1a18bf" width=500 />

<br />

- 자바스크립트에서 다루는 px은 일반적으로 CSS 픽셀입니다.
  - MouseEvent에 들어가 있는 OffsetX, ClientX 같은 값은 CSS 픽셀 단위의 값이고
  - absolute position에 지정하는 top, left 값도 CSS 픽셀 단위의 값이죠.
  - 참고로 DOM 요소의 width, height도 CSS 픽셀 단위입니다.

<br />
 
- 그런데 Canvas의 경우 조금 더 고해상도로 제공하기 위하여 HTMLCanvasElement 의 width, height 속성을 이용하여 내부의 픽셀 단위를 CSS 픽셀과 다르게 설정할 수 있습니다. canvas.width 를 통해 입력한 width의 경우 내부의 픽셀 단위이고, canvas.style.width를 통해 입력한 width는 일반적인 CSS 픽셀 딘위입니다.

<br />

- 이러한 이유로 Canvas내에서 좌표를 쓸 때는 device의 좌표인 물리적 픽셀을 사용하여야 하고, Viewport에 표현하는 좌표를 쓸 때는 CSS의 논리적 픽셀을 사용하여야 합니다. 그래서 Canvas 태그를 사용하는 어플리케이션에서 Canvas 상의 좌표와 Viewport 상의 좌표 간 변환을 하고자할 때 devicePixelRatio을 곱하거나 나누는 절차가 필요한 것입니다.

<br />

- 출처
  - [[CSS] DPR(Device-pixel-ratio)의 이해](https://velog.io/@vnfdusdl/DPRDevice-pixel-ratio%EC%9D%98-%EC%9D%B4%ED%95%B4)
  - [Device-pixel-ratio](https://traodoicv.com/thiet-ke-web-responsive/)
