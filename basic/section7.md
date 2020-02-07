# section7

### 함수(function)

```
//함수 기초(1)
package main

import "fmt"
import "strconv"

//함수 선언 위치는 어느 곳이든 가능
func helloGolang() {
	fmt.Println("ex1 : Hello Golang!")
}

/*
func helloGolang() //예외 발생(괄호 위치 컴파일 에러)
{
	fmt.Println("Hello Golang!")
}
*/

func say_one(m string) {
	fmt.Println("ex2 :", m)
}

func sum(x int, y int) int {
	return x + y
}

func main() {
	//함수
	//선언 : func 키워드로 선언
	//func 함수명(매개변수) (반환타입 or 반환 값 변수명) : 반환 값 존재
	//func 함수명() (반환타입 or 반환 값 변수명) : 매개변수 없음, 반환 값 존재
	//func 함수명(매개변수) : 매개변수 존재, 반환 값 없음
	//타 언어와 달리 반환 값(return value) 여러 개 가능

	//예제1
	helloGolang()

	//예제2
	say_one("Hello World!")

	//예제3
	result := sum(5, 5)
	fmt.Println("ex3 :", result)
	fmt.Println("ex3 :", sum(10, 10))
	fmt.Println("ex3 :", strconv.Itoa(sum(10, 10))) //int to string (strconv.Atoi(int) : string to int)
	
}

```

```
//함수 기초(2)
package main

import "fmt"

func sum(i int, f func(int, int)) {
	f(i, 10) // add(1, 2)를 호출
}

func add(a, b int) {
	fmt.Println("ex1 :", a+b)
}

func multi_value(i int) {
	i = i * 10
}

func multi_reference(i *int) {
	*i *= 10 // *i = *i * 10
}

func main() {
	//함수(콜백) 및 참조 전달(call by reference) 및 값 전달(call by value)

	//예제1 (콜백 호출)
	sum(10, add) //함수 전달

	//예제2
	//call by value
	a := 100

	multi_value(a)
	fmt.Println("ex2 :", a)

	//예제3
	//reference by value
	b := 100

	multi_reference(&b)
	fmt.Println("ex3 :", b)

}

```
```
//함수 기초(3)
package main

import "fmt"

func multiply(x int, y int) (int, int) { //(x, y int)가능
	return x * 10, y * 15
}

func arrayMultiply(a, b, c, d, e int) (int, int, int, int, int) {
	return a * 1, b * 2, c * 3, d * 4, e * 5
}

func main() {
	//다중 값 반환(return values)

	//예제1
	a, b := multiply(10, 5)
	//c := multiply(5, 10) //예외 발생(리턴 값 개수 != 선언 변수 개수)
	c, _ := multiply(10, 5)
	_, d := multiply(5, 10)

	fmt.Println("ex1 : ", a, b)
	fmt.Println("ex1 : ", c)
	fmt.Println("ex1 : ", d)

	//예제2
	x1, x2, x3, x4, x5 := arrayMultiply(1, 2, 3, 4, 5)
	y1, _, y3, _, y5 := arrayMultiply(1, 2, 3, 4, 5)
	fmt.Println("ex2 : ", x1, x2, x3, x4, x5)
	fmt.Println("ex2 : ", y1, y3, y5)

}


```

```
//함수 기초(4)
package main

import "fmt"

func multiply(x int, y int) (r1 int, r2 int) {
	r1 = x * 10
	r2 = y * 20
	return //리턴 변수 지정
}

func multiply2(x int, y int) (int, int) {
	return x * 10, y * 20
}

func main() {
	//다중 값 반환(return values)

	//예제1
	a, b := multiply(10, 5)
	fmt.Println("ex1 : ", a, b)

	//예제2
	c, d := multiply2(10, 5)
	fmt.Println("ex2 : ", c, d)
}

```

```
//함수 심화(1)
package main

import "fmt"

func multiply(n ...int) int {
	tot := 1
	for _, value := range n {
		tot *= value
	}

	return tot
}

func sum(n ...int) int {
	tot := 0
	for _, value := range n {
		tot += value
	}

	return tot
}

func prtWord(msg ...string) {
	for _, value := range msg {
		fmt.Println("ex2 :", value)
	}
}

func main() {
	//함수 고급
	//가변 인자 실습(매개변수 개수가 동적으로 변할 때 - 정해져있지 않음)

	//예제1
	x := multiply(5, 6, 7, 8, 9, 10)
	y := sum(5, 6, 7, 8, 9, 10)
	fmt.Println("ex1 :", x)
	fmt.Println("ex1 :", y)
	fmt.Println()

	//예제2
	prtWord("a", "apple", "test", "seoul", "golang", "hi")
	fmt.Println()

	//예제3
	a := []int{5, 6, 7, 8, 9, 10}

	m := multiply(a...)
	n := sum(a...)

	fmt.Println("ex3 :", m)
	fmt.Println("ex3 :", n)
}

```

```
//함수 심화(2)
package main

import "fmt"

func multiply(x, y int) (r int) {
	r = x * y
	return
}

func sum(x, y int) (r int) {
	r = x + y
	return
}

func main() {
	//함수 고급
	//함수를 변수에 할당

	//예제1 (슬라이스에 할당)
	f := []func(int, int) int{multiply, sum}

	a := f[0](10, 10)
	b := f[1](10, 10)

	fmt.Println("ex1 :", a, f[0](10, 10))
	fmt.Println("ex1 :", b, f[1](10, 10))
	fmt.Println()

	//예제2 (변수에 할당)
	var f1 func(int, int) int = multiply
	f2 := sum

	fmt.Println("ex2 :", f1(10, 10))
	fmt.Println("ex2 :", f2(10, 10))
	fmt.Println()

	//예제3 (맵에 할당)
	m := map[string]func(int, int) int{
		"multiply": multiply,
		"sum":      sum,
	}
	fmt.Println("ex3 :", m["multiply"](10, 10))
	fmt.Println("ex3 :", m["sum"](10, 10))
}

```

```
//함수 심화(3)
package main

import "fmt"

func fact(n int) int {
	if n == 0 {
		return 1
	}
	return n * fact(n-1)
}

func prtHello(n int) {
	if n == 0 {
		return
	}
	fmt.Println("ex2 : (", n, ")", "hi!")
	prtHello(n - 1)
}

func main() {
	//함수 고급
	//재귀 함수(Recursion)

	//예제1
	x := fact(7)
	fmt.Println("ex1 :", x)

	//예제2
	prtHello(10)
}

```

```
//함수 심화(4)
package main

import "fmt"

func main() {
	//함수 고급
	//익명 함수(Anonymous Functions)

	//예제1
	func() {
		fmt.Println("ex1 : Anonymous func!")
	}()

	fmt.Println()

	//예제2
	msg := "Hello Golang!"

	func(m string) {
		fmt.Println("ex2 : ", m)
	}(msg)

	fmt.Println()

	//예제3
	func(x, y int) {
		fmt.Println("ex3 : ", x+y)
	}(10, 20)

	fmt.Println()

	//예제4
	r := func(x, y int) int {
		return x * y
	}(10, 10)
	fmt.Println("ex4 : ", r)
}

```

### Closure

```
//함수 Closure(1)
package main

import "fmt"

func main() {
	//클로저(Closure)
	//익명함수 사용할 경우 함수를 변수에 할당해서 사용가능
	//이 때, 함수는 일급 객체 이므로 변수의 값으로 사용 가능
	//현재 범위에 있는 변수의 값을 캡처 후 호출 할 때 변수 사용 가능(선언 시점 기준)

	//예제1
	multiply := func(x, y int) int { //익명함수 변수 할당
		return x * y
	}

	r1 := multiply(5, 10)

	fmt.Println("ex1 : ", r1)

	//예제2
	m, n := 10, 5            //변수를 캡처
	sum := func(c int) int { //익명함수 변수 할당
		return m + n + c //지역 변수 소멸되지 않는다.(함수 호출 시 마다 사용 가능)
	}

	r2 := sum(10)

	fmt.Println("ex2 : ", r2)

}
```

```
//함수 Closure(2)
package main

import "fmt"

func main() {

	//예제1
	cnt := increaseCnt()

	fmt.Println("ex1 : ", cnt())
	fmt.Println("ex1 : ", cnt())
	fmt.Println("ex1 : ", cnt())
	fmt.Println("ex1 : ", cnt())
	fmt.Println("ex1 : ", cnt())

}

func increaseCnt() func() int {
	n := 0 //지역변수(캡처됨)
	return func() int {
		n += 1
		return n
	}
}

```

### Defer

```
//함수 Defer(1)
package main

import "fmt"

func ex_f1() {
	fmt.Println("f1 : start")
	defer ex_f2() //마지막에 호출
	fmt.Println("f1 : end")
}

func ex_f2() {
	fmt.Println("f2 : called")
}

func main() {
	//Defer 함수 실행(지연)
	//Defer를 호출한 함수가 종료되기 직전에 호출 된다.
	//타 언어의 Finally 문과 비슷
	//주로 리소스 반환 등에 사용

	//예제1
	ex_f1()
}

```
```
//함수 Defer(2)
package main

import "fmt"

func sayHello(msg string) {
	defer func() {
		fmt.Println(msg)
	}()

	func() {
		fmt.Println("Hi ")
	}()
}

func main() {

	//예제1
	sayHello("Golang!")
}

```

```
//함수 Defer(3)
package main

import "fmt"

func stack() {
	for i := 1; i <= 10; i++ {
		defer fmt.Println("ex1 : ", i)
	}
}

func main() {

	//예제1
	stack()
}

```

```
//함수 Defer(4)
package main

import "fmt"

func start(t string) string {
	fmt.Println("start:", t)
	return t
}
func end(t string) {
	fmt.Println("end:", t)
}

func a() {
	defer end(start("b"))
	fmt.Println("in a")
}

func main() {

	//예제1
	a()
}

```
