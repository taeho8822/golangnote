# section6

### 배열 (array)

```
//자료형 : 배열(1)
package main

import "fmt"

func main() {
	//배열
	//배열은 용량, 길이 항상 같다.
	//배열 vs 슬라이스 차이점 중요
	//길이 고정 						   vs 길이 가변
	//값 타입 								  vs 참조 타입
	//복사 전달 							 vs  참조 값 전달
	//전체 비교연산자 사용 가능 vs 비교 연산자 사용 불가
	//대 부분 슬라이스 사용한다.

	//cap() : 배열, 슬라이스 용량
	//len() : 배열, 슬라이스 개수

	//예제1
	var arr1 [5]int
	var arr2 [5]int = [5]int{1, 2, 3, 4, 5}
	var arr3 = [5]int{1, 2, 3, 4, 5}
	arr4 := [5]int{1, 2, 3, 4, 5}
	arr5 := [5]int{1, 2, 3} //기본 0 초기화
	arr6 := [...]int{1, 2, 3, 4, 5}
	arr7 := [5][5]int{
		{1, 2, 3, 4, 5},
		{6, 7, 8, 9, 10}, //콤마 주의
	}

	arr1[2] = 5 //값 삽입

	fmt.Printf("%-5T %d %v\n", arr1, len(arr1), arr1)
	fmt.Printf("%-5T %d %v\n", arr2, len(arr2), arr2)
	fmt.Printf("%-5T %d %v\n", arr3, len(arr3), arr3)
	fmt.Printf("%-5T %d %v\n", arr4, len(arr4), arr4)
	fmt.Printf("%-5T %d %v\n", arr5, len(arr5), arr5)
	fmt.Printf("%-5T %d %v\n", arr6, len(arr6), arr6)
	fmt.Printf("%-5T %d %v\n", arr7, len(arr7), arr7)

	//예제2
	arr8 := [5]int{1, 2, 3, 4, 5}
	arr9 := [5]int{ //여러 줄 선언 콤마 주의
		1,
		2,
		3,
		4,
		5,
	}
	arr10 := [...]string{"Kim", "Lee", "Park"}

	fmt.Printf("%-5T %d %v\n", arr8, len(arr8), arr8)
	fmt.Printf("%-5T %d %v\n", arr9, len(arr9), arr9)
	fmt.Printf("%-5T %d %v\n", arr10, len(arr10), arr10)
}

```

```
//자료형 : 배열(2)
package main

import "fmt"

func main() {
	//배열 순회

	//예제1
	arr1 := [5]int{1, 10, 100, 1000, 10000}

	//len 길이 반복
	for i := 0; i < len(arr1); i++ {
		fmt.Println("ex1 : ", arr1[i])
	}
	fmt.Println() //줄 바꿈

	//예제2
	arr2 := [5]int{1, 10, 100, 1000, 10000}

	//range 사용
	for i, v := range arr2 {
		fmt.Println("ex2 : ", i, v)
	}
	fmt.Println()

	//인덱스 생략1
	for _, v := range arr2 {
		fmt.Println("ex3 : ", v)
	}

	//인덱스 생략2
	fmt.Println()
	for v := range arr2 {
		fmt.Println("ex4 : ", v)
	}

}

```

```
//자료형 : 배열(3)
package main

import "fmt"

func main() {
	//배열 복사
	//값 복사 확인 중요

	//예제1
	arr1 := [5]int{1, 10, 100, 1000, 10000}
	arr2 := arr1

	fmt.Println("ex1 : ", arr1, &arr1)
	fmt.Println("ex1 : ", arr2, &arr2)
	fmt.Printf("ex1: %p %v\n", &arr1, arr1) //주소 값 출력
	fmt.Printf("ex1: %p %v\n", &arr2, arr2) //주소 값 출력

}


```


### slicxe
```
//자료형 : 슬라이스(1)
package main

import "fmt"

func main() {
	//슬라이스(길이 & 용량 개념)
	//슬라이스 배열과 같지만 크기가 동적 할당 가능
	//배열 vs 슬라이스 차이점 중요
	//길이 고정 						   vs 길이 가변
	//값 타입 								  vs 참조 타입(레퍼런스)
	//복사 전달 							 vs  참조 값 전달
	//전체 비교연산자 사용 가능 vs 비교 연산자 사용 불가
	//대 부분 슬라이스 사용한다.

	//make(자료형, 길이, 용량(생략시 길이)) : 할당해야 값 삽입 가능

	//예제1
	var slice1 []int
	slice2 := []int{}
	slice3 := []int{1, 2, 3, 4, 5}
	slice4 := [][]int{
		{1, 2, 3, 4, 5},
		{6, 7, 8, 9, 10}, //콤마 주의
	}
	//slice2[0] = 1 예외 발생
	//slice3[4] = 10 //값 수정 가능

	fmt.Printf("%-5T %d %d %v\n", slice1, len(slice1), cap(slice1), slice1)
	fmt.Printf("%-5T %d %d %v\n", slice2, len(slice2), cap(slice2), slice2)
	fmt.Printf("%-5T %d %d %v\n", slice3, len(slice3), cap(slice3), slice3)
	fmt.Printf("%-5T %d %d %v\n", slice4, len(slice4), cap(slice4), slice4)
	fmt.Println()

	//예제2
	var slice5 []int = make([]int, 5)
	var slice6 = make([]int, 5)
	slice7 := make([]int, 5, 10)
	slice8 := make([]int, 5)
	slice6[2] = 7 //삽입

	fmt.Printf("%-5T %d %d %v\n", slice5, len(slice5), cap(slice5), slice5)
	fmt.Printf("%-5T %d %d %v\n", slice6, len(slice6), cap(slice6), slice6)
	fmt.Printf("%-5T %d %d %v\n", slice7, len(slice7), cap(slice7), slice7)
	fmt.Printf("%-5T %d %d %v\n", slice8, len(slice8), cap(slice8), slice8) //길이와 용량 같다.
	fmt.Println()

	//예제3
	var slice9 []int //nil 슬라이스 (길이와 용량 0)
	if slice9 == nil {
		fmt.Println("This is Nil Slice.")
	}
}


```

```
//자료형 : 슬라이스(2)
package main

import "fmt"

func main() {
	//슬라이스(슬라이스 참조 타입 증명)

	//예제1(배열)
	arr1 := [3]int{1, 2, 3}
	var arr2 [3]int

	arr2 = arr1
	arr2[0] = 7

	fmt.Println("ex1 : ", arr1)
	fmt.Println("ex1 : ", arr2)
	fmt.Println()

	//예제2(슬라이스)
	slice1 := []int{1, 2, 3}
	var slice2 []int

	slice2 = slice1
	slice2[0] = 7

	fmt.Println("ex2 : ", slice1)
	fmt.Println("ex2 : ", slice2)
	fmt.Println()

	//예제3(슬라이스 예외 상황)
	slice3 := make([]int, 5, 10)
	fmt.Println("ex3 : ", slice3[4])
	//fmt.Println("ex3 : ", slice3[5]) //길이 index over 예외
	//fmt.Println("ex3 : ", slice3[8]) //길이 index over 예외
	fmt.Println()

	//예제4(슬라이스 순회)
	for i, v := range arr1 {
		fmt.Println("ex4 : ", i, v)
	}
}

```

```
//자료형 : 슬라이스 심화(1)
package main

import "fmt"

func main() {
	//슬라이스 추가 및 병합

	//예제1
	s1 := []int{1, 2, 3, 4, 5}
	s2 := []int{8, 9, 10, 11, 12}
	s3 := []int{13, 14, 15, 16, 17}
	s1 = append(s1, 6, 7)
	s2 = append(s1, s2...)      //슬라이스를 삽입 할 경우 ... 사용
	s3 = append(s2, s3[0:3]...) //추출 후 병합

	fmt.Println("ex1 : ", s1)
	fmt.Println("ex1 : ", s2)
	fmt.Println("ex1 : ", s3)
	fmt.Println()

	//예제2
	s4 := make([]int, 0, 5)
	for i := 0; i < 15; i++ {
		s4 = append(s4, i)
		fmt.Printf("ex2 -> len: %d, cap: %d, value: %v\n", len(s4), cap(s4), s4) //길이 및 용량 자동 증가(용량 : 2배)
	}

}

```

```
//자료형 : 슬라이스 심화(2)
package main

import "fmt"
import "sort"

func main() {
	//슬라이스 추출 및 정렬
	//slice[i:j] s -> j-1 까지 추출
	//slice[i:]  i -> 마지막 까지 추출
	//slice[:j] 처음 -> j-1 까지 추출
	//slice[:]  처음부터 마지막 까지 추출

	//예제1(추출)
	slice1 := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

	fmt.Println("ex1 : ", slice1[:])
	fmt.Println("ex1 : ", slice1[0:])
	fmt.Println("ex1 : ", slice1[:5])
	fmt.Println("ex1 : ", slice1[0:len(slice1)])
	fmt.Println("ex1 : ", slice1[3:])
	fmt.Println("ex1 : ", slice1[:3])
	fmt.Println("ex1 : ", slice1[1:3])
	fmt.Println()

	//예제2(정렬)
	//sort 패키지 : https://golang.org/pkg/sort/ 참조
	slice2 := []int{3, 6, 10, 9, 1, 4, 5, 8, 2, 7}
	slice3 := []string{"b", "d", "f", "a", "c", "e"}
	fmt.Println("ex2 : ", sort.IntsAreSorted(slice2))
	sort.Ints(slice2)
	fmt.Println("ex2 : ", slice2) //Int형 정렬
	fmt.Println("ex2 : ", sort.IntsAreSorted(slice2))

	fmt.Println()

	fmt.Println("ex2 : ", sort.StringsAreSorted(slice3))
	sort.Strings(slice3)
	fmt.Println("ex2 : ", slice3) //String형 정렬
	fmt.Println("ex2 : ", sort.StringsAreSorted(slice3))

}

```

```
//자료형 : 슬라이스 심화(3)
package main

import "fmt"

func main() {
	//슬라이스 복사
	//copy(복사 대상, 원본)
	//make로 공간을 할당 후 복사 해야한다.
	//복사 된 슬라이스 값 변경해도 원본에는 영향 없음

	//예제1(복사)
	slice1 := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	slice2 := make([]int, 5)
	slice3 := []int{}

	copy(slice2, slice1)
	copy(slice3, slice1)

	fmt.Println("ex1 : ", slice2)
	fmt.Println("ex1 : ", slice3) //복사 안됨

	fmt.Println()

	//예제2
	a := []int{1, 2, 3, 4, 5}
	b := make([]int, 5)
	copy(b, a)
	b[0] = 7
	b[4] = 10

	fmt.Println("ex2 : ", a) //원본 유지
	fmt.Println("ex2 : ", b) //복사 된 대상 변경
	fmt.Println()

	//예제3
	c := [5]int{1, 2, 3, 4, 5}
	d := c[0:3] //주의! 부분적으로 슬라이스 추출은 참조 -> 원본 값 변경 된다.
	d[1] = 7

	fmt.Println("ex3 : ", c)
	fmt.Println("ex3 : ", d)
	fmt.Println()

	//예제4
	e := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	f := e[0:5:7] //용량 지정

	fmt.Println("ex4 : ", len(f), cap(f))
	fmt.Println("ex4 : ", f)
}

```

### Map (맵)
```
//자료형 : 맵(1)
package main

import "fmt"

func main() {
	//맵(Map)
	//맵 : 해시테이블, 딕셔너리(파이썬), Key-Value로 자료 저장
	//레퍼런스 타입!(참조 값 전달)
	//비교 연산자 사용 불가능(참조 타입이므로)
	//특징 : 참조타입 키(Key)로 사용 불가능 , 값(Value)으로 모든 타입 사용 가능
	//make 함수 및 축약(리터럴)로 초기화 가능
	//순서 없음

	//예제1
	var map1 map[string]int = make(map[string]int) //정석
	var map2 = make(map[string]int)                //자료형 생략
	map3 := make(map[string]int)                   //리터럴 형

	fmt.Println("ex1 : ", map1)
	fmt.Println("ex1 : ", map2)
	fmt.Println("ex1 : ", map3)
	fmt.Println()

	//예제2
	map4 := map[string]int{}
	map4["apple"] = 25
	map4["banana"] = 40
	map4["orange"] = 33

	map5 := map[string]int{
		"apple":  15,
		"banana": 30,
		"orange": 23, //콤마 주의
	}

	map6 := make(map[string]int, 10)
	map6["apple"] = 5
	map6["banana"] = 10
	map6["orange"] = 15

	fmt.Println("ex2 : ", map4)
	fmt.Println("ex2 : ", map5)
	fmt.Println("ex2 : ", map6)
	fmt.Println("ex2 : ", map6["orange"])
	fmt.Println("ex2 : ", map6["apple"])
	fmt.Println()

}

```

```
//자료형 : 맵(2)
package main

import "fmt"

func main() {
	//맵(Map)
	//맵 조회 및 순회(Iterator)

	//예제1
	map1 := map[string]string{
		"daum":   "http://daum.net",
		"naver":  "http://naver.com",
		"google": "http://google.com",
	}
	fmt.Println("ex1 : ", map1["google"])
	fmt.Println("ex1 : ", map1["daum"])
	fmt.Println()

	//예제2(순서 없으므로 랜덤)
	for k, v := range map1 {
		fmt.Println("ex2 : ", k, v)
	}

	fmt.Println()

	for _, v := range map1 { //변수 선언 후 사용안하면 예외 발생
		fmt.Println("ex2 : ", v)
	}
}

```

```
//자료형 : 맵(3)
package main

import "fmt"

func main() {
	//맵(Map)
	//맵 값 변경 및 삭제

	//예제1(수정)
	map1 := map[string]string{
		"daum":   "http://daum.net",
		"naver":  "http://naver.com",
		"google": "http://google.com",
		"home1":  "http://test1.com",
	}
	fmt.Println("ex1 : ", map1)
	map1["home2"] = "http://test2.com" //추가
	fmt.Println("ex1 : ", map1)
	map1["home2"] = "http://test2-2.com" //수정
	fmt.Println("ex1 : ", map1)
	fmt.Println()

	//예제2(삭제)
	delete(map1, "home2")
	fmt.Println("ex1 : ", map1)
	delete(map1, "home1")
	fmt.Println("ex1 : ", map1)

}

```

```
//자료형 : 맵(4)
package main

import "fmt"

func main() {
	//맵(Map)
	//맵 조회 할 경우 주의 할점

	//예제1
	map1 := map[string]int{
		"apple":  15,
		"banana": 115,
		"orange": 1115,
		"lemon":  0,
	}

	value1 := map1["lemon"]
	value2 := map1["kiwi"]
	value3, ok := map1["kiwi"]

	fmt.Println("ex1 : ", value1)
	fmt.Println("ex1 : ", value2)
	fmt.Println("ex1 : ", value3, ok) //두 번째 리턴 값으로 키 존재 유무 확인
	fmt.Println()

	//예제2
	if value, ok := map1["kiwi"]; ok {
		fmt.Println("ex2 : ", value)
	} else {
		fmt.Println("ex2 : kiwi is not exist!")
	}

	if value, ok := map1["lemon"]; ok {
		fmt.Println("ex2 : ", value)
	} else {
		fmt.Println("ex2 : kiwi is not exist!")
	}

	if _, ok := map1["kiwi"]; !ok {
		fmt.Println("ex2 : kiwi is not exist!")
	}
}

```

### pointer

```
//자료형 : 포인터(1)
package main

import "fmt"

func main() {
	//포인터
	//Go : 포인터 지원(C, C++)
	//포인터지원 X(파이썬, C#, JAVA 등)
	//주소의 값은 직접 변경 불가능(잘못된 코딩으로 인한 버그 방지)
	//메모리 주소를 출력(값의 메모리 주소)
	//애스터리스크로 사용(*)
	//nil로 초기화(0 아님)

	//예제1
	var a *int            //방법1
	var b *int = new(int) //방법2

	fmt.Println(a) //nil
	fmt.Println(b) //nil

	i := 7
	a = &i //& 주소값 전달
	b = &i

	var c = &i //방법3
	d := &i    //방법4

	fmt.Println("ex1 : ", i)
	fmt.Println("ex1 : ", &i) //실행 할 때 마다 시스템 별로 변경

	fmt.Println("ex1 : ", *a)
	fmt.Println("ex1 : ", a)
	fmt.Println("ex1 : ", &a) //포인터 변수 a의 주소 값

	fmt.Println("ex1 : ", *b)
	fmt.Println("ex1 : ", b)
	fmt.Println("ex1 : ", &b) //포인터 변수 b의 주소 값

	fmt.Println("ex1 : ", *c)
	fmt.Println("ex1 : ", c)
	fmt.Println("ex1 : ", &c) //포인터 변수 c의 주소 값

	fmt.Println("ex1 : ", *d)
	fmt.Println("ex1 : ", d)
	fmt.Println("ex1 : ", &d) //포인터 변수 d의 주소 값
}

```

```
//자료형 : 포인터(2)
package main

import "fmt"

func main() {

	//예제1
	type bag struct{ witdh, height, weight float32 } //구조체
	var p *int = new(int)
	var p_bag *bag = &bag{20, 50, 30}

	fmt.Println("ex1 : ", p)
	fmt.Println("ex1 : ", p_bag)
	fmt.Println()

	//p++              //컴파일 에러, 포인터 연산 허용 X
	//p = 0xc071405232 ////컴파일 에러, 주소값 대입 허용 X

	//예제2
	i := 7
	p = &i

	fmt.Println("ex2 : ", i, *p, &i, p)

	*p++ //1 증가
	fmt.Println("ex2 : ", i, *p, &i, p)

	*p = 10 //포인터 변수 역 참조 값 변경
	fmt.Println("ex2 : ", i, *p, &i, p)

	i = 77 //원본 변수 값 변경
	fmt.Println("ex2 : ", i, *p, &i, p)

}

```

```
//자료형 : 포인터(3)
package main

import "fmt"

func rptc(n *int) {
	*n = 77
}

func vptc(n int) {
	n = 77
}

func main() {
	//포인터 값 전달
	//함수, 메서드 호출 시에 매개변수 값을 복사 전달 -> 함수, 메서드 내에서는 원본 값 변경 불가능
	//원본 값 변경 위해서 포인터 전달 가능
	//특히 크기가 큰 배열인 경우 값 복사시에 시스템 부담 -> 포인터 전달로 해결 But (슬라이스는 참조 전달)

	//예제1
	var a int = 10
	var b int = 10
	fmt.Println("ex1 : ", a)
	fmt.Println("ex1 : ", b)
	fmt.Println()

	rptc(&a)
	vptc(b)
	//vptc(&b) //에러 발생

	fmt.Println("ex1 : ", a)
	fmt.Println("ex1 : ", b)
}

```
