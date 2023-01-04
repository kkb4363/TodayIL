# reduce 메서드

- reduce 메서드는 4가지의 인수를 가진다.
1. accumulator = 축적값
2. currentValue = 배열의 현재 요소
3. index = 배열의 현재 요소의 인덱스
4. array = 호출한 배열

- 최초 함수 실행 시 accumulator , 즉 초기값을 제공하지 않으면 배열의 첫 번째 요소를 사용하고, 빈 배열에서 초기값이 없을 경우 에러가 발생한다.

```
// 예제1 : 배열의 모든 값 더하기
const numbers = [1,2,3,4,5];
const sum = numbers.reduce((a,b) => a + b)
=> sum = 15


// 예제2 : 오브젝트 배열에서 원하는 항목의 값만 더하기
const friends = [
    {
        name:'a',
        age:32
    },
    {
        name:'b',
        age:25
    },
    {
        name:'c',
        age:15
    }
]

const ageSum = friends.reduce((a,b) => {
    return a + b.age;
},0);
=> ageSum = 72

```