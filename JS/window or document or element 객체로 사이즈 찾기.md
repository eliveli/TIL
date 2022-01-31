## window/document/element 객체로 화면/브라우저/html/body/element 사이즈 찾기
1. element 객체의 property. 특정 요소의 width를 직접 찾을 수 있음
- element.clientWidth : 요소의 패딩 영역까지
- element.offsetWidth : 요소의 패딩, 보더, 내부스크롤바까지 포함
<br>

2. window 객체의 property. 아래 셋은 각각 렌더 전후 같음
- window.screen.width : 윈도우 스크린 width
- window.screen.availWidth : 윈도우 스크린 width. 화면에 위젯이 영역을 차지하고 있다면 위젯을 제외하고 계산.
- window.innerWidth : 브라우저 width (브라우저 스크롤바 포함)
<br>

3. document 객체의 property.

	o html, body 영역은 브라우저 스크롤바 제외

	o 브라우저 스크롤바 여부에 따라 html width가 browser width와 같을 수 있음

	o 정확한 값은 렌더 이후에 나옴(document 객체는 그러함. window 객체는 렌더 전후 동일(테스트한 것 한정)
<br><br>

- document.documentElement.clientWidth
: html 영역의 clientWidth. 
- document.documentElement.offsetWidth
: html 영역의 offsetWidth. 
  <br><br>
- document.body.clientWidth
: body 영역의 clientWidth
- document.body.offsetWidth
: body 영역의 offsetWidth
<br>

- width 테스트
 
	![윈도우,다큐먼트 사이즈 체크3](https://user-images.githubusercontent.com/60069112/151740819-c2f6a7a1-76bf-4b83-bda1-ba41fca7b103.png)


- height 테스트

	![윈도우,다큐먼트 사이즈 체크4](https://user-images.githubusercontent.com/60069112/151740520-d0647649-e0c0-4fd7-9836-4bc85256ef32.png)

~~복잡복잡..~~<br>
html 영역의 clientWidth 와 offsetWidth는 동일한 경우가 있었으나 <br>
  html 영역의 clientHeight 와 offsetHeight는 다르게 나온 경우 있음(브라우저 y축 스크롤 가능, x축 없음)<br>
     이 경우 html의 clientHeight는 브라우저height와 같았으나<br>
               html의 offsetHeight는 html 영역의 전체 height 로 나왔음(보더, 내부x축 스크롤바 없었음)<br>
              이 때 body의 clientHeight와 offsetHeight는 동일하게 나왔음.<br>


헷갈려... 
화면 전체 모달의 길이가 필요할 때는 그냥 모달 요소의 offsetWidth 잡아서 가져오자. document 객체는 필요할 경우에 써야지

-22.01.31-
