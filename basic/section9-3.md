# section9-3

### 동기화(Sync)

```
//고루틴 동기화 기초(1)

package main

import (
	"fmt"
	"runtime"
)

//구조체 선언(공유 데이터)
type count struct {
	num int
}

func (c *count) increment() {
	c.num += 1
}

func (c *count) result() {
	fmt.Println(c.num)
}

func main() {
	//고루틴 동기화 예제
	//실행 흐름 제어 및 변수 동기화 가능
	//공유 데이터 보호가 가장 중요

	//동기화 사용하지 않은 경우 예제
	// 시스템 전체 cpu 사용
	runtime.GOMAXPROCS(runtime.NumCPU())

	c := count{num: 0}
	done := make(chan bool)

	for i := 1; i <= 10000; i++ {
		go func() {
			c.increment()
			done <- true
			runtime.Gosched() //Cpu 양보
		}()
	}

	for i := 1; i <= 10000; i++ {
		<-done
	}

	c.result()
}

```

```
//고루틴 동기화 기초(2)

package main

import (
	"fmt"
	"runtime"
	"sync"
)

//구조체 선언(공유 데이터)
type count struct {
	num   int
	mutex sync.Mutex
}

func (c *count) increment() {
	//공유 데이터 수정 전 뮤텍스로 보호
	c.mutex.Lock()
	c.num += 1
	//공유 데이터 수정 후 보호 해제
	c.mutex.Unlock()
}

func (c *count) result() {
	fmt.Println(c.num)
}

func main() {
	//고루틴 동기화 예제
	//실행 흐름 제어 및 변수 동기화 가능
	//공유 데이터 보호가 가장 중요
	//뮤텍스(Mutex) : 여러 고루틴에서 작업하는 공유데이터 보호
	//sync.Mutex 선언 후 Lock, Unlock 사용

	//동기화 사용한 예제
	// 시스템 전체 cpu 사용
	runtime.GOMAXPROCS(runtime.NumCPU())

	c := count{num: 0}
	done := make(chan bool)

	for i := 1; i <= 10000; i++ {
		go func() {
			c.increment()
			done <- true
			runtime.Gosched() //Cpu 양보
		}()
	}

	for i := 1; i <= 10000; i++ {
		<-done
	}

	c.result()
}

```

```
//고루틴 동기화 기초(3)

package main

import (
	"fmt"
	"runtime"
	"time"
)

func main() {
	//뮤텍스 : 상호 배제 -> Thread(고루틴)들이 서로 running time에 서로 영향을 주지 않게 즉, 단독으로 실행되게 하는 기술
	//뮤텍스 : 여러 고루틴에서 작업하는 공유 데이터 보호

	//동기화 사용하지 않은 경우 예제
	//쓰기 읽기 동작 순서가 일정하지 않아 잘못된 오류를 반환 할 가능성 증가
	//시스템 전체 cpu 사용
	runtime.GOMAXPROCS(runtime.NumCPU())

	data := 0

	go func() {
		for i := 1; i <= 10; i++ {
			data += 1
			fmt.Println("Write : ", data)
			time.Sleep(200 * time.Millisecond)
		}
	}()

	go func() {
		for i := 1; i <= 10; i++ {
			fmt.Println("Read1 : ", data)
			time.Sleep(1 * time.Second)

		}
	}()

	go func() {
		for i := 1; i <= 10; i++ {
			fmt.Println("Read2 : ", data)
			time.Sleep(1 * time.Second)
		}
	}()

	time.Sleep(10 * time.Second)

}

```

```
//고루틴 동기화 기초(4)

package main

import (
	"fmt"
	"runtime"
	"sync"
	"time"
)

func main() {
	//뮤텍스 : 상호 배제 -> Thread(고루틴)들이 서로 running time에 서로 영향을 주지 않게 즉, 단독으로 실행되게 하는 기술
	//뮤텍스 : 여러 고루틴에서 작업하는 공유 데이터 보호
	//RWMutex : 쓰기 Lock -> 쓰기 시도 중에는 다른 곳에서 이전 값을 읽으면 X, 읽기 락 , 쓰기 락 전부 방어(방지)
	//RMutex : 읽기 lock -> 읽기 시도 중에 값이 변경 방지 즉, 쓰기 락 방어(방지)

	//동기화 사용하지 않은 경우 예제
	//쓰기 읽기 동작 순서가 일정하지 않아 잘못된 오류를 반환 할 가능성 증가
	//시스템 전체 cpu 사용
	runtime.GOMAXPROCS(runtime.NumCPU())

	data := 0
	mutex := new(sync.RWMutex) //var mutex = new(sync.RWMtex)

	go func() {
		for i := 1; i <= 10; i++ {
			//쓰기 뮤텍스 잠금
			mutex.Lock()
			data += 1
			fmt.Println("Write : ", data)
			time.Sleep(200 * time.Millisecond)
			//쓰기 뮤텍스 잠금 해제
			mutex.Unlock()
		}
	}()

	go func() {
		for i := 1; i <= 10; i++ {
			//읽기 뮤텍스 잠금
			mutex.RLock()
			fmt.Println("Read1 : ", data)
			time.Sleep(1 * time.Second)
			//읽기 뮤텍스 해제
			mutex.RUnlock()

		}
	}()

	go func() {
		for i := 1; i <= 10; i++ {
			//읽기 뮤텍스 잠금
			mutex.RLock()
			fmt.Println("Read2 : ", data)
			time.Sleep(1 * time.Second)
			//읽기 뮤텍스 해제
			mutex.RUnlock()
		}
	}()

	time.Sleep(10 * time.Second)

}

```

```
//고루틴 동기화 기초(5)

package main

import (
	"fmt"
	"runtime"
	"sync"
	"time"
)

func main() {
	//고루틴 동기화 객체
	//동기화 상태(조건) 메소드 사용
	//Wait , notify , notifyAll : 기타 언어
	//Wait , Signal , Broadcas

	// 시스템 전체 CPU 사용
	runtime.GOMAXPROCS(runtime.NumCPU())

	var mutex = new(sync.Mutex)
	var condition = sync.NewCond(mutex)

	c := make(chan int, 5) //비동기 버퍼 채널

	for i := 0; i < 5; i++ {
		go func(n int) {
			mutex.Lock()
			c <- 777
			fmt.Println("Goroutine Wating : ", n)
			condition.Wait() //고루틴 대기(멈춤)
			fmt.Println("Wating End : ", n)
			mutex.Unlock()
		}(i)
	}

	for i := 0; i < 5; i++ {
		<-c
		//fmt.Println("received : ", <-c)
	}

	/*
		for i := 0; i < 5; i++ {
			mutex.Lock()
			fmt.Println("Wake Goroutine(Signal) : ", i)
			condition.Signal() //한 개 씩 깨움(모든 고루틴 생성 후)
			mutex.Unlock()
		}
	*/

	mutex.Lock()
	fmt.Println("Wake Goroutine(Broadcast)")
	condition.Broadcast()
	mutex.Unlock()

	time.Sleep(2 * time.Second)

}

```



```
//고루틴 동기화 고급(1)

package main

import (
	"fmt"
	"runtime"
	"sync"
	"time"
)

func onceTest() {
	//이 부분에 한 번 실행 할 코드 작성
	fmt.Println("Once Test Excute!")
}

func main() {
	//고루틴 동기화 고급
	//Once : 한 번만 실행(주로 초기화에 사용)
	//Do로 실행

	runtime.GOMAXPROCS(runtime.NumCPU())

	once := new(sync.Once) //Once 객체 생성

	for i := 0; i < 5; i++ {
		go func(n int) {
			fmt.Println("Goroutine : ", n)
			once.Do(onceTest)
		}(i)
	}

	time.Sleep(2 * time.Second)

}

```

```
//고루틴 동기화 고급(2)

package main

import (
	"fmt"
	"sync"
)

func main() {
	//고루틴 동기화 고급
	//대기 그룹
	//실행 흐름 변경(고루틴이 종료 될 때 까지 대기 기능)
	//WaitGroup : Add(고루틴 추가), Done(작업 종료 알림), Wait(고루틴 종료시 까지 대기)
	//Add로 추가 된 고루틴 개수와 Done으로 종료되는 알림 횟수 같아야 정확하게 동작한다. (Add == Done)

	wg := new(sync.WaitGroup)

	for i := 0; i < 100; i++ {
		wg.Add(1)
		go func(n int) {
			fmt.Println("WaitGroup : ", n)
			wg.Done()
		}(i)
	}

	//Add == Done 횟수 같아야 함
	wg.Wait()
	fmt.Println("WaitGroup End!")

}

```

```
//고루틴 동기화 고급(3)

package main

import (
	"fmt"
	"runtime"
	"sync"
)

func main() {
	//고루틴 동기화 고급
	//원자성 사용 -> 기능적으로 분할 불가능한 완전 보증된 일련의 조작, 모두 성공하거나, 모두 실패
	//모든 조작이 완료 될 때까지 다른 프로세스 개입 불가
	//sync/atomic에서 원자적 연산자 제공
	//https://golang.org/pkg/sync/atomic 에서 계열 확인 가능
	//주로 공용 변수에 관한 계산 사용

	//원자성 사용 안할 경우 예제
	runtime.GOMAXPROCS(runtime.NumCPU())

	var cnt int64 = 0
	wg := new(sync.WaitGroup)

	for i := 0; i < 5000; i++ {
		wg.Add(1)
		go func(n int) {

			cnt += 1
			wg.Done()
		}(i)
	}

	for i := 0; i < 2000; i++ {
		wg.Add(1)
		go func(n int) {
			cnt -= 1
			wg.Done()
		}(i)
	}

	//Add(7000) == Done(7000) 횟수 같아야 함
	wg.Wait()
	fmt.Println("WaitGroup End! Cnt? >>>>> ", cnt)

}

```

```
//고루틴 동기화 고급(3)

package main

import (
	"fmt"
	"runtime"
	"sync"
	"sync/atomic"
)

func main() {
	//고루틴 동기화 고급
	//원자성 사용 -> 기능적으로 분할 불가능한 완전 보증된 일련의 조작, 모두 성공하거나, 모두 실패
	//모든 조작이 완료 될 때까지 다른 프로세스 개입 불가
	//sync/atomic에서 원자적 연산자 제공
	//https://golang.org/pkg/sync/atomic 에서 계열 확인 가능
	//주로 공용 변수에 관한 계산 사용

	//원자성 사용 안할 경우 예제
	runtime.GOMAXPROCS(runtime.NumCPU())

	var cnt int64 = 0
	wg := new(sync.WaitGroup)

	for i := 0; i < 5000; i++ {
		wg.Add(1)
		go func(n int) {

			//cnt += 1
			atomic.AddInt64(&cnt, 1)
			wg.Done()
		}(i)
	}

	for i := 0; i < 2000; i++ {
		wg.Add(1)
		go func(n int) {
			//cnt -= 1
			atomic.AddInt64(&cnt, -1)
			wg.Done()
		}(i)
	}

	//Add(7000) == Done(7000) 횟수 같아야 함
	wg.Wait()

	finalCnt := atomic.LoadInt64(&cnt)
	//방법1
	fmt.Println("WaitGroup End! Cnt? >>>>> ", cnt)
	//방법2 추천
	fmt.Println("WaitGroup End! Cnt? >>>>> ", finalCnt)

}

```


