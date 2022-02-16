## window 객체

#### window 객체

웹 브라우저의 창을 나타내는 객체로, 대부분의 웹 브라우저에서 지원한다. 자바스크립트의 모든 객체, 전역함수, 전역 변수들은 자동으로 window 객체의 프로퍼티가 되고 window 객체의 메서드는 전역함수, window 객체의 프로퍼티는 전역변수가 된다.

#### 1. wndow.onload

스크립트 언어는 위에서 아래로 해석되기 때문에 DOM에서 HTML 요소를 추출할 때 body보다 위에 있다면 해석 순서에 문제가 생길 수 있다. 따라서 문서가 다 준비된 상황 이후에 발동하게끔 하는 역할을 한다.

> window.onload = function(){
>
> ​		문서가 로딩된 이후에 호출할 문장
>
> }

#### 2. window.setTimeout()

설정한 시간 이후에 넘겨주는 함수를 호출한다.

> window.setTimeout(함수, 밀리초);

#### 3. window.open()

새로운 브라우저 창을 열 수 있으며, 새로운 창의 세부적인 옵션들도 설정할 수 있다.

> `let 객체명 = window.open(url, name, specs, replace);`
>
> - url : 열어줄 주소
> - name : 열리는 창의 이름
>   - `_blank` : 새 창에서 열림
>   - `_child` : 자식 프레임
>   - `_parent` : 부모 프레임
>   - `_self` : 현재 창에서 열림
> - specs : 선택적인 값으로 창의 크기, 스크롤 여부, 리사이즈 등을 지정
> - replace : 히스토리 목록에 새 항목을 만들지, 현재 항목을 대체할지 지정한다.
>   - `true` : 현재 히스토리 대체
>   - `false` : 새 항목

````js
window.onload = function(){
    window.setTimeout(function(){
        let google = window.open("https://www.google.co.kr","_blank",
                                "width=600 height=300", true);
    }, 3000);
}
````

> 페이지가 로딩된 후 3초(3000밀리초)가 지나면 구글 페이지가 새 창에서 열리게 설정