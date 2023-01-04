# sort()
- sort 메서드는 배열의 요소를 정렬하는데 사용하는 함수다.

```
const String = ['b','c','a'];
String.sort();
=> [a,b,c]

const Digit = [11,2,5,20,8];
Digit.sort();
=> [11,2,20,5,8]
=> sort()는 기본적으로 유니코드값으로 정렬하기 때문에 예상과 다르게 11,2,20,5,8로 정렬된다.

=> 그러므로 숫자를 정렬하려면 아래처럼 해야함.
Digit.sort(a,b) => a-b; // 오름차순
Digit.sort(a,b) => b-a; // 내림차순
```

- 이해가 안된다면 아래 블로그 참조
- https://velog.io/@mystyle730/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-Sort%ED%95%A8%EC%88%98-%EC%9D%B4%ED%95%B4