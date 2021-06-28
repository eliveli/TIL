# router & redux
오늘은 3주차 강의를 수강했다. 라우터와 리덕스에 관한 내용인데 간단하게만 정리해야지.

## react-router-dom
```react-router-dom``` 이 아이의 도움을 받아 리액트에서 라우팅을 할 수 있다!
```
...
ReactDOM.render(
	<BrowserRouter>
		<App />
	</BorserRouter>,
	document.getElementById("root")
);
```
이렇게 ```App``` 컴포넌트를 ```BrowserRouter```가 감싸 주고,
```App``` 내부에서는 경로에 따라 뷰를 그려줄 컴포넌트 를 연결해 준다.
```
<Route path="/경로 " component={ 컴포넌트 } />
```
아래와 같이 링크를 통하면 미리 설정한 라우트의 경로로 연결되어 뷰를 볼 수 있다.
```
<Link to = "/경로"> 여기를 클릭하면 이동! </Link>
```

링크와 또 다른 방식의 페이지 이동을 할 수도 있는데,  ```this.props.history.push('/경로 ')```이렇게 history 객체를 이용하면 된다.

강의에서는  ```withRouter```로 App을 감싸준 후에 props를 받아올 수 있었다.
```export default withRouter(App)``` 
그래서 난 ```withRouter```가 필수적인 줄 알았는데, 검색해보니 꼭 그런 건 아닌 듯하다.  ```App```이 라우트되지 않는 컴포넌트라서 ```history```객체를 사용하기 위해 ```withRouter```를 이용한 거라는 듯.
```<Route path = "/ 경로" component = { 컴포넌트 }>```
이렇게 App 안의 다른 자식 컴포넌트들은 route되면서 바로 props의 history 객체를 사용할 수 있지만 ```App```은 부모라 route 설정을 줄 수 없으니까...!

...라고 이해했는데 맞는지 잘 모르겠다.
강의에서는 App에서 다른 컴포넌트로 history를 props로 넘겨줘서 사용하게 하던데 위 맥락 대로라면 route 처리한 컴포넌트이니 굳이 그럴 필요 없이  history 객체를 사용할 수 있는 것 아닌가? 
아니면 강의에서는 props를 자식 컴포넌트로 넘겨주는 걸 보여주기 위해 부러 그렇게 한 거라던가..?
강의 영상을 굳이 챙겨보지 않고 강의 자료를 통해 학습 중인데, 그래서 강사님 설명을 놓친 부분이 있을 지도 모르겠다... 아 피곤해 일단 지금은 자러 가야겠다.. 일단은 진도 나가고 의문점은 나중에 기회 되면 좀더 알아보자...


그리고 Redux는 모든 컴포넌트의 state 관리를 ```store``` 한 곳에서 하게 해 준다. 액션, 액션 크리에이터, 리듀서, 스토어 등 여러 관련 개념들이 있음.
(졸려서 더 적기는 진짜 무리.. 굿나잇..🙏)

-2021.06.27- (인데 시간은 다음날 03:45..