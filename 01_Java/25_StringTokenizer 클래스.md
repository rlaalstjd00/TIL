## StringTokenizer 클래스

StringTokenizer 클래스는 긴 문자열을 지정된 구분자를 기준으로 토큰이라는 여러개의 문자열로 잘라내는데 사용된다.

#### StringTokenizer의 메서드

|           생성자/메서드            |                             설명                             |
| :--------------------------------: | :----------------------------------------------------------: |
|     StringTokenizer(str,delim)     | 문자열(str)을 구분자(delim)으로 나누는  StringTokenizer를 생성한다. (구분자는 토큰으로 취급하지 않음) |
| StringTokenizer(str,delim,boolean) | 위와 같지만, boolean 부분의 값을 true로 하면 구분자도 토큰으로 간주한다. |
|           countTokens()            |                  전체 토큰의 수를 반환한다.                  |
|          hasMoreTokens()           |                 토큰이 남아있는지 알려준다.                  |
|            nextToken()             |                    다음 토큰을 반환한다.                     |

````java
String str = "11,12,13,14";
StringTokenizer st = new StringTokenizer(str, ",");
StringTokenizer st2 = new StringTokenizer(str, ",", true);

System.out.println(st.countTokens());	// 4
System.out.println(st2.countTokens());	// 7

while(st.hasMoreTokens()){
    System.out.println(st.nextToken());
    /*
    	11
    	12
    	13
    	14
    */
}

````



> #### StringTokenizer vs split()
>
> 둘다 문자열을 구분자로 잘라내는 역할을 하는데 어떤 점이 다를까?
>
> - `split()` 은 구분자로 정규식 표현을 사용한다.
> - StringTokenizer 는 구분자로 단 하나의 문자를 사용한다.
> - 따라서 성능면에서는 StringTokenizer가 더 우월하지만, 복잡한 형태의 구분자로 문자열을 나누어야 할 때는 `split()` 을 사용하는 것이 적합할 것이다.
>
> ````java
> String str = "1aA2bB3cC";
> String[] results = str.split("[0-9]");
> for(int i=0; i<results.length; i++){
>     System.out.println("results["+i+"] = " + result[i]);
> }
> 
> /*
> 	results[0] = 
> 	results[1] = aA
> 	results[2] = bB
> 	results[3] = cC
> */
> ````
>
> > 위의 코드는`split()` 을 이용해서 문자열 을 숫자 하나를 기준으로 자르는 코드이다.
> >
> > 따라서 주어진 문자열에서 숫자인 1, 2, 3을 기준으로 잘려 aA, bB, cC가 남는 것이다.
> >
> > 이렇게 구분자가 가변적일 때는 `split()` 과 정규식을 이용해서 처리해야 한다.

