# section2

### 상수 (const)

```
//상수1
package main

import "fmt"

func main() {
	//상수
	//const 사용 초기화, 한 번 선언 후 값 변경 금지 , 고정 된 값 관리 용

	const a string = "test1"
	const b = "test2"
	const c int32 = 10 * 10
	//const d = getHeight()
	const e = 35.6
	const f = false
	/*
		에러 발생
		const g string
		g = "test3"
	*/

	fmt.Println("a : ", a, "b : ", b, "c : ", c, "e : ", e, "f : ", f)
}
```

```
//상수2
package main

import "fmt"

func main() {

	const a, b int = 10, 99
	const c, d, e = true, 0.84, "test"
	const (
		x, y int16 = 50, 90
		i, k       = "Data", 7776
	)

	fmt.Println("a : ", a, "b : ", b, "c : ", c, "e : ", e)
	fmt.Println("x : ", x, "y : ", y, "i : ", i, "k : ", k)
}
```

### 변수 (variable1)
```
//변수1
package main

import "fmt"

func main() {
	//기본 초기화
	//정수타입 : 0, 실수(소수점) : 0.0, 문자열 : "", Boolean : False
	//변수명 : 숫자 첫글자X, 대소문자 구분, 문자 숫자 밑줄 특수기호 사용 가능
	//변수 및 상수 : 함수 내외에서 사용 가능
	var a int
	var b string
	var c, d, e int
	var f, g, h int = 1, 2, 3
	var i float32 = 11.4
	var j string = "Hi Golang!"
	var k = 4.75 //선언 동시 초기화
	var l = "Hi Seoul!"
	var m = true

	a = 4
	b = "Helloworld"
	e = 4

	fmt.Println("a : ", a)
	fmt.Println("b : ", b)
	fmt.Println("c : ", c, "d : ", d, "e : ", e)
	fmt.Println("f : ", f, "g : ", g, "h : ", h)
	fmt.Println("i : ", i)
	fmt.Println("j : ", j)
	fmt.Println("k : ", k)
	fmt.Println("l : ", l)
	fmt.Println("m : ", m)
}
```

```
//변수2
package main

import "fmt"

func main() {
	//여러 개 선언
	var (
		name      string = "machine"
		height    int32
		weight    float32
		isRunning bool
	)

	height = 250
	weight = 350.56
	isRunning = true

	fmt.Println("name : ", name, "height : ", height, "weight : ", weight, "isRunning : ", isRunning)
}
```

```
//변수2
package main

import "fmt"

func main() {
	//짧은 선언 : 선언과 동시에 초기화
	//함수 안에서만 사용 가능(전역x) , 선언 후 할당 예외 발생
	//주로 제한된 범위의 함수내에서 사용 할 경우 코드 가독성을 높일 수 있다. -> 추천
	shortVar1 := 3
	shortVar2 := "Test"
	shortVar3 := false

	//shortVar3 := true // 에러 발생

	fmt.Println("shortVar1 : ", shortVar1, "shortVar2 : ", shortVar2, "shortVar3 : ", shortVar3)

	//Example
	if i := 10; i < 11 {
		fmt.Println("Short Variable Test Success!")
	}
}
```

### 열거형 (enumeration)

```
//열거형1
package main

import "fmt"

func main() {
	//열거형
	//상수를 사용하는 일정한 규칙에 따라 숫자를 증가시키는 묶음
	const (
		Jan = 1
		Feb = 2
		Mar = 3
		Apr = 4
		May = 5
		Jun = 6
	)
	fmt.Println("Jan : ", Jan)
	fmt.Println("Feb : ", Feb)
	fmt.Println("Mar : ", Mar)
	fmt.Println("Apr : ", Apr)
	fmt.Println("May : ", May)
	fmt.Println("Jun : ", Jun)
}
```

```
//열거형2
package main

import "fmt"

func main() {
	//열거형
	//상수를 사용하는 일정한 규칙에 따라 숫자를 증가시키는 묶음

	const (
		A = iota
		B
		C
	)

	const (
		Jan = iota + 1 //계산 식 가능
		Feb
		Mar
		Apr
		May
		Jun
	)

	fmt.Println("A : ", A)
	fmt.Println("B : ", B)
	fmt.Println("C : ", C)

	fmt.Println("Jan : ", Jan)
	fmt.Println("Feb : ", Feb)
	fmt.Println("Mar : ", Mar)
	fmt.Println("Apr : ", Apr)
	fmt.Println("May : ", May)
	fmt.Println("Jun : ", Jun)
}
```
```
//열거형3
package main

import "fmt"

func main() {
	//열거형
	//상수를 사용하는 일정한 규칙에 따라 숫자를 증가시키는 묶음

	const (
		_ = iota
		A
		B
		C
	)

	const (
		_ = iota + 0.75*2
		DEFAULT
		SILVER
		GOLD
		PLATINUM
	)

	fmt.Println("A : ", A)
	fmt.Println("B : ", B)
	fmt.Println("C : ", C)

	fmt.Println("DEFAULT : ", DEFAULT)
	fmt.Println("SILVER : ", SILVER)
	fmt.Println("GOLD : ", GOLD)
	fmt.Println("PLATINUM : ", PLATINUM)

}

```

