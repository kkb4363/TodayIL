# Redux 로컬스토리지

- 새로 고침하면 Redux로 저장한 state들이 날아가는데 login 후 다음 페이지에서 새로고침해도 로그인 정보가 그대로 남길 바란다면
- Redux-persist를 이용하여 localstorage에 login상태를 저장한다.

1. PersistReducer 생성하기

- npm i redux-persist

2. reducer 코드 변경하기

```
import {combineReducers} from 'redux';
import {persistReducer} from 'redux-persist';
import 현재쓰는Reducer from '경로';
import storage from 'redux-persist/lib/storage';
// 세션 스토리지 사용하려면 import storage from 'redux-persist/lib/storage/session;

const persistConfig = {
    key:'아무거나',
    storage,
    whitelist:['현재쓰는Reducer']
};

const rootReducer = combineReducers({
    현재쓰는Reducer
});

export default persistReducer(persistConfig, rootReducer);
```

3. index.js 수정하기

```
import {persistStore} from 'redux-persist';
import {persistGate} from 'redux-persist/integration/react';

const persistor = persistStore(store);

ReactDOM.render(
    <Provider store={store}>
        <PersistGate persistor={persistor}>
            <React.StrictMode>
                <App />
            </React.StrictMode>
        </PersistGate>
    </Provider>, document.getElementById('root')
);
```
