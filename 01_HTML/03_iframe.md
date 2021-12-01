## iframe

inline frame 요소로 해당 웹페이지 안에 또 다른 하나의 웹페이지를 삽입할 수 있다. 

(단, 정보보호를 위해 iframe기능에 제한을 둔 사이트들은 새 창으로만 접근이 가능하다.)

`<iframe src="삽입할 페이지 주소">대체 내용</iframe>`

> iframe 태그를 지원하지 않는 브라우저를 위해 태그 사이에 대체 내용을 넣어주는 것이 좋다.

- iframe과 함께 사용가능한 CSS 속성

1. src : iframe에 삽입할 페이지 주소
2. width : iframe의 너비 지정 (px, %)
3. height : iframe의 높이 지정 (px, %)
4. frameborder : 테두리 유무 설정 (1 테두리있음, 2 테두리없음)
5. scrolling : 스크롤바 유무 선택 (yes 스크롤바표시, no 표시안함, auto 자동)
6. marginheight : 내용의 위 아래 margin
7. marginwidth : 내용의 좌 우 margin
8. align : iframe을 정렬 (top, middle, bottom, left, right)
9. name : target이 필요한 프레임 이름

````html
<iframe src="https://www.naver.com" stlye="width:100%; height:600px;">
    이 브라우저는 iframe을 지원하지 않습니다.
</iframe>
````

> 위의 코드를 보자. 현재 만들고 있는 페이지에 iframe으로 네이버 사이트를 삽입한 것이다. style 속성에서 너비를 페이지기준 100%, 높이를 600px로 만들어서 삽입한 것이다. 만약 iframe을 지원하지 않는 브라우저를 사용한다면 대체문자인 "이 브라우저는 iframe을 지원하지 않습니다." 가 출력될 것이다.

