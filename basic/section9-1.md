# section9-1

### 고루틴(Goroutine)

```
//고루틴(Goroutine)기초(1)
package main

import "fmt"
import "time"

func exe1() {
	fmt.Println("exe1 func start", time.Now())
	time.Sleep(1 * time.Second)
	fmt.Println("exe1 func end", time.Now())
}

func exe2() {
	fmt.Println("exe2 func start", time.Now())
	time.Sleep(1 * time.Second)
	fmt.Println("exe2 func end", time.Now())
}

func exe3() {
	fmt.Println("exe3 func start", time.Now())
	time.Sleep(1 * time.Second)
	fmt.Println("exe3 func end", time.Now())
}

func main() {
	//고루틴(Goroutine)
	//타 언어의 쓰레드(Thread)와 비슷한 기능
	//생성 방법 매우 간단, 리소스 매우 적게 사용
	//즉, 수많은 고루틴 동시 생성 실행 가능
	//비동기적 함수 루틴 실행(매우 적은 용량 차지) -> 채널을 통해 통신
	//공유메모리 사용 시에 정확한 동기화 코딩 필요
	//싱글루틴에 비해 항상 빠른 처리 결과는 아니다.

	exe1() //가정 먼저 실행(일반적인 실행 흐름)

	//예제1
	fmt.Println("Main Routine Start : ", time.Now())
	go exe2()
	go exe3()
	time.Sleep(4 * time.Second) // 4초 대기 (주석처리하면 별도 고루틴 종료 : 메인함수 종료 시 모두 종료)
	//fmt.Scanln() //콘솔에서 테스트 할 경우 시간 대기 용도 사용 가능
	fmt.Println("Main Routine End : ", time.Now())
}

```

```
//고루틴(Goroutine)기초(2)
package main

import "fmt"
import "time"

func exe(name string) {
	fmt.Println(name, " start : ", time.Now())
	for i := 0; i < 1000; i++ {
		fmt.Println(name, ">>>>>>>", i)
	}
	fmt.Println(name, " func end : ", time.Now())
}

func main() {
	//고루틴(Goroutine)

	exe("t1")
	//예제1
	fmt.Println("Main Routine Start : ", time.Now())
	go exe("t2")
	go exe("t3")
	time.Sleep(4 * time.Second) //time.Second, Minute, Hour, Millisecond ....
	fmt.Println("Main Routine End : ", time.Now())
}

```

```
//고루틴(Goroutine)기초(3)
package main

import "fmt"
import "time"
import "math/rand"
import "runtime"

func exe(name int) {
	r := rand.Intn(100)
	fmt.Println(name, " start : ", time.Now())
	for i := 0; i < 100; i++ {
		fmt.Println(name, ">>>>>>>", r, i)
	}
	fmt.Println(name, " func end : ", time.Now())
}

func main() {
	//고루틴(Goroutine)
	//멀티 코어(다중 CPU) 최대한 활용

	runtime.GOMAXPROCS(runtime.NumCPU())                        // 현 시스템의 CPU 코어 개수 반환 후 설정
	fmt.Println("Current System Cpu : ", runtime.GOMAXPROCS(0)) // 설정 값 출력

	//예제1
	fmt.Println("Main Routine Start : ", time.Now())
	for i := 0; i < 100; i++ {
		go exe(i) //고루틴 100개 생성
	}
	time.Sleep(5 * time.Second) //time.Second, Minute, Hour, Millisecond ....
	fmt.Println("Main Routine End : ", time.Now())
}

```

```
//고루틴(Goroutine)기초(4)
package main

import (
	"fmt"
	"runtime"
	"time"
)

func main() {
	//고루틴(Goroutine)
	//클로저 사용 예제

	//예제1
	runtime.GOMAXPROCS(1) // CPU를 하나만 사용

	s := "Goroutine Closure : "

	for i := 0; i < 1000; i++ { //고루틴 1000개 실행
		go func(n int) {
			fmt.Println(s, n, " - ", time.Now())
		}(i) //반복문 클로저는 일반적으로 즉시 실행 But 고루틴 클로저는 가장 나중에 실행(반복문 종료 후)
	}
	/*
		//실행 결과 비교
		for i := 0; i < 1000; i++ {
			go func() {
				fmt.Println(s, n, " - ", time.Now())
			}()
		}
	*/

	time.Sleep(5 * time.Second)
}

```
