# section4


### 공통 사용자 lib

```
//라이브러리 및 접근제어(1)
package lib

func CheckNum(c int32) bool {
	return c > 10
}

```
```
//라이브러리 및 접근제어(2)
package lib

func CheckNum1(c int32) bool {
	return c > 100
}

// private 소문자로 시작
func checkNum2(c int32) bool {
	return c > 1000
}

```

### init
```
//GO 초기화 함수(1)
package main

import (
	"fmt"
)

func init() {
	fmt.Println("Init is being executed")
}

func main() {
	//init : 패키지 로드 시에 가장 먼저 호출
	//가장 먼저 초기화 되는 작업 작성 시 유용하다.
	fmt.Println("Main Source Code!!")
}

```

```
//GO 초기화 함수(2)
package main

import (
	"fmt"
)

func init() {
	fmt.Println("Init1 is being executed")
}

func init() {
	fmt.Println("Init2 is being executed")
}

func init() {
	fmt.Println("Init3 is being executed")
}

func main() {
	fmt.Println("Main Source Code!")
}

```
```
//GO 초기화 함수(3)
package main

import (
	"fmt"
	"basic/section04/lib"
)

var num int32

//변수 초기화
func init() {
	num = 30
}

func main() {
	fmt.Print("10 보다 큰 수? :  ", lib.CheckNum(num))
}

```

### 접근제어 (access)

```
//패키지 접근제어(1)
package main

import (
	"basic/section04/lib2"
	"fmt"
)

func main() {
	//패키지 접근제어
	//변수,상수,함수,메서드,구조체 등 식별자
	//대문자 : 패키지 외부 접근 가능
	//소문자 : 패키지 외부 접근 불가(패키지 내에서만 접근 가능)

	fmt.Print("100 보다 큰 수? :  ", lib.CheckNum1(101))
//	fmt.Print("1000 보다 큰 수? :  ", lib.checkNum2(1001)) //예외 발생 (접근 불가)

}

```

```
//패키지 접근제어(2)
package main

import (
	"fmt"
	_ "basic/section04/lib"        //빈 식별자 사용
	testlib "basic/section04/lib2" //별칭 사용
)

func main() {
	//패키지 접근제어
	//별칭 사용
	//빈 식별자 사용

	fmt.Print("100 보다 큰 수? :  ", testlib.CheckNum1(101))
}

```

### 패키지(pakage)
```
//패키지(1)
package main

//선언 방법1
/*
import "fmt"
import "os"
*/

//선언 방법2
import (
	"fmt"
	"os"
)

func main() {
	//패키지 : 코드 구조화 및 재사용
	//Go는 패키지로 구성되어 있음
	//서로 다른 패키지간에 서로 import 후 사용
	//패키지 이름 = 디렉터리 이름
	//같은 패키지 내 -> 소스파일 같은 디렉터리 위치
	//네이밍 규칙 : 소문자, 패키지명 = 소스파일명

	var name string

	fmt.Print("이름은? :  ")

	fmt.Scanf("%s", &name)

	fmt.Fprintf(os.Stdout, "Hi %s\n", name)

}

```

```
//패키지(2)
package main

import (
	"fmt"
	"basic/section04/lib"
)

func main() {
	//패키지 종류
	//1.메인 프로그램(main)
	//2.다른 패키지에서 호출 가능한 라이브러리

	fmt.Print("10 보다 큰 수? :  ", lib.CheckNum(15))

}

```
