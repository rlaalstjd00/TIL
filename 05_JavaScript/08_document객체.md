## document 객체

웹 페이지 그 자체를 의미한다. 웹 페이지에 존재하는 HTML 요소에 접근하고자 할 때에는 반드시 document 객체부터 시작한다.

#### document.getElementById("아이디")

해당 아이디를 가진 요소를 선택하여 객체로 가져온다.

````html
<div id = "hello">
    안녕하세요 자바스크립트 입니다.
</div>

<script>
	let divTag = document.getElementById("hello");
    divTag.style.color = "red";
</script>
````

> id가 "hello"인 태그를 선택에 글씨 색을 red로 설정.

#### document.getElementsByTagName("태그명")

해당 태그인 요소들을 선택하여 배열로 가져온다.

````html
<ul>
    <li>JAVA<li>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>

<script>
	let liTag = document.getElementsByTagName("li");
   	for(let i=0; i<liTag.length; i++ ){
        liTag[i].style.color = "white";
        liTag[i].style.background = "black"; 
    }
</script>
````

> li 태그의 모든 요소들의 글자 색을 white, 배경색을 black으로 지정.

#### document.getElementsByClassName("클래스명")

해당 클래스를 가진 요소들을 선택하여 배열로 가져온다.

````html
<ul>
    <li class="odd">JAVA<li>
    <li class="even">HTML</li>
    <li class="odd">CSS</li>
    <li class="even">JavaScript</li>
</ul>

<script>
	let oddItems = document.getElementsByClassName("odd");
    for(let li of oddItems){
        li.style.color = "red";
    }
</script>
````

> odd 클래스를 가진 태그의 글자 색 red로 지정.

#### document.querySelectorAll("CSS 선택자")

선택자에 해당하는 요소를 배열로 가져온다.

````html
<div id="hello">
    안녕하세요 자바스크립트 입니다.
</div>

<script>
	let divTag = document.querySelectorAll("#hello");
    divTag.style.color = "red";
</script>
````

> id가 "hello"인 태그를 선택에 글씨 색을 red로 설정.

