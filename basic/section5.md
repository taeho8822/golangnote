# section5

### Bool
```
//데이터 타입 : Bool(1)
package main

import "fmt"

func main() {
	//Bool
	//조건부 논리 연산자랑 주로 사용 : !, || , &&
	//암묵적 형변환 X : 0, nil -> false 변환 없음

	//예제1
	var b1 bool = true
	var b2 bool = false
	b3 := true
	//b4 := 1

	fmt.Println("ex1 : ", b1)
	fmt.Println("ex1 : ", b2)
	fmt.Println("ex1 : ", b3 == b3)
	fmt.Println("ex1 : ", b1 && b3)
	fmt.Println("ex1 : ", b1 || b2)
	fmt.Println("ex1 : ", !b2)

	/*
		예외 발생
		if b4 {
			fmt.Println("true")
		}
	*/

}

```

```
//데이터 타입 : Bool(2)
package main

import "fmt"

func main() {

	//예제1
	fmt.Println("ex1 : ", true && true)
	fmt.Println("ex1 : ", true && false)
	fmt.Println("ex1 : ", false && false)
	fmt.Println("ex1 : ", true || true)
	fmt.Println("ex1 : ", true || false)
	fmt.Println("ex1 : ", false || false)
	fmt.Println("ex1 : ", !true)
	fmt.Println("ex1 : ", !false)

	//예제2
	num1 := 15
	num2 := 37

	fmt.Println("ex2 : ", num1 < num2)
	fmt.Println("ex2 : ", num1 > num2)
	fmt.Println("ex2 : ", num1 >= num2)
	fmt.Println("ex2 : ", num1 != num2)
	fmt.Println("ex2 : ", num1 <= num2)

}

```

### 숫자(numeric)

```
//데이터 타입 : Numeric(1)
package main

import "fmt"

func main() {
	//데이터 타입 : 숫자형
	//정수, 실수, 복소수
	//32bit, 64bit, unsigned(양수)
	//정수 : 8진수(0), 16진수(0x), 10진수

	var num1 int = 17
	var num2 int = -68
	var num3 int = 0631       // 8진수로 저장
	var num4 int = 0x32fa2c75 // 16진수로 저장

	fmt.Println("ex1 : ", num1)
	fmt.Println("ex1 : ", num2)
	fmt.Println("ex1 : ", num3)
	fmt.Println("ex1 : ", num4)

}

```

```
//데이터 타입 : Numeric(2)
package main

import "fmt"

func main() {
	//데이터 타입 : 숫자형
	//정수형 문자 출력

	//예제1
	//아스키(영문)
	var char1 byte = 72
	var char2 byte = 0110
	var char3 byte = 0x48

	//유니코드(한글)
	var char4 rune = 50556   // 유니코드
	var char5 rune = 0142574 // 44032 (8진수)
	var char6 rune = 0xC57C  // 44032 (16진수)

	fmt.Printf("%c %c %c\n", char1, char2, char3)
	fmt.Printf("%d %d %d\n", char1, char2, char3)
	fmt.Printf("%d %o %x\n", char1, char2, char3)
	fmt.Printf("%c %c %c\n", char4, char5, char6)
	fmt.Printf("%d %d %d\n", char4, char5, char6)
	fmt.Printf("%d %o %x\n", char4, char5, char6)

}

```

```
//데이터 타입 : Numeric(3)
package main

import "fmt"

func main() {
	//데이터 타입 : 숫자형
	//실수형(부동소수점)
	//float32(7자리), float64(15자리)

	//예제1
	// 소수점 사용
	var num1 float32 = 0.14
	var num2 float32 = .75647
	var num3 float32 = 442.0378373
	var num4 float32 = 10.0

	// 지수 표기법
	var num5 float32 = 14e6
	var num6 float64 = .156875E+3
	var num7 float64 = 5.32521e-10

	fmt.Println("ex1 : ", num1)
	fmt.Println("ex1 : ", num2)
	fmt.Println("ex1 : ", num3)
	fmt.Println("ex1 : ", num4-0.1)          //주의1
	fmt.Println("ex1 : ", float32(num4-0.1)) //주의2
	fmt.Println("ex1 : ", float64(num4-0.1)) //주의3 부동소수점 오차 생김
	fmt.Println("ex1 : ", num5)
	fmt.Println("ex1 : ", num6)
	fmt.Println("ex1 : ", num7)

}

```

```
//데이터 타입 : Numeric(4)
package main

import "fmt"

func main() {
	//데이터 타입 : 숫자형
	//복소수 형(complex number)
	//complex64(32bit 실수 + 허수)
	//complex128(64bit 실수 + 허수)

	//예제1
	var num1 complex64 = 5 + 7i
	num2 := 8 + 1i
	num3 := complex(3, 2) //complex128
	var num4 complex128 = 9 + 3i
	num5 := complex64(2 + 3i)

	fmt.Println("ex1 : ", num1)
	fmt.Println("ex1 : ", num2)
	fmt.Println("ex1 : ", num3)
	fmt.Println("ex1 : ", num4)
	fmt.Println("ex1 : ", num5)

	//예제2
	//real() : 실수부 출력
	//imag() : 허수부 출력
	fmt.Println("ex2 : ", num1, real(num1), imag(num1))
	fmt.Println("ex2 : ", num2, real(num2), imag(num2))
	fmt.Println("ex2 : ", num3, real(num3), imag(num3))
	fmt.Println("ex2 : ", num4, real(num4), imag(num4))
	fmt.Println("ex2 : ", num5, real(num5), imag(num5))

}

```

### 숫자 연산자
```
//데이터 타입 : Numeric 연산(1)
package main

import "fmt"
import "math"

func main() {
	//숫자 연산(산술, 비교)
	//타입이 같아야 가능
	//다른 타입끼리는 반드시 형 변환 후 연산
	//형 변환 없을 경우 예외(에러) 발생
	// +, -, *, /, %, >>, <<, &, ^..

	//예제1 : 최대값 확인
	var n1 uint8 = math.MaxUint8
	var n2 uint16 = math.MaxUint16
	var n3 uint32 = math.MaxUint32
	var n4 uint64 = math.MaxUint64

	fmt.Println("ex1 : ", n1)
	fmt.Println("ex1 : ", n2)
	fmt.Println("ex1 : ", n3)
	fmt.Println("ex1 : ", n4)
	fmt.Println("ex1 : ", math.MaxInt8)
	fmt.Println("ex1 : ", math.MaxInt16)
	fmt.Println("ex1 : ", math.MaxInt32)
	fmt.Println("ex1 : ", math.MaxInt64)
	fmt.Println("ex1 : ", math.MinInt8)
	fmt.Println("ex1 : ", math.MinInt16)
	fmt.Println("ex1 : ", math.MinInt32)
	fmt.Println("ex1 : ", math.MinInt64)
	fmt.Println("ex1 : ", math.MaxFloat32)
	fmt.Println("ex1 : ", math.MaxFloat64)

	//예제2 (형 변환)
	n5 := 100000 //int
	n6 := int16(10000)
	n7 := uint8(100)

	//fmt.Println("ex2 : ", n5+n6) //예외 발생(컴파일 에러)
	//fmt.Println("ex2 : ", n6+n7) //예외 발생(컴파일 에러)
	fmt.Println("ex2 : ", n5+int(n6))
	fmt.Println("ex2 : ", n6+int16(n7))
	fmt.Println("ex2 : ", n6 > int16(n7))
	fmt.Println("ex2 : ", n6-int16(n7) > 5000)
}

```

```
//데이터 타입 : Numeric 연산(2)
package main

import "fmt"

func main() {

	//예제1
	var n1 uint8 = 125
	var n2 uint8 = 90

	fmt.Println("ex1 : ", n1+n2)
	fmt.Println("ex1 : ", n1-n2)
	fmt.Println("ex1 : ", n1*n2)
	fmt.Println("ex1 : ", n1/n2)
	fmt.Println("ex1 : ", n1%n2)
	fmt.Println("ex1 : ", n1<<2)
	fmt.Println("ex1 : ", n1>>2)
	fmt.Println("ex1 : ", ^n1)

	//예제2
	var n3 int = 12
	var n4 float32 = 8.2
	var n5 uint16 = 1024
	var n6 uint32 = 120000

	//fmt.Println(n3 + n4)          //예외 발생(컴파일 에러)
	fmt.Println(float32(n3) + n4) //형 변환 후 계산
	fmt.Println(n3 + int(n4))     //소수 부분 값 손실
	fmt.Println(n5 + uint16(n6))  //형 변환에 의한 값 손실
}

```

```
//데이터 타입 : Numeric 연산(3)
package main

//import "math"

func main() {

	//예제1(오버플로우 에러 : 범위 초과)
//	var n1 uint8 = math.MaxUint8 + 1
//	var n2 uint16 = math.MaxUint16 + 1
//	var n3 uint32 = math.MaxUint32 + 1
//	var n4 uint64 = math.MaxUint64 + 1

	//예제2(오버플로우 에러 : 범위 미만)
//	var n1 uint8 = -1
//	var n2 uint16 = -1
//	var n3 uint32 = -1
//	var n4 uint64 = -1
}

```

### 문자열 (string)
```
//데이터 타입 : 문자열(1)
package main

import "fmt"
import "unicode/utf8"

func main() {
	//문자열
	//큰따옴표 "" , 백스쿼트 `` 작성
	//Golang : 문자 char 타입 존재하지 않음 -> rune(int32)로 문자 코드 값으로 표현
	//문자 : 작은따옴표 '' 로 작성
	//자주 사용 하는 escape : \\, \', \", \a(콘솔벨), \b(백스페이스), \f(쪽바꿈), \n(줄바꿈), \r(복귀), \t(탭)

	//예제1
	var str1 string = "c:\\go_study\\src\\"
	str2 := `c:\go_study\src\`

	fmt.Println("ex1 : ", str1, "\t", "ok1")
	fmt.Println("ex1 : ", str2, "\t", "ok2")

	//예제2
	var str3 string = "Hello, world!"
	var str4 string = "안녕하세요"
	var str5 string = "\ud55c\uae00"             // 한글 유니코드(4자리는 소문자 -> u)
	var str6 string = "\U0000d55c\U0000ae00"     // 한글 유니코드(8자리는 소문자 -> U)
	var str7 string = "\xed\x95\x9c\xea\xb8\x80" // UTF-8 인코딩 바이트 코드

	fmt.Println()
	fmt.Println("ex2 : ", str3)
	fmt.Println("ex2 : ", str4)
	fmt.Println("ex2 : ", str5)
	fmt.Println("ex2 : ", str6)
	fmt.Println("ex2 : ", str7)
	fmt.Println()

	//예제3
	//길이(바이트수)
	fmt.Println("ex3 : ", len(str3))
	fmt.Println("ex3 : ", len(str4))
	fmt.Println()

	//예제4
	//길이(실제 길이)
	fmt.Println("ex4 : ", utf8.RuneCountInString(str3))
	fmt.Println("ex4 : ", utf8.RuneCountInString(str4))
	fmt.Println("ex4 : ", len([]rune(str4)))
}

```

```
//데이터 타입 : 문자열(2)
package main

import "fmt"

func main() {
	//문자열 표현
	//문자열 : UTF-8 인코딩 (유니코드 문자 집합) -> 바이트 수 주의

	//예제1
	var str1 string = "Golang"
	var str2 string = "World"
	var str3 string = "고프로그래밍"

	fmt.Println("ex1 : ", str1[0], str1[1], str1[2], str1[3], str1[4], str1[5])
	fmt.Println("ex1 : ", str2[0], str2[1], str2[2], str2[3], str2[4])
	fmt.Println("ex1 : ", str3[0], str3[1], str3[2], str3[3], str3[4], str3[5])
	fmt.Println("ex1 : ", str3[0], str3[1], str3[2], str3[3], str2[4], str3[5], str3[len(str1)-2])

	//예제2
	fmt.Printf("ex2 : %c %c %c %c %c %c\n", str1[0], str1[1], str1[2], str1[3], str1[4], str1[5])
	fmt.Printf("ex2 : %c %c %c %c %c\n", str2[0], str2[1], str2[2], str2[3], str2[4])
	fmt.Printf("ex2 : %c %c %c %c %c %c\n", str3[0], str3[1], str3[2], str3[3], str3[4], str3[5]) //문제 발생

	conStr := []rune(str3)
	fmt.Printf("ex2 : %c %c %c %c %c %c\n", conStr[0], conStr[1], conStr[2], conStr[3], conStr[4], conStr[5])

	//예제3
	for i, char := range str1 {
		fmt.Printf("ex3 : %c(%d)\t", char, i)
	}

	fmt.Println()

	for i, char := range str2 {
		fmt.Printf("ex3 : %c(%d)\t", char, i)
	}

}

```

### string 연산

```
//데이터 타입 : 문자열 연산(1)
package main

import (
	"fmt"
	"strings"
)

func main() {
	//문자열 연산
	//추출, 비교, 조합(결합)

	//예제1(추출)
	var str1 string = "Golang"
	var str2 string = "World"

	fmt.Println("ex1 : ", strings.Index(str2,"ld"))
	fmt.Println("ex1 : ", str1[0:2], str1[0])
	fmt.Println("ex1 : ", str2[3:], str2[0])
	fmt.Println("ex1 : ", str2[:4], str2[0])
	fmt.Println("ex1 : ", str1[1:3])
}

```

```
//데이터 타입 : 문자열 연산(2)
package main

import "fmt"

func main() {

	//예제1(비교)
	str1 := "Golang"
	str2 := "World"

	fmt.Println("ex1 : ", str1 == str2) //바이트로 비교
	fmt.Println("ex1 : ", str1 != str2)
	fmt.Println("ex1 : ", str1 > str2)
	fmt.Println("ex1 : ", str1 < str2)

}

```

```
//데이터 타입 : 문자열 연산(3)
package main

import (
	"fmt"
	"strings"
)

func main() {
	//문자열 조합은 한 번 생성 후 수정 불가 이유로 새로 계속해서 생성 된다.
	//효율적 사용을 위해서 되도록 join 함수 사용 추천

	//예제1(결합 : 일반연산)
	str1 := "Go is expressive, concise, clean, and efficient. Its concurrency mechanisms make it easy to " +
		"write programs that get the most out of multicore and networked machines, while its novel " +
		"type system enables flexible and modular program construction. Go compiles quickly to machine " +
		"code yet has the convenience of garbage collection and the power of run-time reflection."
	str2 := "It's a fast, statically typed, compiled language that feels like a dynamically typed, interpreted language."

	fmt.Println("ex1 : ", str1+str2)

	//예제2(결합 : Join)
	strSet := []string{} //슬라이스 선언
	strSet = append(strSet, str1)
	strSet = append(strSet, str2)
	fmt.Println("ex2 : ", strings.Join(strSet, ""))

}

```

