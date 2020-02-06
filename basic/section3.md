# section3

### if

```
//IF문(1)
package main

import "fmt"

func main() {
	//제어문 - IF
	//반드시 Boolean 식으로 검사 -> 1, 0 (자동 형 변환 없음)
	//소괄호 사용 x

	var a int = 20
	b := 30

	//예제1
	if a >= 15 {
		fmt.Println("15 이상")
	}

	//예제2
	if b >= 25 {
		fmt.Println("25 이상")
	}

	//에러 발생1
	/*
		if b >= 25
		{
			fmt.Println("25 이상")
		}
	*/

	//에러 발생2
	/*
		if b >= 25
			fmt.Println("25 이상")
	*/

	//에러 발생3
	/*
		if c := 1; c {
			fmt.Println("True")
		}
	*/

	//예제3 (간단한 문장 : Optional Statement)
	if c := 40; c >= 35 {
		fmt.Println("35 이상")
	}
	//c += 20 //에러 발생
}

```

```
//IF문(2)
package main

import "fmt"

func main() {

	var a int = 50
	b := 70

	//예제1
	if a >= 65 {
		fmt.Println("65 이상")
	} else {
		fmt.Println("65 미만")
	}

	//예제2
	if b >= 70 {
		fmt.Println("70 이상")
	} else {
		fmt.Println("70 미만")
	}

	//에러 발생
	/*
		if a >= 65 {
			fmt.Println("65 이상")
		} else
		{
			fmt.Println("65 미만")
		}
	*/

	//예제3
	if c := 90; c >= 100 {
		fmt.Println("100 이상")
	} else {
		fmt.Println("100 미만")
	}
}

```

```
//IF문(3)
package main

import "fmt"

func main() {

	i := 100

	//if - else if 예제(1)
	if i >= 120 {
		fmt.Println("120 이상")
	} else if i >= 100 && i < 120 {
		fmt.Println("100 이상 120 미만")
	} else if i < 100 && i >= 50 {
		fmt.Println("50 이상 100 미만")
	} else {
		fmt.Println("50 미만")
	}

	//if - else if 예제(2)
	if j := 75; j >= 120 {
		fmt.Println("120 이상")
	} else if j >= 100 && j < 120 {
		fmt.Println("100 이상 120 미만")
	} else if j < 100 && j >= 50 {
		fmt.Println("50 이상 100 미만")
	} else {
		fmt.Println("50 미만")
	}

}

```

### switch
```
//Switch문(1)
package main

import "fmt"

func main() {
	//제어문 - Switch
	//Switch 뒤 표현식(Expression) 생략 가능
	//case 뒤 표현식(Expression) 사용 가능
	//자동 break 때문에 fallthrough 존재
	//Type 분기 -> 값이 아닌 변수 Type 으로 분기 가능

	//예제1
	a := -7
	switch {
	case a < 0:
		fmt.Println(a, "는 음수")
	case a == 0:
		fmt.Println(a, "는 0")
	case a > 0:
		fmt.Println(a, "는 양수")
	}

	//예제2
	switch b := 27; {
	case b < 0:
		fmt.Println(b, "는 음수")
	case b == 0:
		fmt.Println(b, "는 0")
	case b > 0:
		fmt.Println(b, "는 양수")
	}

	//예제3
	switch c := "go"; c {
	case "go":
		fmt.Println("Go!")
	case "java":
		fmt.Println("Java!")
	default:
		fmt.Println("일치하는 값 없음")
	}

	//예제4
	switch c := "go"; c + "lang" {
	case "golang":
		fmt.Println("GoLang!")
	case "java":
		fmt.Println("Java!")
	default:
		fmt.Println("일치하는 값 없음")
	}

	//예제5
	switch i, j := 20, 30; {
	case i < j:
		fmt.Println("i는 j보다 작다")
	case i == j:
		fmt.Println("i와 j는 같다")
	case i > j:
		fmt.Println("i는 j보다 크다")
	}

}
```

```
//Switch문(2)
package main

import "fmt"

func main() {

	//예제1
	a := 30 / 15
	switch a {
	case 2, 4, 6: // i가 2, 4, 6일 때
		fmt.Println("a -> ", a, "짝수")
	case 1, 3, 5: // i가 1, 3, 5일 때
		fmt.Println("a -> ", a, "홀수")
	}

	//예제2
	switch i := 75; {
	case i >= 50 && i < 100:
		fmt.Println("i -> ", i, "50 이상, 100 미만")
	case i >= 0 && i < 05:
		fmt.Println("i -> ", i, "0 이상, 50 미만")
	}

	//예제3
	c := "success"
	d := 2

	switch d {
	case 1:
		fmt.Println(1)
	case 2:
		if c == "success" {
			fmt.Println("Login Success")
			//break //break 필요한 경우
		}
		fmt.Println("Pass")
	}

	//예제4
	switch e := "go"; e {
	case "java":
		fmt.Println("Java")
		fallthrough
	case "go":
		fmt.Println("Go")
		fallthrough
	case "python":
		fmt.Println("Python")
		fallthrough
	case "ruby":
		fmt.Println("Ruby")
		fallthrough
	case "c":
		fmt.Println("C")
		//fallthrough //마지막 라인 fallthrough 사용 불가
	}

}
```

```
//Switch문(3)
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {
	//예제1
	rand.Seed(time.Now().UnixNano())

	switch i := rand.Intn(100); {
	case i >= 50 && i < 100:
		fmt.Println("i -> ", i, " 50 이상 100미만")
	case i >= 25 && i < 50:
		fmt.Println("i -> ", i, " 25 이상 50미만")
	default:
		fmt.Println("i -> ", i, " 기본 값")
	}
}
```
### for

```
//For문(1)
package main

import "fmt"

func main() {
	//반복문 - For
	//Go에서 유일한 반복문
	//다양한 사용법 숙지

	//예제1
	for i := 0; i < 5; i++ {
		fmt.Println("ex1 : ", i)
	}

	//에러 발생1
	/*
		for i := 0; i < 5; i++
		{
			fmt.Println("ex1 : ", i)
		}
	*/

	//에러 발생2
	/*
		for i := 0; i < 5; i++
			fmt.Println("ex1 : ", i)
	*/

	//예제2 (무한 루프)
	/*
		for {
			fmt.Println("ex2 : Hello, Golang!")
			fmt.Println("ex2 : Infinite loop!")
		}
	*/

	//예제3 (Range용법)
	loc := []string{"Seoul", "Busan", "Incheon"}
	for index, name := range loc {
		fmt.Println("ex3 :", index, name)
	}
}

```
```
//For문(2)
package main

import "fmt"

func main() {

	//예제1
	sum1 := 0

	for i := 0; i <= 100; i++ {
		sum1 += i
	}
	fmt.Println("ex1 : ", sum1)

	//예제2
	sum2, i := 0, 0

	for i <= 100 {
		sum2 += i
		i++
		//i := i++ //에러 발생 (후치 연산 반환 값 X)
	}
	fmt.Println("ex2 : ", sum2)

	//예제3
	sum3, i := 0, 0

	for {
		if i > 100 {
			break
		}
		sum3 += i
		i++
	}
	fmt.Println("ex3 : ", sum2)

	//예제4
	for i, j := 0, 0; i <= 10; i, j = i+1, j+10 {
		fmt.Println("ex3 : ", i, j)
	}

	//에러 발생
	/*
		for i, j := 0, 0; i <= 10; i++, j += 10 {
			fmt.Println("ex3 : ", i, j)
		}
	*/
}

```
```
//For문(3)
package main

import "fmt"

func main() {

	//예제1
	sum, i := 0, 0

	for {
		if i > 100 {
			break
		}
		sum += i
		i++
	}
	fmt.Println("ex1 : ", sum)

	//예제2
Loop1:
	//fmt.Println("break Loop") //에러 발생(Loop 레이블 밑에 소스코드)
	for i := 0; i < 5; i++ {
		for j := 0; j < 5; j++ {
			if i == 2 && j == 4 {
				break Loop1
			}
			fmt.Println("ex2 : ", i, j)
		}
	}

	//예제3
	for i := 0; i < 10; i++ {
		if i%2 == 0 {
			continue
		}
		fmt.Println("ex3 : ", i)
	}

	//예제4
Loop2:
	//fmt.Println("continue Loop") //에러 발생(Loop 레이블 밑에 소스코드)
	for i := 0; i < 3; i++ {
		for j := 0; j < 3; j++ {
			if i == 1 && j == 2 {
				continue Loop2
			}
			fmt.Println("ex4 : ", i, j)
		}
	}
}

```

### golang 특징

```
//GO 특징(1)
package main

import "fmt"

func main() {
	//모호하거나 애매한 문법 금지
	//후치 연산자 허용 , 전치 연산자 비허용
	//증감연산 반환 값 없음
	//포인터(Pointer 허용, 연산 비허용)
	//주석 사용법 숙지( //, /**/)

	//예제1
	sum, i := 0, 0

	for i <= 100 {
		//sum += i++ //예외 발생(증감 연산 반환 값)
		sum += i
		i++
		//++i //예외 발생(전위 증감)
	}
	fmt.Println("ex1 : ", sum)

}
```

```
//GO 특징(2)
package main

import "fmt"

func main() {
	//문장 끝 세미콜론(;)주의
	//자동으로 끝에 세미콜론 삽입
	//두 문장을 한 문장에 표현할 경우 명시적으로 세미콜론 사용
	//반복문 및 제어문(if, for) 사용할 경우 주의

	//예제1
	for i := 0; i <= 10; i++ {
		//fmt.Print("ex1 : ");fmt.Println(i)
		fmt.Print("ex1 : ")
		fmt.Println(i)
	}

	//예제2
	/*
		for j := 10; j >= 0; j-- //예외 발생(세미콜론)
		{
			fmt.Print("ex2 : ",j)
		}
	*/

}
```

```
//GO 특징(3)
package main

import "fmt"

func main() {
	//코드 서식 지정
	//한 사람이 코딩 한 것같은 일관성 유지
	//코드 스타일 유지
	//gofmt -h : 사용법
	//gofmt -w : 원본파일에 반영

	//예제1
	for i := 0; i <= 100; i++ {
		fmt.Print("ex1 : ", i)
	}
}
```
