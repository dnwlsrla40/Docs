# Redux & Redux-saga

## Redux-saga

- 리덕스는 action -> reducer -> store 같이 동기적인 순서로 데이터를 변경합니다.
- 그런데 서버와의 네트워크 통신, 타이머 이벤트 같은 비동기 요소를 주입해야 되는 경우가 있습니다.
- 물론 useEffect에서 try...catch, axios, fetch API를 사용해서 억지로 할 수 있지만, 코드가 난잡해지고 관리하기가 불편합니다.
- 그래서 리덕스의 동기적인 데이터 처리 과정에, 비동기적인 상황을 제어 할 수 있는 라이브러리를 추가해줍니다. 그것이 Redux-Saga이며, 이를 사용했을 때 대표적인 장점은 아래와 같습니다.
  - 비동기 상황을 손쉽게 제공해주기 때문에, useEffect에서 try...catch, axios, fetch API를 억지로 사용했을 때 보다 code의 가독성이 올라간다.
  - 여러 컴포넌트에서 발생하는 비동기 상황을 하나의 file에서 관리 할 수 있다.

## Redux-Saga Method

- 기본적으로 Redux-Saga는 자바스크립트의 일반 함수가 아닌, 제너레이터 함수에서 동작합니다.
  - https://velog.io/@rohkorea86/Generator-%ED%95%A8%EC%88%98%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%B4%EB%B3%B4%EC%9E%90-%EC%9D%B4%EB%A1%A0%ED%8E%B8-%EC%99%9C-%EC%A0%9C%EB%84%A4%EB%A0%88%EC%9D%B4%ED%84%B0-%ED%95%A8%EC%88%98%EB%A5%BC-%EC%8D%A8%EC%95%BC-%ED%95%98%EB%8A%94%EA%B0%80
- 많은 메서드들을 제공해주지만, 이번 프로젝트에서는 일부만 사용 할 예정입니다
  - all : 여러 이팩트를 동시에 실행시킬 때 사용. 일반적으로 file을 export default으로 전달할 때, 제너레이터 함수를 하나로 묶는 역할에 사용
  - takeLatest : 동일한 이벤트가 여러번 발생했을 때, 맨 마지막에 발생한 이벤트만 받아들이는 함수
  - call : 비동기적인 상황을 동기적으로 바꾸고 싶을 때 사용. 서버 API 요청을 보내고 처리되는 것을 기다릴 때 사용
  - put : 리덕스에서 dispatch와 같은 역할
- Redux-Saga의 작성 패턴은 3가지입니다
  - 1.request action을 catch하는 제너레이터 함수
  - 2.성공 및 실패를 처리하는 제너레이터 함수
  - 3.API 통신을 담당하는 일반 함수

## Redux-Saga 동작 과정

- 1.특정 상황에서 리덕스 action 발생

  - code에서는 useEffect가 발생했을 때 인기 tags를 불러오는 상황으로 가정

    ```javascript
    // 최초로 게시글들을 불러오는 useEffect
    useEffect(() => {
      dispatch({
        type: LOAD_TOP_10_TAGS_REQUEST,
        data: "test",
      });
    }, []);
    ```

- 2.Redux-saga에서 LOAD_TOP_10_TAGS_REQUEST를 캐치

  - request를 catch하는 함수 이름을 작성할 때 "watch"를 붙여줌
  - takeLatest : 중복되는 이벤트가 발생했을 때, 맨 마지막 이벤트만 catch하는 함수
  - watchLoadTop10Tags() 함수는 맨 하단에 export default function\*의 all() 배열에 추가해줌

  ```javascript
  [redux action을 캐치하는 함수]
  function* watchLoadTop10Tags() {
    yield takeLatest(LOAD_TOP_10_TAGS_REQUEST, loadTop10Tags);
  }
  ```

  ```javascript
  [watchLoadTop10Tags all 메서드에 추가]
  export default function* () {
    yield all([fork(watchLoadPosts), fork(loadTop10Tags)]);
  }
  ```

- 3.성공 및 실패를 처리하는 제너레이터 함수 생성

  - 비동기 상황에서 에러 처리를 할 수 있도록 try...catch 사용
  - call : 서버의 성공 및 실패의 값을 기다리기 위해, 비동기적인 상황을 동기적인 상황으로 전환
  - put : 마치 redux에서 dispatch와 같은 역할. 특정 action을 redux-saga가 redux에게 전달해줌

    ```javascript
    // actions
    import { LOAD_TOP_10_TAGS_SUCCESS } from "store/actions/postAction";
    import { LOAD_TOP_10_TAGS_FAILURE } from "store/actions/postAction";

    function* loadTop10Tags(action) {
      try {
        // call : 서버 결과값 기다림
        // acion.data : 상단 useEffect에서 dispatch 됐을 때, 객체값이 action에 들어옵니다
        const result = yield call(loadTop10TagsApi, acion.data);
        // put : 리덕스에게 action 전달
        yield put({
          type: LOAD_TOP_10_TAGS_SUCCESS,
          data: result.data,
        });
      } catch (error) {
        yield put({
          type: LOAD_TOP_10_TAGS_FAILURE,
          data: error.response.data,
        });
      }
    }
    ```

- 4.API 함수 생성

  - 이때는 제너레이터 함수가 아니고 일반 함수입니다
  - 여기서 axios를 사용해서 REST API 규약에 맞춰서 서버에게 값을 전달합니다.
  - const result = yield call(loadTop10TagsApi);가 값을 획득하기 위해, 결과값을 return해줍니다.

    ```javascript
    function loadPostsApi(/*call()이 실행됐을 때 두번 째 인자가 여기로 들어 옴*/) {
      return axios.get(`/top10Tags`);
    }
    ```

- 5.서버에서 결과값 전달
  - yield put()을 통해 서버의 결과값을 리덕스에게 전달해줍니다.
  - initialState에다가 서버의 결과값을 받기 위한 property를 추가해줍니다.
  - immer를 사용해서 불변성을 지킬 필요없이 자바스크립트의 메서드로 값을 추가해줄 수 있습니다.

```javascript
const initialState = {
  posts: [],
  recentPosts: [],
  notices: [], // 공지사항 배열 추가
  top10Tags: [], // 인기 태그 배열 추가
  hello: true, // 그냥 임의로 만들어 봤어요
};

const PostReducer = (state = initialState, action) => {
  return immer(state, (draft) => {
    switch (action.type) {
      /* ......
        위에는 여러개의 case가 있다고 가정해주세요
        ......
      */
      // 인기 태그 load 요청
      case LOAD_TOP_10_TAGS_REQUEST: {
        draft.hello = true;
        break;
      }
      // 인기 태그 load 성공
      case LOAD_TOP_10_TAGS_SUCCESS: {
        draft.hello = true;
        draft.top10Tags.push(action.data);
        break;
      }
      // 인기 태그 load 실패
      case LOAD_TOP_10_TAGS_FAILURE: {
        draft.hello = false;
        break;
      }
      default: {
        break;
      }
    }
  });
};
```

## redux-saga 예제 전체 code

```javascript
function loadPostsApi(data) {
  return axios.get(`/top10Tags`);
}

function* loadTop10Tags(action) {
  try {
    const result = yield call(loadTop10TagsApi, action.data);
    yield put({
      type: LOAD_TOP_10_TAGS_SUCCESS,
      data: result.data,
    });
  } catch (error) {
    yield put({
      type: LOAD_TOP_10_TAGS_FAILURE,
      data: error.response.data,
    });
  }
}

function* watchLoadTop10Tags() {
  yield takeLatest(LOAD_TOP_10_TAGS_REQUEST, loadTop10Tags);
}

export default function* () {
  yield all([fork(watchLoadPosts), fork(loadTop10Tags)]);
}
```
