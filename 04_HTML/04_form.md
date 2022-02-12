#### form 태그

웹 페이지 내에서 사용자로부터 입력을 받은 후 데이터를 모아서 다른 페이지로 전송할 때 사용하는 태그.

`<form action="데이터를 전송할 위치" method="전송방식(get/post)"> </form>` 같은 형식으로 쓰인다.

- form 태그에 사용가능한 속성

  1. `action` : form 데이터를 전송할 위치를 지정
  2. `name` : 폼을 식별하기 위한 이름을 지정
  3. `accept-charset` : 폼 전송에 사용할 문자 인코딩 지정
  4. `target` : action에서 지정한 파일을 현재 창이 아닌 다른 위치에 열도록 지정
  5.  `method` : 폼을 서버에 전송할 방식을 지정 (get / post)
     - `get` : 폼 데이터를 URL 끝에 붙여서 눈에 보이게 보냄. 데이터가 외부에 노출되어 보안에 취약함
     - `post` : 폼 데이터를 내부적으로 보이지 않게 보냄.


#### input 태그

사용자에게 입력받기 위해 사용하는 태그.

`<input type="" size="" placeholder="" name="" value="">` 같은 형식으로 쓰인다.

- input 태그에 사용가능한 속성

  1. `maxlength` : 값의 최대 길이
  2. `size` : 글상자의 크기 ( 값의 길이와 상관 없음 )
  3. `placeholder` : 사용자에게 어떤 값을 입력해야 하는지 유도, 안내해주는 문자열값
  4. `readonly` : 읽기전용, 수정 불가능
  5. `value` : 실제값
  6. `name` : 해당 입력의 이름 ( 데이터를 처리하는 쪽에서 식별자 역할을 한다. )
  7. `required` : 필수 항목
  8. `type`

  -  type 속성
    1. `text` : 텍스트 입력
    2. `password` : 비밀번호 입력
    3. `radio` : 동그란 버튼 ( 중복으로 체크 불가능하며 name이 같은것들 끼리 세트 )
    4. `checkbox` : 네모난 버튼 ( 중복으로 체크 가능 )
    5. `file` : 파일 첨부 퍼튼 ( form에 enctype 속성을 적어줘야한다. / enctype = "multipart/form-data")
    6. `color` : 원하는 색상 선택
    7. `email` : 이메일 입력 (@ 포함)
    8. `url` : http://, https:// 포함해서 입력
    9. `tel` : 휴대폰번호
    10. `date` : 날짜
    11. `number` : 숫자 크기를 조절하는 상하버튼이 있는 입력
    12. `range` : 일정 범위 안의 값만 입력
    13. `search` : 검색어 입력 (입력시 지울 수 있는 x 버튼이 오른쪽 끝에 생김)
    14. `button` : 버튼
    15. `submit` : 제출버튼 ( form의 모든 데이터들을 전송하며 입력 마무리 )
    16. `reset` : 리셋버튼

````html
<body>
	<form action="a.html" method="post">
        <p>
            아이디<input type="text" size="100" name="userid" maxlength="12" value="apple" readonly>
        </p>
        <p>
            비밀번호<input type="password" placeholder="비밀번호를 입력하세요" name="userpw" required>
        </p>
        <p>
            성별<br>
            <!-- usergender 라는 이름으로 체크된것의 value값이 전송됨 -->
            <input type="radio" name="usergender" value="남">남 /
            <input type="radio" name="usergender" value="여"> 여
        </p>
        <p>
            취미<br>
            <input type="checkbox" value="영화보기" name="userhobby">영화보기 /
            <input type="checkbox" value="음악감상" name="userhobby">음악감상 /
            <input type="checkbox" value="게임하기" name="userhobby">게임하기
        </p>
        <p>
            <!-- 버튼의 value 속성값은 버튼에 써질 문자열이다 -->
            제출하기<input type="submit" value="회원가입">
            초기화<input type="reset" value="모두 지우기">
        </p>
    </form>
</body>
````

