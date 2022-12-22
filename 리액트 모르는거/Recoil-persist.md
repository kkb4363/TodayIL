# Recoil-persist
- localstorage나 sessionstorage에 값을 저장,사용할 때 씀

## 사용법
1. npm i recoil-persist
2. 코드 예시
```
import {recoilPersist} from 'recoil-persist';

const {persistAtom} = recoilPersist({
    key:'toDoLocal',
    storage:localStorage,
})

export const toDoState = atom<ITodo[]>({
    key:'toDo',
    default:[],
    effects_UNSTABLE:[persistAtom],
})
```