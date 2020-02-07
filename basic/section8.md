# section8

### 사용자정의 타입

```
//사용자 정의 타입(1)
package main

import "fmt"

// 사용자 정의 타입(구조체)
type Car struct {
	name  string
	color string
	price int64
	tax   int64
}

//구조체 <-> 메소드 바인딩
func (c Car) Price() int64 {
	return c.price + c.tax
}

func main() {
	//Go -> 객체 지향 타입을 구조체로 정의한다.(클래스, 상속 개념 없음)
	//상태, 메소드를 분리해서 정의(결합성 없음)
	//사용자 정의 타입 : 구조체 , 인터페이스 , 기본타입 , 함수
	//구조체와 -> 메서드 연결을 통해서 타 언어의 클래스 형식 처럼 사용 가능(객체 지향)

	//예제1
	bmw := Car{name: "520d", price: 54500000, color: "white", tax: 545000}
	benz := Car{name: "220d", price: 74500000, color: "white", tax: 745000}

	bmwPrice := bmw.Price()
	benzPrice := benz.Price()

	fmt.Println("ex1 : ", &bmw)
	fmt.Println("ex1 : ", bmwPrice)
	fmt.Println("ex1 : ", bmw.Price())

	fmt.Println("ex1 : ", &benz == &bmw)

	fmt.Println("ex1 : ", &benz)
	fmt.Println("ex1 : ", benzPrice)
	fmt.Println("ex1 : ", benz.Price())

}


```

```
//사용자 정의 타입(2)
package main

import "fmt"

type cnt int

func main() {
	//기본 자료형 사용자 정의 타입

	//예제1
	a := cnt(5)

	fmt.Println("ex1 : ", a)

	//예제2
	var b cnt = 15

	fmt.Println("ex2 : ", b)
	//testConvertT(b) //예외 발생 (중요!) 사용자 정의 타입 <-> 기본 타입 : 매개변수 전달 시에 변환해야 사용 가능 (cnt(5), int(5))
	testConvertT(int(b))

	testConvertD(b)
	testConvertD(cnt(10)) //사용 가능
	//testConvertD(int(b)) //예외 발생 (중요!) 사용자 정의 타입 <-> 기본 타입 : 매개변수 전달 시에 변환해야 사용 가능 (cnt(5), int(5))
}

func testConvertT(i int) {
	fmt.Println("ex 2 : (Default Type) : ", i)
}

func testConvertD(i cnt) {
	fmt.Println("ex 2 : (Custom Type) : ", i)
}

```

```
//사용자 정의 타입(3)
package main

import "fmt"

type totCost func(int, int) int

func describe(cnt int, price int, fn totCost) {
	fmt.Printf("cnt: %d, price: %d, orderPrice: %d", cnt, price, fn(cnt, price))
}

func main() {
	//함수 사용자 정의 타입

	//예제1
	var orderPrice totCost
	orderPrice = func(cnt int, price int) int {
		return (cnt * price) + 1000000
	}
	describe(3, 10000000, orderPrice)
}

```
```
//사용자 정의 타입(4)
package main

import "fmt"

type shopingBasket struct{ cnt, price int }

func (b shopingBasket) purchase() int {
	return b.cnt * b.price
}

func (b *shopingBasket) rePurchaseP(cnt, price int) {
	b.cnt += cnt
	b.price += price
}

func (b shopingBasket) rePurchaseD(cnt, price int) {
	b.cnt += cnt
	b.price += price
}

func main() {
	//리시버 전달(값, 참조) 형식
	//함수는 기본적으로 값 호출  -> 변수의 값이 복사 후 내부 전달(원본 수정X) -> 맵, 슬라이스 등은 참조 전달
	//리시버(구조체)도 마찬가지로 포인터를 활용해서 메소드 내에서 원본 수정 가능

	//예제1
	bs1 := shopingBasket{3, 5000}
	fmt.Println("ex1(totPrice) : ", bs1.purchase())
	bs1.rePurchaseP(10, 10000) //매개변수 전달(참조)
	fmt.Println("ex1(totPrice) :", bs1.purchase())

	fmt.Println()

	//예제2
	bs2 := shopingBasket{5, 5000}
	fmt.Println("ex2(totPrice) : ", bs2.purchase())
	bs2.rePurchaseD(10, 10000) //매개변수 전달(복사)
	fmt.Println("ex2(totPrice) :", bs2.purchase())

	fmt.Println()

	//예제3
	bs3 := shopingBasket{10, 10000}

	fmt.Println("ex3(totPrice) : ", bs3.purchase())
	bs3.rePurchaseP(-5, -7000) //매개변수 전달(참조)
	fmt.Println("ex3(totPrice) :", bs3.purchase())
}


```
### 구조체(struct)
```
//구조체 기본(1)
package main

import "fmt"

type Account struct {
	number   string
	balance  float64
	interest float64
}

func (a Account) Calculate() float64 {
	return a.balance + (a.balance * a.interest)
}

func main() {
	//구조체
	//Go의 필드들의 집합체 또는 컨테이너
	//필드는 갖지만 메소드는 갖지 않는다.
	//객체지향 방식을 지원 -> 리시버를 통해 메소드랑 연결
	//상속, 객체, 클래스 개념 없음
	//구조체 -> 구조체 선언 -> 구조체 인스턴스(리시버)

	//예제1
	kim := Account{number: "245-901", balance: 10000000, interest: 0.015}
	lee := Account{number: "245-902", balance: 12000000} //기본값 0 초기화
	park := Account{number: "245-903", interest: 0.025}
	cho := Account{"245-904", 15000000, 0.03}

	fmt.Println("ex1 : ", kim)
	fmt.Println("ex1 : ", lee)
	fmt.Println("ex1 : ", park)
	fmt.Println("ex1 : ", cho)

	fmt.Println()

	//예제2
	fmt.Println("ex2 : ", int(kim.Calculate()))
	fmt.Println("ex2 : ", int(lee.Calculate()))
	fmt.Println("ex2 : ", int(park.Calculate()))
	fmt.Println("ex2 : ", int(cho.Calculate()))
}

```
```
//구조체 기본(2)
package main

import "fmt"

type Account struct {
	number   string
	balance  float64
	interest float64
}

func (a Account) Calculate() float64 {
	return a.balance + (a.balance * a.interest)
}

func main() {

	//예제1
	//선언 방법1
	var kim *Account = new(Account)
	kim.number = "245-901"
	kim.balance = 10000000
	kim.interest = 0.015

	//선언 방법2
	hong := &Account{number: "245-902", balance: 15000000, interest: 0.04}

	//선언 방법3
	lee := new(Account)
	lee.number = "245-903"
	lee.balance = 13000000
	lee.interest = 0.025

	fmt.Println("ex1 : ", kim)
	fmt.Println("ex1 : ", hong)
	fmt.Println("ex1 : ", lee)
	fmt.Printf("ex1 : %#v\n", kim)
	fmt.Printf("ex1 : %#v\n", hong)
	fmt.Printf("ex1 : %#v\n", lee)

	fmt.Println()

	//예제2
	fmt.Println("ex2 : ", int(kim.Calculate()))
	fmt.Println("ex2 : ", int(hong.Calculate()))
	fmt.Println("ex2 : ", int(lee.Calculate()))

}

```
```
//구조체 기본(3)
package main

import "fmt"

type car struct {
	color string
	name  string
}

func main() {

	//예제1
	//함수의 매개변수로 전달시에는 기본적으로 값 복사 이므로, 필요시 포인터로 전달해야 한다.
	c1 := car{"red", "220d"}
	c2 := new(car)
	c2.color, c2.name = "white", "sonata"
	c3 := &car{}
	c4 := &car{"black", "520d"}

	fmt.Println(c1)
	fmt.Println(c2)
	fmt.Println(c3)
	fmt.Println(c4)
	fmt.Println()
}

```
```
//구조체 기본(4)
package main

import "fmt"

func main() {
	//구조체 익명 선언 및 활용

	//예제1
	car1 := struct{ name, color string }{"520d", "red"}

	fmt.Println("ex1 : ", car1)
	fmt.Printf("ex1 : %#v\n", car1)

	//예제2
	cars := []struct{ name, color string }{{"520d", "red"}, {"220d", "white"}, {"420d", "black"}}
	for _, c := range cars {
		fmt.Printf("(%s, %s) ----- (%#v)\n", c.name, c.color, c)
	}

}

```
```
//구조체 기본(5)
package main

import "fmt"
import "reflect"

type Car struct {
	name    string "차량명"
	color   string "색상"
	company string "제조사"
}

func main() {
	//필드 태그 사용

	//예제1
	tag := reflect.TypeOf(Car{})
	for i := 0; i < tag.NumField(); i++ {
		fmt.Println("ex1 : ", tag.Field(i).Tag, tag.Field(i).Name, tag.Field(i).Type)
	}
}

```
```
//구조체 기본(6)
package main

import "fmt"

type spec struct { //소문자로 선언
	length int "전장"
	height int "전고"
	width  int "전축"
}

type Car struct { //대문자로 선언
	name    string
	color   string
	company string
	detail  spec
}

func main() {
	//중첩 구조체

	//예제1
	car1 := Car{
		"520d",
		"silver",
		"bmw",
		spec{4000, 1000, 2000},
	}
	// 내부 spec 구조체 값 출력
	fmt.Println("ex1 : ", car1.name)
	fmt.Println("ex1 : ", car1.color)
	fmt.Println("ex1 : ", car1.company)
	fmt.Printf("ex1 : %#v\n", car1.detail)
	fmt.Println()

	//예제2
	// 내부 spec 구조체 필드 값 출력
	fmt.Println("ex2 : ", car1.detail.length)
	fmt.Println("ex2 : ", car1.detail.height)
	fmt.Println("ex2 : ", car1.detail.width)

}

```

```
//구조체 심화(1)
package main

import "fmt"

type Account struct {
	number   string
	balance  float64
	interest float64
}

func NewAccount(number string, balance float64, interest float64) *Account { //포인터 반환 아닌 경우 값 복사로 사용
	return &Account{number, balance, interest} // 구조체 인스턴스를 생성한 뒤 포인터를 리턴
}

func main() {
	//구조체 생성자 패턴 예제

	//예제1
	kim := Account{number: "245-901", balance: 10000000, interest: 0.015}

	var lee *Account = new(Account) //new 함수로 초기화와 동시에 구제체 필드 값 할당은 불가능
	lee.number = "245-902"
	lee.balance = 13000000
	lee.interest = 0.025

	fmt.Println("ex1 : ", kim)
	fmt.Println("ex1 : ", lee)

	//예제2
	park := NewAccount("245-903", 17000000, 0.04)
	fmt.Println("ex2 : ", park)

}

```

```
//구조체 심화(2)
package main

import "fmt"

type Account struct {
	number   string
	balance  float64
	interest float64
}

func CalculateD(a Account) { //값 복사 전달
	a.balance = a.balance + (a.balance * a.interest)
}

func CalculateF(a *Account) { //주소(참조) 전달
	a.balance = a.balance + (a.balance * a.interest)
}

func main() {
	//구조체 생성자 패턴 예제

	//예제1
	kim := Account{number: "245-901", balance: 10000000, interest: 0.015}
	lee := Account{number: "245-902", balance: 12000000, interest: 0.045}

	fmt.Println("ex1 : ", kim)
	fmt.Println("ex1 : ", lee)
	fmt.Println()

	CalculateD(kim)
	CalculateF(&lee) //CalculateF(lee) 호출 시 예외 발생

	fmt.Println("ex1 : ", int(kim.balance))
	fmt.Println("ex1 : ", int(lee.balance))

}

```

```
//구조체 심화(3)
package main

import "fmt"

type Account struct {
	number   string
	balance  float64
	interest float64
}

//리시버 변수 사용안할 경우 func(_ Account) -> 밑줄로 생략 가능

func (a Account) CalculateD(bonus float64) { //값 복사 전달
	a.balance = a.balance + (a.balance * a.interest) + bonus
}

func (a *Account) CalculateF(bonus float64) { //주소(참조) 전달
	a.balance = a.balance + (a.balance * a.interest) + bonus
}

func main() {
	//구조체 생성자 패턴 예제

	//정리 : 구조체 인스턴스 값 변경 시 -> 포인터 전달 , 보통의 경우 -> 값 전달

	//예제1
	kim := Account{number: "245-901", balance: 10000000, interest: 0.015}
	lee := Account{number: "245-902", balance: 12000000, interest: 0.045}

	fmt.Println("ex1 : ", kim)
	fmt.Println("ex1 : ", lee)
	fmt.Println()

	lee.CalculateD(1000000)
	kim.CalculateF(1000000)

	fmt.Println("ex1 : ", int(lee.balance))
	fmt.Println("ex1 : ", int(kim.balance))

}

```

```
//구조체 심화(4)
package main

import "fmt"

type Employee struct {
	name   string
	salary float64
	bonus  float64
}

func (e Employee) Calculate() float64 {
	return e.salary + e.bonus
}

type Executives struct {
	Employee
	specialBonus float64
}

func main() {
	//구조체 임베디드 패턴
	//다른 관점으로 메소드를 재 사용하는 장점 제공

	//상속을 허용하지 않는 Go 언어에서 메소드 상속 활용을 위한 패턴

	//예제1
	//직원
	ep1 := Employee{"kim", 2000000, 300000}
	ep2 := Employee{"park", 1500000, 200000}
	//임원
	ex := Executives{
		Employee{"lee", 4000000, 1000000},
		1000000,
	}

	fmt.Println("ex1 : ", int(ep1.Calculate()))
	fmt.Println("ex1 : ", int(ep2.Calculate()))
	//Employee 구조체 통해서 메소드 호출(임베디드)
	fmt.Println("ex1 : ", int(ex.Calculate()+ex.specialBonus))

}

```

```
//구조체 심화(5)
package main

import "fmt"

type Employee struct {
	name   string
	salary float64
	bonus  float64
}

func (e Employee) Calculate() float64 {
	return e.salary + e.bonus
}

//이름이 같은 함수 사용 : 오버라이딩
func (e Executives) Calculate() float64 {
	return e.Employee.salary + e.Employee.bonus + e.specialBonus
}

type Executives struct {
	Employee
	specialBonus float64
}

func main() {
	//구조체 임베디드 메소드 오버라이딩 패턴
	//
	//예제1
	//직원
	ep1 := Employee{"kim", 2000000, 300000}
	ep2 := Employee{"park", 1500000, 200000}
	//임원
	ex := Executives{
		Employee{"lee", 4000000, 1000000},
		1000000,
	}

	fmt.Println("ex1 : ", int(ep1.Calculate()))
	fmt.Println("ex1 : ", int(ep2.Calculate()))

	fmt.Println("ex1 : ", int(ex.Calculate()+ex.specialBonus)) //오버라이딩 : 잘못 된 값 반환
	fmt.Println("ex1 : ", int(ex.Calculate()))                 //오버라이딩 : 정확한 값
	fmt.Println("ex1 : ", int(ex.Employee.Calculate()+ex.specialBonus))

}

```
