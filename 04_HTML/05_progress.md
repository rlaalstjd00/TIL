## progress

progress 태그는 진행 정도를 나타내는 태그이며 `<progress value="" max=""> </progress>` 의 형식으로 쓰인다.

`max` 속성은 전체 진행을 나타내는 숫자가, `value` 속성에는 현재 진행 정도를 나타내는 숫자를 쓴다. `max` 중에서 `value` 만큼 채워진 바의 형태로 나타난다.

````html
<!-- 100중에서 20만큼 채워진 바 -->
<progress value="20" max="100"> </progress>
<!-- 100중에서 60만큼 채워진 바 -->
<progress value="60" max="100"> </progress>
````

JS와 같이 사용해 버튼을 누르면 진행 정도가 올라가게 설정할 수 있다.

````html
<body>
    <!-- "pg"라는 아이디를 가진 max가 100인 진행 바 -->
    <progress id="pg" value="0" max="100"></progress>
    <!-- "진행"이라고 적힌 버튼을 만들고, 그 버튼이 클릭되면 doing()이라는 함수가 실행된다. -->
    <input type="button" value="진행" onclick="doing();">
</body>
<script>
    <!-- JS/ doing() 함수 -->
    <!-- "pg" 라는 아이디를 가진 것의 value 값에 +10
	function doing(){
        document.getElementById("pg").value += 10;
    }
</script>
````

