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
