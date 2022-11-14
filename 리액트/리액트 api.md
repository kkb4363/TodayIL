# XML -> JSON 변환하는법
- 동아리 프로젝트 중에 API를 호출해야하는 과제가 있었는데 
지금까지는 JSON으로만 API를 받아왔었다가 XML 로 API를 받아오려니깐 어떻게 해야할 지 몰라서 구글링을 하다 알게되었다.
- 우선 SERVER.JS로 익스프레스 인스턴스를 만들어야 한다.
- 결론 : express server를 사용하는 법이 있다.

# 비동기 vs 동기 
1. 비동기 : 동시에 일어나지 않는 것 (Asynchronous)
2. 동기 : 동시에 일어나는 것 (synchronous)
- 동기는 설계가 매우 간단하지만 결과가 주어질 때까지 아무것도 못하고 대기해야하는 단점이 있다.
- 비동기는 동기보단 복잡하지만 결과가 주어지는데 시간이 걸리더라도 그 시간동안 다른 작업을 할 수 있으므로 자원을 효율적으로 사용할 수 있다.

# axios vs await
- 참고 : https://velog.io/@gudwh14/5.-React-Javascript-axios-%EC%99%80-await-async

## axios 
- axios는 javascript 라이브러리 중 하나인 fetch api와 같은 비동기 통신 라이브러리이다.
- fetch 와 axios의 차이점은 axios는 req,res을 모두 json형식으로 자동으로 변환시켜 준다.
- axios를 이용하여 api호출을 하는 경우 바로 응답이 오지 않기에 일반적으로 비동기 방식을 사용한다. 


## async , await
- async&await은 javascript에서 가장 최근에 등장한 비동기 처리 패턴이다. async&await을 통해서 promise를 사용할 수 있다.
- Promise 객체는 비동기 작업이 끝난 후 결과를 알려주는 용도로 사용한다. 말 그대로 '비동기 작업 끝나면 알려주겠다고 약속할게' 라는 의미다. 
- promise 객체에 .then()을 붙이면 이행 상태의 처리를 할 수 있고, .catch를 붙이면 실패 상태를 처리할 수 있다.