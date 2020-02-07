# section9-2

### 채널(channel)

```
//채널(Channel) 기초(1)

package main

import (
	"fmt"
	"time"
)

func work1(v chan int) {
	fmt.Println("Work1 : S ---> ", time.Now())
	time.Sleep(1 * time.Second)
	fmt.Println("Work1 : E ---> ", time.Now())
	v <- 1
}

func work2(v chan int) {
	fmt.Println("Work2 : S ---> ", time.Now())
	time.Sleep(1 * time.Second)
	fmt.Println("Work2 : E ---> ", time.Now())
	v <- 2
}

func main() {
	//채널(Channel)
	//고루틴간의 상호 정보(데이터) 교환 및 실행 흐름 동기화 위해 사용 : 채널(동기식, 레퍼런스 타입)
	//실행 흐름 제어 가능(동기, 비동기) -> 일반 변수로 선언 후 사용 가능
	//데이터 전달 자료형 선언 후 사용(지정 된 타입만 주고받을 수 있음)
	//interface{} 전달을 통해서 자료형 상관없이 전송 및  수신가능
	//값을 전달(복사 후 : bool , int등) , 포인터(슬라이스, 맵) 등을 전달시에는 주의! -> 동기화 사용(Mutex)
	//멀티프로세싱 처리에서 교착상태(경쟁) 주의!
	// <- , ->  ( 채널 <- 데이터 : 송신) , ( <- 채널 : 수신)

	//예제1
	fmt.Println("Main : S ---> ", time.Now())

	//var v chan int
	//v = make(chan int)

	v := make(chan int) //int형 채널 선언
	go work1(v)
	go work2(v)

	<-v
	<-v
	fmt.Println("Main : E ---> ", time.Now())
}

```

```
//채널(Channel) 기초(2)

package main

import (
	"fmt"
)

func rangeSum(rg int, c chan int) {
	sum := 0

	for i := 1; i <= rg; i++ {
		sum += i
	}
	c <- sum
}

func main() {
	//채널(Channel)

	c := make(chan int)

	go rangeSum(1000, c)
	go rangeSum(7000, c)
	go rangeSum(5000, c)

	//순서대로 데이터 수신(동기) : 채널에서 값 수신 완료 될 때까지 대기
	result1 := <-c
	result2 := <-c
	result3 := <-c

	fmt.Println("ex1 : ", result1)
	fmt.Println("ex1 : ", result2)
	fmt.Println("ex1 : ", result3)
}

```

```
//채널(Channel) 기초(3)

package main

import (
	"fmt"
	"time"
)

func main() {
	//채널(Channel)
	//예제1(동기 : 버퍼 미사용)

	ch := make(chan bool)
	cnt := 6

	go func() {
		for i := 0; i < cnt; i++ {
			ch <- true
			fmt.Println("Go : ", i)
			time.Sleep(1 * time.Second) //Sleep 주석 처리 후 테스트!
		}
	}()

	for i := 0; i < cnt; i++ {
		<-ch
		fmt.Println("Main : ", i)
	}

}

```

```
//채널(Channel) 기초(4)

package main

import (
	"fmt"
	"runtime"
)

func main() {
	//채널(Channel)
	//예제1(비동기 : 버퍼 사용)
	//버퍼 : 발신 -> 가득차면 대기 , 비어있으면 작동 , 수신 -> 비어있으면 대기 , 가득차있으면 작동

	runtime.GOMAXPROCS(1)
	ch := make(chan bool, 4)
	cnt := 12

	go func() {
		for i := 0; i < cnt; i++ {
			ch <- true
			fmt.Println("Go : ", i)
		}
	}()

	for i := 0; i < cnt; i++ {
		<-ch
		fmt.Println("Main : ", i)
	}

}

```

```
//채널(Channel) 기초(5)

package main

import (
	"fmt"
)

func main() {
	//채널(Channel
	//Close : 채널 닫기, 주의 -> 닫힌 채널에 값 전송 시 패닉(예외) 발생
	//Range : 채널안에서 값을 꺼낸다.(순회) , 채널 닫아야(Close) 반복문 종료 -> 채널이 열려 있고 값 전송하지 않으면 계속 대기!

	//예제1
	ch := make(chan bool)
	go func() {
		for i := 0; i < 5; i++ {
			ch <- true
		}
		close(ch) //5회 채널에 값 전송 후 채널 닫기
	}()

	for i := range ch { //채널에서 값을 꺼내온다.(채널이 Close 될 때까지)
		fmt.Println("ex1 : ", i)
	}
}

```

```
//채널(Channel) 기초(6)

package main

import (
	"fmt"
)

func main() {
	//채널(Channel)
	//Close : 채널 닫기

	ch := make(chan int)

	go func() {
		for i := 0; i < 3; i++ {
			ch <- 77777
		}
	}()

	val1, ok1 := <-ch
	fmt.Println("ex1 : ", val1, ok1)
	val2, ok2 := <-ch
	fmt.Println("ex1 : ", val2, ok2)
	val3, ok3 := <-ch
	fmt.Println("ex1 : ", val3, ok3)

	close(ch) //채널 닫기
	val4, ok4 := <-ch
	fmt.Println("ex1 : ", val4, ok4)
}

```

```
//채널(Channel) 심화(1)

package main

import (
	"fmt"
	"time"
)

func sendOnly(c chan<- int, cnt int) {
	for i := 0; i < cnt; i++ {
		c <- i
	}

	c <- 777

	//fmt.Println(<-c) //수신 전용 채널에서 발신 처리 시 예외 발생
}

func receiveOnly(c <-chan int) {
	for i := range c {
		fmt.Println("received : ", i)
	}

	fmt.Println(<-c)
}

func main() {
	//채널(Channel)
	//함수 등의 매개변수에 수신 및 발신 전용 채널 지정 가능
	//전용 채널 설정 후 방향이 다를 경우 예외 발생
	//발신 전용 channel <- 데이터형
	//수신 전용 <- channel
	//매개 변수를 통해서 전용 채널 확인할 수 있다.
	//채널 또한 함수의 반환 값으로 사용 가능

	//예제1
	c := make(chan int)

	go sendOnly(c, 10) //발신전용
	go receiveOnly(c)  //수신전용

	time.Sleep(2 * time.Second) //2초간 대기

}

```

```
//채널(Channel) 심화(2)

package main

import (
	"fmt"
)

func sum(cnt int) <-chan int {
	sum := 0
	tot := make(chan int)
	go func() {
		for i := 1; i < cnt; i++ {
			sum += i
		}
		tot <- sum
	}()
	return tot
}

func main() {
	//채널(Channel)
	//채널 또한 함수의 반환 값으로 사용 가능

	//예제1
	c := sum(100)

	fmt.Println("ex1 : ", <-c)

}

```

```
//채널(Channel) 심화(3)

package main

import "fmt"

func receiveOnly(cnt int) <-chan int {
	sum := 0
	tot := make(chan int)
	go func() {
		for i := 1; i <= cnt; i++ {
			sum += i
		}
		tot <- sum
		tot <- 777
		tot <- 777
		close(tot)
	}()
	return tot
}

func total(c <-chan int) <-chan int {
	tot := make(chan int)
	go func() {
		a := 0
		for i := range c {
			a = a + i
		}
		tot <- a
	}()
	return tot
}

func main() {
	//채널(Channel)

	//예제1
	c := receiveOnly(100) //채널 반환
	output := total(c)    //채널 전달 후 반환
	//output <- 777 //예외
	fmt.Println("ex1 : ", <-output)
}

```

```
//채널(Channel) 심화(4)

package main

import "fmt"
import "time"

func main() {
	//채널(Channel) 셀렉트 구문
	//채널 Select 구문 -> 채널에 값이 수신되면 해당 case 문 실행
	//일회성 구문이므로, For(반복문)안에서 수행
	//default 구문 처리 주의

	//예제1
	ch1 := make(chan int)
	ch2 := make(chan string)

	go func() {
		for {
			ch1 <- 77
			time.Sleep(250 * time.Millisecond)
		}
	}()

	go func() {
		for {
			ch2 <- "Golang Hi!"
			time.Sleep(500 * time.Millisecond)
		}
	}()

	go func() {
		for {
			select {
			case num := <-ch1:
				fmt.Println("ch1 : ", num)
			case str := <-ch2:
				fmt.Println("ch2 : ", str)
				//default:
				//fmt.Println("default test")
			}
		}
	}()

	time.Sleep(7 * time.Second)
}

```

```
//채널(Channel) 심화(5)

package main

import "fmt"
import "time"

func main() {
	//채널(Channel)

	//예제1
	ch1 := make(chan int)
	ch2 := make(chan string)

	go func() {
		for {
			num := <-ch1 //값 수신
			fmt.Println("ch1 : ", num)
			time.Sleep(250 * time.Millisecond)
		}
	}()

	go func() {
		for {
			ch2 <- "Golang Hi!" //값 발신
			time.Sleep(500 * time.Millisecond)
		}
	}()

	go func() {
		for {
			select {
			case ch1 <- 777: //발신용도
			case str := <-ch2:
				fmt.Println("ch2 : ", str)
			}
		}
	}()
	time.Sleep(7 * time.Second)
}

```
