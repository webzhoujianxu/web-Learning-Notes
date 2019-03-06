**第一次学习react,刚用react-create-app搭建了一个项目第一点想先去找路由**

于是乎百度搜索了一下react的路由, 找到了react-dom-router

```
npm i react-router-dom -s
```

 [官方文档](https://reacttraining.com/react-router/web/guides/quick-start)  翻阅了下

首先看到的是如下代码

```javascript
import React from "react";
import { BrowserRouter as Router, Route, Link } from "react-router-dom";

function Index() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function Users() {
  return <h2>Users</h2>;
}

function AppRouter() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about/">About</Link>
            </li>
            <li>
              <Link to="/users/">Users</Link>
            </li>
          </ul>
        </nav>

        <Route path="/" exact component={Index} />
        <Route path="/about/" component={About} />
        <Route path="/users/" component={Users} />
      </div>
    </Router>
  );
}

export default AppRouter;

```

wtf? 最开始的时候有点蒙圈.因为在使用vue-router的时候都定义在一个公用文件里面然后注入vue实例。

仔细阅读了下

```javascript
 <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about/">About</Link>
            </li>
            <li>
              <Link to="/users/">Users</Link>
            </li>
          </ul>
        </nav>

        <Route path="/" exact component={Index} />
        <Route path="/about/" component={About} />
        <Route path="/users/" component={Users} />
      </div>
    </Router>
```

似乎跟render dom放在了一起 用router 包裹一下  

```javascript
 <Route path="/" exact component={Index} />
```

这部分就是在定义路由 指定对应组件

