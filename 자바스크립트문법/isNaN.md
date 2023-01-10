# isNaN() 함수

- 매개변수가 숫자인지 검사하는 함수이다.
- NaN은 Not a Number이다.

```
let a = 123.123 = false //숫자이므로 false
let b = '123' = false // 따옴표로 감쌌지만, 숫자로 취급
let c = 'gggg' = true // 숫자가 아니므로 true
let d = 123 * 123 = false // 숫자이므로
let e = '123 * 123' = true // 따옴표안에 문자가 있으므로 true

isNaN(a)
```

## 자바스크립트 인식 오류

- 자바스크립트에서는 숫자에 e가 붙으면 지수로 인식하여 문자인 경우도 그냥 숫자로 인식한다.
- 해결방법

```
let arr = '123e'
arr.every(c => isNaN(c));
// 모든 요소가 number이면 false리턴
```
