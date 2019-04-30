---
title: react-router 4.0 的非组件跳转
date: 2019-04-22 16:40:26
categories: 
    - web前端
tags:
    - react
    - 小功能
---

这次搭的脚手架用上了react-router 4.x,组件内的路由跳转可以用 `widthRouter`实现，非组件内的可以用以下方法

```
// src/history.js

import { createBrowserHistory } from 'history';

export default createBrowserHistory();
```
用 `import { Router }` 代替 `import { BrowserRouter as Router })`:

```
// src/index.jsx

// ...
import { Router, Route, Link } from 'react-router-dom';
import history from './history';

ReactDOM.render(
  <Provider store={store}>
    <Router history={history}>
      <div>
        <ul>
          <li><Link to="/">Home</Link></li>
          <li><Link to="/login">Login</Link></li>
        </ul>
        <Route exact path="/" component={HomePage} />
        <Route path="/login" component={LoginPage} />
      </div>
    </Router>
  </Provider>,
  document.getElementById('root'),
);
```

需要跳转的地方

```
// src/actions/userActionCreators.js

// ...
import history from '../history';

export function login(credentials) {
  return function (dispatch) {
    return loginRemotely(credentials)
      .then((response) => {
        // ...
        history.push('/');
      });
  };
}
```
[参考](https://stackoverflow.com/questions/42701129/how-to-push-to-history-in-react-router-v4)