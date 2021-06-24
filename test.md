# 클릭- 구분- 요청
![enter image description here](https://lh3.googleusercontent.com/taxCKkXSSBRaDDB1TvD9fcBYx9zaBaUgKGYR6VhbHR_aGgUT0boMK9ngb-NfJta-yExlOcClmHn__sk6VzCznSoR2b6W5wflqaMw4yVHki4IF_HrfKtg7hPAJ_kzwdppGjM_imfK1qzrmYOMwhmdzDIR75oVz8WcfpGO1I8Ln1pO_vYIY59jshPr9KcISmqEWdp53Sg8gMo9Pm3wyr5-pvnflcpSsxvn3jMoAlHrEcWokLGhBkj7IZMPdGPXV9Ss0ZZhD-4DojNQELqVNZvKewwsbsNfWM6xAlDTWgsfjSEAH_filQWFiXHt3i09LFHtD3r7TP0vimXHU6E6Xx_rwQo4llMITdOE1fiUSNaJQkCTGBFVAC_T-kI50dtYEOUYtDiVanmoFqYXCwWLiaQFgsf1U-oiGUrcfaX2ZKP2WeNfNQfk6E-bkjHj0gZV5cn5djS0-2z920jwmPXCfcQeHDC9oyX0cYa6253BIIk2D0uM1yOJPK_4mjGFX1V1Pf_-_m-bB-6xkT1nQlejKWJzKGsoxBFUqWgmjW4q53A2hl6xN5eqIlKWKTMi3oBva2VMbE52O6B8dGX01SJTzGrCMi1OfzXu4B_CYUx2jEqU_g68xL0mwWdNcI3qDK46yJKwtQ6VXGJPFCIiPYGzWz18LrMosmw8InnY7njjeMxXdYl6Nw28pn-J9bLfJiCUQf7sA1r1B2s_ORpsmbf_nZcNSwlv=w488-h625-no?authuser=0)

카드 클릭 시 그 카드에 해당하는 정보를 받아 서버에 요청하는 코드.
지난번 프로젝트 때 내가 만들었다가 사용은 안 했는데
혹시 나중에 참고할 일이 있을까 해 정리해서 올려 봄

   ```
   <script>
        let info_list = ['1', '2', '3', '4', '5', '6', '7', '8']; 
        let card_list = document.getElementsByClassName('card');
        
        // 카드 클릭 시 실행
        function show_detail(event) {
	       card = get_card(event)
	       
	       index = get_index(card);
	       
	       info = get_info(index);
	       
	       req_detail(info);
	   }
	   
	   function get_card(event) {
	       let target_element = event.target;
	       while ('card' !== target_element.getAttribute('class')) {
	           target_element = target_element.parentNode
	       }
	       return target_element
	   }
	                   
	   function get_index(card) {
	       for (let i = 0; i < card_list.length; i++) {
	           if (card === card_list[i]) {
	               return i;
	           }
	       }
	   }
	   
	   function get_info(index) {
	         return info_list[index]
	   }
	   
	   function req_detail(info) {
	       $.ajax(  요청 내용  )
	   }
</script>
```
```
<div class="card" onclick="show_detail(event)">
	<img />
	<div>
	    <h2>제목</h2>
	    <p>부제</p>
	    <div>요약 등등</div>
	</div>
</div>
```

- ```<script>``` 첫 줄에 있는  ```info_list``` 는 서버에서 카드 데이터를 가져와 카드를 만들 때 같이 만듬(이 코드에는 그 내용이 없음). 카드 구분을 위한 것.(카드의 인덱스 == info 인덱스)

-  ```<div class="card" onclick="show_detail(event)">``` 의 부모 태그인 카드리스트를 만들었더니 그 안에 직접 만든 카드 외에 다른 것들이 생겨남! 그런 고로 카드 끼리의 인덱스를 알 수 없었다...     
	그래서 '카드' 클래스만 모아 인덱스를 찾는 방법으로 변경한 것(아래 내용)
	```<script>``` 둘째 줄 ```let card_list = document.getElementsByClassName('card');```

-2021.06.24-
