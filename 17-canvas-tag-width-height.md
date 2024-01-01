# Canvas 태그의 width, height

- canvas 태그에는 width 라고 인지되는 속성이 canvas.width 와 canvas.style.width 두 가지가 존재합니다. (height 에서도 마찬가지로 두 가지가 존재합니다.)
  - 여기서 canvas.width 의 경우 논리적인 Pixel 단위의 폭으로 Drawing 을 위하여 필요한 값입니다.
  - 그리고 canvas.style.width 의 경우 CSS Pixel 단위의 폭을 의미합니다.

<br />

- 만약 아래와 같은 방식으로 width, height 를 부여한다면 canvas 의 실제 사이즈는 800 X 600 픽셀인 반면 그림을 그리기 위한 픽셀은 400 X 300 픽셀이 됩니다. 그러다보니 Canvas 상 하나의 픽셀이 화면의 2 X 2 픽셀에 표현이 되고, 흐릿한 이미지가 만들어지게 됩니다.

```
canvas.width = 400;
canvas.height = 300;
canvas.style.width = '800px';
canvas.style.height = '600px';
```

<br />

- 그러한 이유로 Canvas 를 사용하는 일반적인 어플리케이션의 경우 아래와 같은 방식으로 Canvas 의 width, height를 지정하게 됩니다. 이렇게 지정할 경우 CSS Pixel 단위의 폭은 부모의 width, height에 꽉 채우게 되고, 논리적인 Pixel 단위의 폭은 devicePixelRatio 를 곱한 화면의 최대 해상도의 width, height가 사용되게 됩니다.

```
canvas.style.width = "100%";
canvas.style.height = "100%";

canvas.width = canvas.clientWidth * window.devicePixelRatio;
canvas.height = canvas.clientHeight * window.devicePixelRatio;
```

<br />

- window.devicePixelRatio 를 곱하고 나누는 것의 의미는 [16-device-pixel-ratio.md](https://github.com/muilyang12/what_i_studied/blob/main/16-device-pixel-ratio.md?plain=1)에서 설명한 내용을 보시면 알 수 있습니다.

<br />

- 출처
  - [Canvas width and height in HTML5](https://stackoverflow.com/questions/4938346/canvas-width-and-height-in-html5)
