## location 객체

현재 브라우저 표시된 HTML 문서의 주소를 얻거나, 브라우저의 새 문서를 불러올 때 사용한다. location 객체의 프로퍼티와 함수를 이용하면 현재 문서의 URL 주소를 다양하게 해석하여 처리할 수 있다.

#### location.href

현재 페이지의 URL 정보가 담겨있는 프로퍼티

대입을 통해 새로운 문자열을 넣으면 페이지 이동이 일어난다.

#### location.reload()

새로고침

#### location.assign("URL주소")

현재 URL을 지정한 URL로 바꿔서 이동

> `assign`은 단순한 이동으로, 이전 페이지로의 이동이 가능하다.

#### location.replace("URL 주소")

현재 URL을 지정한 URL로 대체해서 바꾸고 이전으로 이동 불가

> `replace`는 이전 사이트가 이동된 사이트로 덮어씌워졌다고 생각하면 된다. 따라서 이전페이지로의 이동이 불가능하다.

```` html
<html>
<head>
<meta charset="UTF-8">
<title>이동할 페이지 선택</title>
</head>
<body>
	<form id="myForm" name = "myForm">
		<p>
			<label>
				네이버<input id="site" type="radio" value="naver" name="site" checked>
			</label>
		</p>
		<p>
			<label>
				다음<input id="site" type="radio" value="daum" name="site">
			</label>
		</p>
		<p>
			<label>
				구글<input id="site" type="radio" value="google" name="site">
			</label>
		</p>
		<p>
			<input type="button" onclick="sendit()" value="이동">
		</p>
	</form>
</body>
<script>
	function sendit(){
		let frm = document.myForm;
		let inputTag = frm.site;
		switch(inputTag.value){
		case "naver":
			location.href = "https://www.naver.com";
			break;
		case "daum":
			location.href = "https://www.daum.net";
			break;
		case "google":
			location.href = "https://www.google.com";
			break;	
		}
	}
</script>
</html>
````

> 위의 코드에서 이동할 페이지의 라디오 버튼을 체크하고 이동 버튼을 누르면 `location.href` 로 연결된 해당 사이트로 이동하는 것을 확인할 수 있다.



## history 객체

브라우저의 히스토리 정보를 문서 상태 목록으로 저장하는 객체

#### history.go(n)

n만큼 페이지 이동. 

양수면 앞으로, 음수면 뒤로, 0이면 새로고침

#### history.back

뒤로가기

#### history.forward()

앞으로 가기