오늘 겪은 시행착오 중 몇 가지.

1.
리액트에서 table 만드는 중 문제 발생.
```colgrouop``` 이 작동하지 않음.
```thead```에 적용하지 않은 background-color가 적용됨.(개발자도구로 봤을 때는 thead의 tr에 적용되었던가)
thead와 tbody의 칸 정렬이 다름.
...
대처: thead를 빼 버리고 tbody만 사용...ㅎ thead의 tr을 tbody로 옮김!

2.
카카오 지도 api를 이용해 지도 보이기.
지도는 가져왔는데 위도, 경도 적용이 제대로 안 됨.
```
useEffect(() => {
	const  container = document.getElementById('detailMap');
	const  options = {
		center:  new  kakao.maps.LatLng( latitude, longitude ),
		level:  3
	};
	const  map = new  kakao.maps.Map(container, options);
```
center:  new  kakao.maps.LatLng( latitude, longitude ) 여기에서 위도, 경도를 latitude, longitude 변수에 담아 주었더니 엉뚱한 위치가 나옴...
그런데 변수 말고 숫자 값으로 주었더니 위치가 제대로 표시되고.
왜 그런거지...? 하....

일단 지도 띄우고, 지도에 위치 마커 표시하는 것까지 성공!
 하...막막했는데 아래 링크에서 큰 도움을 받았다.
https://apis.map.kakao.com/web/sample/basicMarker/

지도 위치 오류는 왜 나는지 알아보자..

...
다시 보니 문제 없다... 표시 대로 잘 나오고 있음...
처음에 설정된 주소값과 위도,경도가 서로 달랐나 보다.
아까 팀원분들과 작업 상황을 공유했는데, 그러면서 주소와 지도에 보이는 위치가 다르다는 말씀을 들었거든.
그리고 나서 구글 지도에 해당 주소를 검색했더니 이전 데이터의 위도,경도랑 아주 살짝 다르더라.
새로운 위도, 경도를 가져와 적용했는데 지도가 이전 위치에서 조금 움직였을 뿐이라 지도 위치 설정에 문제가 있는 줄 알았음...
여러 가지로 찾아보다가 내 작업에 띄운 지도와 구글 지도가 같은 위치인 걸 발견!
하.... 확인해보니 문제 없이 잘 작동하네...
ㅎㅎㅎ 하이고
이전 지도의 위치가 하필 내가 사는 지역이었던지라 내가 예전에 지도 검색했던 게 영향을 준 줄 알았어...ㅠㅠㅠ
처음에 위도,경도가 실제 주소와 달랐을 뿐이었고 그 외에는 아무 문제 없었는데....ㅠㅠ

![지도_위치_헤맨것](https://user-images.githubusercontent.com/60069112/126366250-cd5a5c3f-7160-40cb-aeef-e3baffa9f844.png)


진짜ㅋㅋㅋ주소가 강남 압구정동인데 지도는 강남을 빠져나가는 다리 부근을 가리키고 있으니....에고


3.
풀 이미지 화면에 띄웠을 때 이미지 내비게이션에 가려지는 문제.

![이미지 해결하기_ 내비게이션 1](https://user-images.githubusercontent.com/60069112/126366274-361d6c5f-6af8-4495-b267-3212b3e7c9e2.png)
![이미지 해결하기_ 내비게이션2](https://user-images.githubusercontent.com/60069112/126366282-b67637a7-597d-4d07-acf1-00d5b4146fdf.png)

position이 sticky인 내비게이션 컴포넌트가 position이 fixed인 풀 이미지 컴포넌트를 가린다! 
이것저것 테스트해 봤는데!
z-index도 듣지 않았...었는데...
헐?
개발자도구에서 풀이미지 컴포넌트에 z-index:2 를 설정했더니 아무것도 얘를 가리지 않는다.
z-index:1 로 설정하면 지도에 가려짐ㅎㅎ
z-index:0 이면 지도, 내비게이션 둘 모두 얘를 가리고.
z-index:-1 은 페이지의 모든 요소들이 가리고ㅎㅎ(어머 신기해라 배경 느낌이네ㅎㅎ)
그래서 z-index:2로 하기!

아까 z-index로 테스트할 때는 안 되었었는데ㅎㅎㅎ

뭔가 테스트해볼 때는 작업하는 에디터에서 하기 보다 브라우저에서 하는 것도 좋겠다....
적용하는데 걸리는 시간도 줄고 변화도 빨리 감지할 수 있고...
무엇보다 에디터에서 적용하면 브라우저 새로고침 해야 하니까ㅋㅋㅋ
이유는 모르겠지만 에디터에서 적용한 게 브라우저에 바로 반영이 안 될 수도 있고.. 아까도 새로고침 했을 텐데 적용 안되었던 거 보면.... 뭐 다른 곳에 문제가 있었을 수도 있지만.
여튼! 
바로바로 눈으로 확인해 보려면, 특히 CSS 테스트는 브라우저에서 개발자도구로 해 보는 것도 좋겠다...! 진짜...!
어제 팀원 분이 내가 겪고 있던 문제 해결하실 때도 브라우저 개발자도구로 값 변경하며 테스트해보신 것 같더라ㅎㅎ

(+)
이미지 아이콘 넣을 때 최대한 클론 사이트와 비슷하게 하려 하니 힘들었다.
초반에는 무료 소스 가져다가 편집해 쓰거나 간단해 보이는 건 내가 만들기도 했는데,
시간 많이 걸리고 비율 문제 등으로 결과물이 예상과 달라서(내가 만든 이미지...ㅋ)
머티리얼 아이콘 사용.
근데 얘도 크기를 키우니 외곽선이 굵어서 주위 이미지들이랑 어울리지 않음...
심지어 내가 찾는 이미지아이콘도 없는 경우가 많음.
그래서 결국은 무료이미지아이콘을 다운 받아 일일이 이미지 백그라운드로 넣어줌..
ㅎㅎㅎ(최대한 비슷하게 만드는 건 포기...아이콘을 어떻게...하..)
그래도 머티리얼 아이콘도 나름 유용하게 쓸 수 있을 듯.
작은 아이콘이 필요할 때 + (이건 확실치 않지만)css 파일에 링크를 넣어 바로 사이트의 이미지아이콘을 쓸 수 있을 때..? 리액트에서도 가능할 것 같은데..!  
-2021.07.20-
