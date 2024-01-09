# Device Pixel Ratio in Canvas

- 3D 뷰어 어플리케이션을 만들다보니 canvas 태그를 주되게 사용하고 있습니다. 그런데 사실 canvas 태그 내에 렌더링 하는 부분들은 모두 외부 유료 라이브러리가 해주다보니 저는 간접적이게만 canvas를 사용하고 있습니다.

<br />

- 그런데 해당 라이브러리의 소스코드를 보면 3D 좌표와 canvas 상 좌표로 변환하는 동작이나 반대 동작을 수행하는 경우 항상 window.devicePixelRatio라는 값을 사용하여 곱하거나 나누는 과정을 수행합니다. 그 값의 의미와 사용 이유에 궁금증이 생겨 한 번 조사해보았습니다.

<br />

---

<br />

- Physical pixels and Logical pixels
  - Physical pixels: 단말이 실제로 표현할 수 있는 물리적인 화소(pixel)의 기본 단위.
  - Logical pixels: HTML/CSS에서 논리적으로 표현할 수 있는 화소의 기본 단위.

<br /> 
 
- DPR (device-pixel-ratio): The ratio between physical pixels and logical pixels
  - 뷰포트는 CSS 픽셀을 단위로 가지지만, 기기는 물리적 픽셀을 단위로 가집니다.
  - 어떤 기기에서는 물리적 픽셀이 CSS 픽셀보다 4배 작기도 하고, 어떤건 9배 작기도 합니다.
  - 높은 해상도의 기기일수록, 높은 DPR을 가지고 있다고 합니다. 즉, 하나의 CSS 픽셀 안에 많은 물리적 픽셀이 들어가 있는 것이죠.

<br />
 
<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/7aacc71e-4fe5-450c-a45f-c26f5e1a18bf" width=500 />

<br />

- 자바스크립트에서 다루는 일반적인 px는 뷰포트 상에서의 값으로 CSS 픽셀 단위를 가지고 있습니다.
  - MouseEvent에 들어가 있는 OffsetX, ClientX 같은 값은 CSS 픽셀 단위의 값이고
  - absolute position에 지정하는 top, left 값도 CSS 픽셀 단위의 값이죠.
  - 참고로 DOM 요소의 width, height도 CSS 픽셀 단위입니다.

<br />
 
- 그런데 Canvas의 경우 조금 더 고해상도로 제공하기 위하여 HTMLCanvasElement의 width 속성과 style.width 속성을 사용하여 canvas 태그 내 픽셀 단위를 CSS 픽셀과 다르게 설정할 수 있습니다. (마찬가지로 height도 두 가지가 존재합니다.)
  - canvas.width 를 통해 설정한 width의 경우 canvas 내부의 width로 해당 디바이스의 물리적 픽셀의 한계까지 입력할 수 있습니다. (canvas 내 그림의 해상도를 높게 표현하기 위해 사용하죠.)
  - 반대로 canvas.style.width를 통해 설정한 width는 뷰포트에 그려지는 canvas 태그의 크기로 일반적인 CSS 픽셀 단위를 따릅니다.

<br />

- 만약 아래와 같은 방식으로 width, height를 부여한다면 canvas의 실제 사이즈는 800 X 600 픽셀인 반면 그림을 그리기 위한 픽셀은 400 X 300 픽셀이 됩니다. 그러다보니 Canvas 상 하나의 픽셀이 화면의 2 X 2 픽셀에 표현이 되고, 흐릿한 이미지가 만들어지게 됩니다.

```
canvas.width = 400;
canvas.height = 300;
canvas.style.width = '800px';
canvas.style.height = '600px';
```

<br />

- 저희가 사용하는 라이브러리의 경우 초기 initialize 코드에는 아래와 같은 방식으로 canvas의 width, height를 지정하는 로직이 들어있습니다. 이 경우 CSS Pixel 단위의 폭은 부모의 width, height에 꽉 채우게 되고, canvas 내의 해상도를 표현하는 width는 devicePixelRatio 를 곱한 화면의 최대 해상도 (물리적인 Pixel 단위의 width) 를 사용하게 됩니다.

```
canvas.style.width = "100%";
canvas.style.height = "100%";

canvas.width = canvas.clientWidth * window.devicePixelRatio;
canvas.height = canvas.clientHeight * window.devicePixelRatio;
```

<br />

- 이러한 이유로 Canvas내에서 좌표를 쓸 때는 device의 좌표인 물리적 픽셀을 사용하여야 하고, Viewport에 표현하는 좌표를 쓸 때는 CSS의 논리적 픽셀을 사용하여야 합니다. 그래서 Canvas 태그를 사용하는 어플리케이션에서 Canvas 상의 좌표와 Viewport 상의 좌표 간 변환을 하고자할 때 devicePixelRatio을 곱하거나 나누는 절차가 필요한 것입니다.

<br />

- 출처
  - [[CSS] DPR(Device-pixel-ratio)의 이해](https://velog.io/@vnfdusdl/DPRDevice-pixel-ratio%EC%9D%98-%EC%9D%B4%ED%95%B4)
  - [Device-pixel-ratio](https://traodoicv.com/thiet-ke-web-responsive/)
  - [Canvas width and height in HTML5](https://stackoverflow.com/questions/4938346/canvas-width-and-height-in-html5)
