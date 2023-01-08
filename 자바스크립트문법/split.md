# split() 함수
- string.split(separator,limit)
- split 함수는 문자열을 separator로 잘라서 limit 크기 이하의 배열에 잘라진 문자열을 저장해 리턴한다.
- separator는 필수 아님 , 문자열을 잘라 줄 구분자, 값이 입력되지 않으면 문자열 전체를 배열에 담아서 리턴한다.
- limit도 필수 아님

```
예시1) 파라미터를 입력하지 않은 경우
const str = 'apple banana orange';
const str = str.split();
=> apple banana orange

예시2) separator 활용하는 경우
const str = 'apple banana orange';
const str = str.split(' ');
=> [apple, banana, orange]
```