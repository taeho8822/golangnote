# section8-2

### 인터페이스(interface)

```
//인터페이스 기본(1)
package main

import "fmt"

type test interface{} //빈 인터페이스

func main() {
	//인터페이스
	//객체의 동작을 표현, 골격
	//단순히 동작에 대한 방법만 표시
	//추상화 제공
	//인터페이스의 메소드를 구현한 타입은 인터페이스로 사용 가능
	//Go언어를 유연하게 사용 가능
	//덕타이핑 : Go 언어의 독창적인 특성

	/*
	  type 인터페이스명 interface {
	     메서드1() 반환 값(타입형)
	  	 메서드2() //반환 값 없을 경우
	   }
	*/

	//예제1
	var t test
	fmt.Println("ex1 : ", t) //Empty 인터페이스인 경우 nil 리턴
}

```

```
//인터페이스 기본(2)
package main

import "fmt"

type Dog struct {
	name   string
	weight int
}

//bite 메소드 구현
func (d Dog) bite() {
	fmt.Println(d.name, " bites!")
}

//동물의 행동 인터페이스 선언
type Behavior interface {
	bite()
}

func main() {
	//인터페이스 구현 예제

	//예제1
	dog1 := Dog{"poll", 10}
	var inter1 Behavior
	inter1 = dog1
	inter1.bite() //인터페이스 -> Dog의 bite 메소드 실행

	//예제2
	dog2 := Dog{"mary", 12}
	inter2 := Behavior(dog2) //인터페이스 선언 및 초기화
	inter2.bite()

	//예제3
	inters := []Behavior{dog1, dog2} //슬라이스 타입 인터페이스 선언

	//인덱스 형태로 실행
	for idx, _ := range inters {
		inters[idx].bite()
	}

	//값 형태로 실행
	for _, val := range inters {
		val.bite()
	}

}

```

```
//인터페이스 기본(3)
package main

import "fmt"

type Dog struct {
	name   string
	weight int
}

type Cat struct {
	name   string
	weight int
}

//구조체 Dog 메소드 구현
func (d Dog) bite() {
	fmt.Println("Dog bites!")
}

func (d Dog) sounds() {
	fmt.Println("Dog barks!")
}

func (d Dog) run() {
	fmt.Println("Dog is running!")
}

//구조체 Cat 메소드 구현
func (c Cat) bite() {
	fmt.Println("Cat bites!")
}

func (c Cat) sounds() {
	fmt.Println("Cat cries!")
}

func (c Cat) run() {
	fmt.Println("Cat is running!")
}

//인터페이스를 파라미터로 받는다.
func act(animal Behavior) {
	animal.bite()
	animal.sounds()
	animal.run()
}

//동물의 행동 인터페이스 선언
type Behavior interface {
	bite()
	sounds()
	run()
}

func main() {
	//인터페이스 구현 예제
	//인터페이스 규격화 역할 이해
	//인터페이스에 정의된 메소드 사용 유도
	//코드의 가독성 및 유지보수 증가

	//덕타이핑 예제
	//덕타이핑 : 구조체 및 변수의 값이나 타입은 상관하지 않고 오로지 구현된 메소드로만 판단하는 방식
	//Go의 중요한 특징 : 오리처럼 걷고, 소리내고, 헤엄 등 행동이 같으면 오리라고 볼 수 있다 -> 의미

	//예제1
	dog := Dog{"poll", 10}
	cat := Cat{"bob", 5}

	//개 행동 실행
	act(dog)
	//고양이 행동 실행
	act(cat)

}

```

```
//인터페이스 기본(4)
package main

import "fmt"

type Dog struct {
	name   string
	weight int
}

type Cat struct {
	name   string
	weight int
}

func (d Dog) run() {
	fmt.Println(d.name, "Dog is running!")
}

func (c Cat) run() {
	fmt.Println(c.name, "Cat is running!")
}

//익명 인터페이스(타입 정의x)
func act(animal interface{ run() }) {
	animal.run()
}

func main() {
	//익명 인터페이스 사용 예제(즉시 선언 후 사용)

	//예제1
	dog := Dog{"poll", 10}
	cat := Cat{"bob", 5}

	//개 행동 실행
	act(dog)
	//고양이 행동 실행
	act(cat)

}

```

```
//인터페이스 기본(5)
package main

import "fmt"

type Dog struct {
	name   string
	weight int
}

type Cat struct {
	name   string
	weight int
}

func printValue(s interface{}) {
	fmt.Println(s)
}

func main() {
	//인터페이스 활용(빈 인터페이스)
	//함수내에서 어떠한 타입이라도 유연하게 매개변수로 받을 수 있다. (모든 타입 지정 가능)

	//예제1
	dog := Dog{"poll", 10}
	cat := Cat{"bob", 5}

	//빈 인터페이스 : 어떤 값이든 허용 가능(유연성 증가)
	printValue(dog)
	printValue(cat)
	printValue(15)
	printValue("Animal")
	printValue(25.5)
	printValue([]Dog{})

}

```

```
//인터페이스 고급(1)
package main

import "fmt"

type Dog struct {
	name   string
	weight int
}

type Cat struct {
	name   string
	weight int
}

func printValue(s interface{}) {
	fmt.Println(s)
}

func main() {
	//인터페이스 활용(빈 인터페이스)
	//함수내에서 어떠한 타입이라도 유연하게 매개변수로 받을 수 있다. (모든 타입 지정 가능)
	//빈 인터페이스 : 함수 매개변수, 리턴 값, 구조체 필드 등으로 사용

	//예제1
	dog := Dog{"poll", 10}
	cat := Cat{"bob", 5}

	//빈 인터페이스 : 어떤 값이든 허용 가능(유연성 증가)
	printValue(dog)
	printValue(cat)
	printValue(15)
	printValue("Animal")
	printValue(25.5)
	printValue([]Dog{})

}

```

```
//인터페이스 고급(2)
package main

import "fmt"

func main() {
	//빈 인터페이스 타입 상세 설명
	//모든 타입을 나타내기 위해 빈 인터페이스 사용
	//동적타입으로 생각하면 쉽다(타 언어의 Object 타입)

	//예제1
	var a interface{}

	printContents(a)

	a = 7.5
	printContents(a)

	a = "Golang"
	printContents(a)

	a = true
	printContents(a)

	a = nil
	printContents(a)
}

func printContents(v interface{}) {
	fmt.Printf("Type : (%T) ", v) //원본 타입
	fmt.Println("ex1 : ", v)
}

```

```
//인터페이스 고급(3)
package main

import "fmt"
import "reflect"

func main() {
	//타입 변환
	//실행(런타임) 시에는 인터페이스에 할당한 변수는 실제 타입으로 변환 후 사용해야 하는 경우
	//인터페이스.(타입) 형식 -> 형 변환
	//interfaceVal.(type)

	//예제1
	var a interface{} = 15

	b := a
	c := a.(int)
	//d := a.(float64) //예외 발생

	fmt.Println("ex1 : ", a)
	fmt.Println("ex1 : ", reflect.TypeOf(a))

	fmt.Println("ex1 : ", b)
	fmt.Println("ex1 : ", reflect.TypeOf(b))

	fmt.Println("ex1 : ", c)
	fmt.Println("ex1 : ", reflect.TypeOf(c))

	fmt.Println()

	//예제2(저장된 타입 실제 타입 검사)
	if v, ok := a.(int); ok { //해당 타입 값, 타입 체크 결과
		fmt.Println("ex2 : ", v, ok)
	}

}

```

```
//인터페이스 고급(3)
package main

import "fmt"
import "reflect"

func main() {
	//타입 변환
	//실행(런타임) 시에는 인터페이스에 할당한 변수는 실제 타입으로 변환 후 사용해야 하는 경우
	//인터페이스.(타입) 형식 -> 형 변환
	//interfaceVal.(type)

	//예제1
	var a interface{} = 15

	b := a
	c := a.(int)
	//d := a.(float64) //예외 발생

	fmt.Println("ex1 : ", a)
	fmt.Println("ex1 : ", reflect.TypeOf(a))

	fmt.Println("ex1 : ", b)
	fmt.Println("ex1 : ", reflect.TypeOf(b))

	fmt.Println("ex1 : ", c)
	fmt.Println("ex1 : ", reflect.TypeOf(c))

	fmt.Println()

	//예제2(저장된 타입 실제 타입 검사)
	if v, ok := a.(int); ok { //해당 타입 값, 타입 체크 결과
		fmt.Println("ex2 : ", v, ok)
	}

}

```

```
//인터페이스 고급(5)
package main

import (
	"fmt"
	"strconv"
)

type Account struct {
	number   string
	balance  float64
	interest float64
}

func structToMsg(arg interface{}) string {
	switch arg.(type) {
	case Account:
		o := arg.(Account)
		return "Account : " + o.number + " : " + strconv.FormatFloat((o.balance*o.interest+o.balance), 'f', -1, 64)
	case *Account:
		o := arg.(*Account)
		return "*Account : " + o.number + " : " + strconv.FormatFloat((o.balance*o.interest+o.balance), 'f', -1, 64)
	default:
		return "Error"
	}
}

func main() {

	//예제1
	fmt.Println(structToMsg(Account{number: "245-901", balance: 10000000, interest: 0.015}))
	fmt.Println(structToMsg(&Account{number: "245-902", balance: 12000000, interest: 0.035}))

	var user = new(Account)
	user.number = "245-903"
	user.balance = 15000000
	user.interest = 0.025

	fmt.Println(structToMsg(user))
}

```
