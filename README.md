# React-Redux

## 2020.09.28

`yarn add redux`
`yarn add react-redux`
`yarn add react-router-dom`

## 2020.09.29

### mapStateToProps

```javascript
import React, { useState } from "react";
import { connect } from "react-redux";

function Home({ toDos }) {
  const [text, setText] = useState("");
  function onChange(e) {
    setText(e.target.value);
  }
  function onSubmit(e) {
    e.preventDefault();
    setText("");
  }
  return (
    <>
      <h1>To Do</h1>
      <form onSubmit={onSubmit}>
        <input type="text" value={text} onChange={onChange} />
        <button>Add</button>
      </form>
      <ul>{JSON.stringify(toDos)}</ul>
    </>
  );
}

// mapStateToProps? => Redux State로부터 Component에 props으로써 전달하는 메소드
// mapStateToProps에서 return 된 값이 Component의 props로 들어간다.
function mapStateToProps(state) {
  return { toDos: state };
}

// connect란? Component와 Store를 연결해주는 것.
export default connect(mapStateToProps)(Home);
```

### mapDispatchToProps

```javascript
import React, { useState } from "react";
import { connect } from "react-redux";
import { actionCreators } from "../store";

function Home({ toDos, addToDo }) {
  const [text, setText] = useState("");
  function onChange(e) {
    setText(e.target.value);
  }
  function onSubmit(e) {
    e.preventDefault();
    addToDo(text);
    setText("");
  }
  return (
    <>
      <h1>To Do</h1>
      <form onSubmit={onSubmit}>
        <input type="text" value={text} onChange={onChange} />
        <button>Add</button>
      </form>
      <ul>{JSON.stringify(toDos)}</ul>
    </>
  );
}

// mapStateToProps? => Redux State로부터 Component에 props으로써 전달하는 메소드
// mapStateToProps에서 return 된 값이 Component의 props로 들어간다.
function mapStateToProps(state) {
  return { toDos: state };
}

// Component에서 dispatch를 사용할 수 있게 해주는 메소드
function mapDispatchToProps(dispatch) {
  return {
    addToDo: (text) => dispatch(actionCreators.addToDo(text)),
  };
}

// connect란? Component와 Store를 연결해주는 것.
export default connect(mapStateToProps, mapDispatchToProps)(Home);

// mapStateToProps가 필요하지 않을경우에는?
// export default connect(null, mapDispatchToProps)(Home);
```
