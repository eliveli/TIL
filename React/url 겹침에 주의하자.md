### 문제 상황
- 설정: 로그인하지 않은 경우 톡톡 작성 페이지에 들어가면 톡톡 메인 페이지로 이동됨
- 문제: 이동 이후 다른 작업(dispatch)이 실행됨

### 원인 탐색
- 조건문 미작동?   
 ![1조건문](https://user-images.githubusercontent.com/60069112/128404999-aa52a5db-e9f2-4364-aa73-32ae4ef9402d.jpg)

  - if ( ...  ) {  ... return ; } 조건 만족했으나 끝나지 않고 다른 조건문의 작업이 실행됨
  - 조건문을 else if 로 연결해도 결과는 같음.
  - 테스트 결과 조건문은 문제가 없음. 다른 페이지에서 동일한 작업이 실행됨.
- 문제가 되는 코드
``` 
    if (!is_login) {
        alert("로그인 후 이용하세요~"); 
        history.replace("/talk");
        return;
    }
```    
  - alert 확인 버튼 누르기 전:
    - 톡톡 작성 페이지가 보임
    - 콘솔에서 톡톡 상세 페이지로 이동됨 ( 화면에 렌더링되지는 않음 )
  - alert 확인 버튼 누른 후:
    - 톡톡 메인 페이지로 이동
    - 직후 dispatch 작업이 실행됨. 상세페이지에 같은 작업이 있음.

- url 구분:   
![원인2](https://user-images.githubusercontent.com/60069112/128405184-7a7e4e0f-dfc7-46c0-bf7d-f7bbfa6a8a03.jpg)
  - talk/write  (문제 발생. 상세 페이지 연결됨. 포스트 작성 시)
  - talk/write/:id  (문제 없음. 포스트 수정 시)
  - talk/:id  (상세 페이지)   

![원인파악](https://user-images.githubusercontent.com/60069112/128405161-20b7da49-e254-4852-996c-8529c31bd8bf.jpg)

- 콘솔 확인하니 상페 페이지에서 url의 id값이 write로 나옴
- 페이지 이동 조건 분기를 빼 버려도 상세페이지로 이동됨.
- 상세페이지 만든 이후 url이 겹치면서 문제가 발생한 것...

### 문제 해결   
- 상세페이지 url 수정.
-  talk/:id   ->   talk/detail/:id     
![해결](https://user-images.githubusercontent.com/60069112/128405235-1f0b95ea-f76f-4bb5-a003-903b68288087.jpg)

### 잡담
- 수 시간을 들여 문제 해결...
- 사소하지만 사소하지 않은 곳에서 문제가...생기는군...

-2021.08.05-
