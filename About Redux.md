# Redux ?

### Redux를 왜 쓰는가 ?
 - props라는 문법을 쓰지 않기 위해 
 - 상태 관리가 용이 

1. props 라는 문법을 쓰지 않기 위해란 무슨 말인가?
 - 우리는 리엑트를 사용하여 웹 개발을 할때에는 여러 가지 컴포넌트를 만들어 예를 들어
버튼 컴포넌트 또는 메뉴 컴포넌트 그리고 배경 컴포넌트등을 하나로 만들어 웹을 만드는 방식이다
그런데 웹을 만들다 보면 state(변수)를 만들고 싶어지는데 예를 들어 고객들의 몸무게를 저장하여 나타내주고 싶은데 
하나의 컴포넌트에 이 저장값을 집어 넣었을때 다른 곳의 컴포넌트에는 못쓴다고 한다 그래서 props 라는 문법을 사용하여 
다른 곳으로 넘겨주는 방식을 쓰고 있는데 하위 컴포넌트가 많으면 모두다  하나하나의 컴포넌트 안에 state를 사용하여 
넘겨 줘야 하는 번거 로움이 있다 만약 극단 적으로 1000개의 컨포넌트가 있다고 하면 그것을 다 넣어줘야 한다는 말
그래서 Redux를 설치를 하는 것이고 state를 보관하여 모든 컴포넌트에 프롭스를 없이 정보를 전달할 수 있다고 한다

2. 상태관리가 용이 해진다는 말은?
 - state 관리가 용이, 컴포넌트들이 몸무게 state를 변경하기 시작할때 예를 들어 컨포넌트 마다 어떠한 버튼을 누를시 
몸무게가 변경 된다고 하고 갑자기 몸무게 출력에 버그가 생겼다고 했을때 극단적으로 100만개의 변수가 있다고 하면 이것들 다 
찾으면 힘들 것이다. 그래서 Redux Store 부분에 state 수정방법을 올려 놓고 API를 만들때 component들은 수정 요청만 Redux에게 
하는 것이고 Redux는 수정된 자료만 넘겨주므로써 상태 관리 및 버그 관리에 용이 하게 된다.


### 사용 방법 

0. 저장방법 (index.js 파일)
 - import 로 {Provider},{createrStore} 를 각각 들고 온다
 - const 체중 = 100ㅣ;
1. 꺼내온것 
 - const 꺼내온거 = useSelector((state)=>state);
2. 컴포넌트에서 state 수정요청 하려면?
 - dispatch


# 리덕스 스토어는 user.js 파일
# Redux-Import
리덕스 관련 import code

yarn add redux react-redux redux-thunk redux-logger history@4.10.1 connected-react-router@6.8.0

yarn add immer redux-actions


# 이 밑 부터는 configureStore.js 에 

# Redux-store 만들기 
let store = (initialStore) => createStore(rootReducer, enhancer);

export default store();

# Rootreducer 만들기
const rootReducer = combineReducers({
  user: User,
});

# 미들웨어 준비 

const middlewares = [thunk];

// 지금이 어느 환경인 지 알려줘요. (개발환경, 프로덕션(배포)환경 ...)
const env = process.env.NODE_ENV;

// 개발환경에서는 로거라는 걸 하나만 더 써볼게요.
if (env === "development") {
  const { logger } = require("redux-logger");
  middlewares.push(logger);
}

# redux devTools 설정 
const composeEnhancers =
  typeof window === "object" && window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
    ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({
        // Specify extension’s options like name, actionsBlacklist, actionsCreators, serialize...
      })
    : compose;
    
# 미들웨어 묶기
const enhancer = composeEnhancers(
  applyMiddleware(...middlewares)
);


# import 하기 

import { createStore, combineReducers, applyMiddleware, compose } from "redux";
import thunk from "redux-thunk";
import { createBrowserHistory } from "history";
import { connectRouter } from "connected-react-router";

import User from "./modules/user";



