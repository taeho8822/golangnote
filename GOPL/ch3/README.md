# GOPL CH3  

### 3.4 Bool
true, false 값을 가진다
다른 언어와 달리 0,1 사용불가
== 또는 < 같은 비교연산자는 불리언 결과를 생성한다.
권장사항 x == true 와 같은 중복된표현 지양해야 한다. x로 간소화
	
### 3.5 문자열 (stirg)  
텍스트를 담고있는 데이터  
불변의 바이트 시퀀스  
len(문자열) : 문자 갯수가 아닌  바이트 길이 한글(3byte)  
문자열[i:j] : i째 인덱스에서 j번째 인덱까지 일부 바이트를 담는 새 문자열 생성  
  
### 3.5.1 문열 리터럴  
큰따옴표 사용가능 "Hllo, 世"  
이스케이프 
```
  \a: "alert r bell  
  \b: backspae  
  \f: form feed  
  \n: newline  
  \r: carriage return  
  \t: tab  
	\v: vertical tab  
	\': single qute(only in the rune literal '\'')  
	\": double quo (only within "..." literals)  
	\\: backslash  
	- 16진 이스케이프 /xhh  
	- 8진 이스케이프 000  
	- 백쿼트(`) 사 이스케이프 가능  
 ```
### 3.5.2 유니코드
US-ASCII 
전세계 필기 시스템의 문자를 수집  
Go애서 룬(rune) 이라 부르는 표준 숫자를 붙인 유니코드이다  

### 3.5.3 UT-8
유니 코드  코드 포인트를 바이트 단위 가변 길이 인코딩이다
1~4바이트
```
	0xxxxxx	룬 0-127	(ASCII)
	11xxxxx 10xxxxxx	128-2047	(값 <128 미사용)
	110xxxx 10xxxxxx 10xxxxxx	2048−655	(값 <2048 미사용)
	1110xxx 10xxxxxx 10xxxxxx 10xxxxx 65536−0x10ffff	(다른 값은 사용하지 않음)
	\uhhh 16비트값 , Uhhhhhhhh 32비트값
```
문자 길이
```
	unicode/utf8 패키지
	utf8.RuneCountnString(문자열)
	len([]rune(문자열))
```
### 3.5.4 문자열과 바트 슬라이스

문자열조작 주요 표준패키지   
bytes, strings, strconv, unicode   
bytes 패키지 []byte 타입의 이트 슬이스를 조작  
문자열은 불변이기 때문에 점진적인 문열 구축는 다수의 할당 및 복사 연산이 필요  
bytes.Buffer 타입을 사용하것 효율적  
  
### 3.5.5 문자열과 숫자 사이의 변환
정수를 문자열로 변환 2가지 방법
```
  fmt.Sprintf
	strconv.Itoa("integer to ASCII")
```
```
x := 123
y := fmt.Sprintf("%d", x)
fmt.Println(y, strconv.Itoa(x)) // "123 123"
```
FormatInt그리고 FormatUint다른 기본에 숫자를 포맷 할 수 있다
```
fmt.Println(strconv.FormatInt(int64(x), 2)) // "1111011"
```

```
x, err := strconv.Atoi("123") // x is an int
y, err := strconv.ParseInt("123", 10, 64) // base 10, up to 64 bits
```
