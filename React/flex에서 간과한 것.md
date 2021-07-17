## 최종 결론:
    1. 불필요하게 flex 설정을 주면서 삽질함(디폴트가 flex라...)
    2. 코드는 간결하게
    3. flex 설정을 좀 더 알아보자




개별 flex 아이템에 정확한 width 설정하기.  
-flex item을 다시 flex container로 만들 때 유용!-  
  
(추가. 아래 방법은 모든 flex item의 디폴트 width를 100%로 설정한 경우 특정 flex item에 고정값 width를 주는 방법임.  
원래는 flex-item도 고정값 width 설정이 가능함!  
주위 flex item들과 설정값을 잘 조정하기만 한다면....)  
```
1. <flex container>  
2.   <1번의 flex item이자 3번의 flex container>  
3.		<flex item>  
```
2번에 정확한 width를 주고 싶었음.    

찾은 방법:  
```
🎈css에서.  
div {  
  flex : 0 0 500px;           
}  
```
```
🎈react에서. (Grid 컴포넌트에 flex를 props로 미리 설정하기)  
<Grid flex="0 0 500px">      
```
 
`flex: 0 0 500px;`   
차례로  `flex-grow`, `flex-shrink`, `flex-basis`   
앞의 둘은 0으로 해 주고 고정 width값을 세 번째 순서에 넣어 주기.  
~~flex-grow, shrink ...나는 너희들과 친해지고 싶지 않단다....이런 마인드였는데 세상에 이렇게 도움이 될 줄은...~~   
width 설정이 만족스럽지 않아 꽤 헤맨 터라 신대륙 발견한 기분...😀  
  
시도한 방법:  
1. width 설정  
- 고정값 주기(ex. 500px) -> 설정대로 적용 안 됨  
- 비율 설정(ex. 50%).  
   -- 최상위 flex 컨테이너는 고정 width 설정 가능. 그러므로 하위 flex item에 비율값 width는 잘 적용됨.  
   -- 클론코딩에서 적용 시 문제점은  
		 . 비율 값이기에 내가 딱 원하는 width는 얻지 못할 수 있음.  
        . 클론할 사이트에서 부모 width와 자식 width의 고정값으로 비율을 계산해야 함(ㅎㅎㅎㅎ)  
      . 일단 보류....   
2. min-width  
 1번과 같은 문제. (px로 고정값 width 적용이 안 됨)  

3. padding 설정  
  - 내용이 입력되는 하위 컴포넌트가 있기에 padding으로 width를 대체하기 어려움.  
   -- (width == padding 가로 길이 + 입력된 데이터의 가로 길이)  
  -- 넣어주는 내용이 다 다르니 전체 width도 바뀜...  

https://pythonq.com/so/html/739024  
 (얘는 참고 링크!)





<hr />

헐.... width 를 디폴트 100%로 설정해 놓고 쓰고 있었어...  
원래는 flex도 고정 width 설정이 가능한데....  
근데 왜 아까는 width 적용이 잘 안 되었지?  
flex 컨테이너 안에 flex 아이템이 여럿 있어서 각 아이템이 width 100%가 되어 그런가?   
->그러면 각 아이템이 부모 width를 똑같이 나누어 가짐. 각각 같은 가로 길이를 가지는 것.  

```
1. <flex container>
2.   <1의 flex item && flex container>
3.		<flex item>
4.	    <flex item>
5.	 <flex item>
```

3~4번은 flex-start, 5번은 flex-end처럼 정렬하고,  
5번을 여유 공간으로 설정하고 싶음.  
  
그래서 3~4번의 각 flex item들은 딱 데이터 길이만큼의 가로 길이를 가지면서(stretch 되지 않고 )  
3~4번에 데이터가 얼마나 입력되든 상관 없이   
5번의 여유 공간 부분만 줄었다 늘었다 했으면 좋겠음.  


시행착오.  
1.  
1번 flex container에  space-between 설정  
-> 2번 5번이 똑같은 가로 길이를 가짐.  
-> 2번에 justify-content 설정을 적용해도 3번 4번에 먹히지 않음  
나는 3번 4번 5번 flex item들이 서로 다르게 정렬되길 바람.  
  
---> 여기에서 문제가 된 것: 얘네 모두 디폴트 width를 100%로 했음. 그러면 flex item들이 부모인 flex container의 width를 똑같이 나누어 가지게 됨.  
따라서 내부 flex item 정렬이 의미가 없음.... 다 똑같이 부모 컨테이너를 꽉 채우면서 같은 길이를 가지는 걸...  
  
2.   
특정 flex item에 width="auto" 설정  
-> 데이터가 들어있는 content의 가로 길이에 꼭 맞게 width 적용됨  
(불필요한 여백 없음)  
->글자가 한 줄에 이어지지 않음. 몇 글자 씩 다음 줄로 내려감...  
->대체 왜?  
  
3. 기본 Grid 컴포넌트에 적용된 style을 바꿈.  
```display : flex;``` (변경 전)  
```display: ${(props) =>  props.display || "flex"};``` (변경 후)  
  
display 설정을 block으로 각각 주면서 관련 설정들을 제거했더니 원하는 결과가 나옴...!  
  
그리고 마지막 글자가 다음줄로 넘어가는 건 ```white-space ``` 를 적용해서 해결!
  
```white-space: ${(props) =>  props.whiteSpace || ""};```  
  
다른 분의 답변 덕에 문제 해결...!   
하....기본 flex 설정을 잊고 있었구나.  
습관대로 사용하다가 오해를..삽질을....쿨럭...
  
그리고 불필요한 부분은 최대한 제거하는 게 좋음...  
팀업이라 공통 컴포넌트 설정을 바꾸는 게 다소 꺼려지더라도 필요하면 해야 함...  
값을 넘겨주지 않을 때 디폴트 설정만 하면 되는 거면 더욱...!  
-2021.07.17-
