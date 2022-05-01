---
title: '[筆記]_React-Router'
date: 2022-04-27 01:16:54
tags: [筆記, React]
---

<small>Version: 2021/11 v6.0.0</small>
<!-- more -->

## React Router v6簡介
  React Router 於 2021年底發佈了 v6 的穩定版，
  由於v6含有大量 Hook，需依賴於 React v16.8以上版本。

## 安裝
  ```sh
    npm install react-router-dom@6
  ```

---

## 主要組件
  - ### 路由器設置
    - #### BrowserRouter
      使用常規URL路徑，
      如 `https://reactrouter.com/docs/en/v6`。
      切換url時會發送 request 到 server端，
      server端必須有對應的response(在server端設定)。
      一般來說，在SPA(單頁應用)中，除了API 以外的 request，
      server 都應回傳 index.html。
      ```jsx
        import { BrowserRouter } from 'react-router-dom';

        ReactDOM.render(
          <BrowserRouter>
            <App />
          </BrowserRouter>,
          root
        );
      ```
    - #### HashRouter
      使用當前位置，頁面路徑會加上『＃』，
      如 `https://reactrouter.com/#/docs/en/v6`。
      換url時不會發送request。僅在前端置換頁面。
      ```jsx
        import { HashRouter } from 'react-router-dom';

        ReactDOM.render(
          <HashRouter>
            <App />
          </HashRouter>,
          root
        );
      ```
  
  - ### 路由匹配
    - #### Route
      用來定義路徑與component的關係。
      有兩個主要參數：`path`、`element`。
        - `path`：設定對應路徑。
        - `element`：欲渲染的 component。
    
      ```jsx
        <Route path="/about" element={ <About /> }>
      ```
    - #### Routes
      為 舊版的 `Switch` 組件的升級版。
      Routes 會查看所有 `<Route>` 元素，找到與目前路徑匹配的子項目。
      ```jsx
        <Routes>
          <Route path="/" element={ <Dashboard /> }>
            <Route path="messages" element={ <DashboardMessages /> } />
            <Route path="tasks" element={ <DashboardTasks /> } />
            <Navigate to="/about" replace="{ true }">   // 重導向
          </Route>
          <Route path="/about" element={ <AboutPage /> } />
        </Routes>
      ```
    
  - ### 導航
    - #### Link
      用於創建連結導向，`<Link>`會生成 `<a>` 元素。
      ```jsx
        <Link to="/product"> 商品頁 </Link>
      ```
    - #### NavLink
      Link 的加強版，當路徑與`NavLink`對應時，會附帶一個 active 表示頁面正在作用中的參數。
      方便製作 active 效果。
      ```jsx
        <NavLink
          to="/messages"
          className={
            ({ isActive }) => isActive ? 'active' : ''
          }
        >
      ```

---

## 應用範例
  - ### 一般路由
    ```jsx
      import * as React from "react";
      import * as ReactDOM from "react-dom";
      import {
        BrowserRouter,
        Link,
        Routes,
        Route
      } from "react-router-dom";

      function App() {
        return (
          <>
            <nav>
              <Link to="/">home</Link>
              <Link to="/product">product</Link>
            </nav>
            <Routes>
              <Route path="/" element={<Home />} />
              <Route path="/product" element={<Product />} />
            </Routes>
          </>
        )
      }
      ReactDOM.render(
        <BrowserRouter>
          <App />
        </BrowserRouter>,
        root
      );
    ```
  - ### 巢狀路由
    使用`Outlet`
    ```jsx
      import * as React from "react";
      import * as ReactDOM from "react-dom";
      import {
        BrowserRouter,
        Link,
        Routes,
        Route
      } from "react-router-dom";

      function App() {
        return (
          <>
            <nav>
              <Link to="/product">productIndex</Link>
              <Link to="/product/add">productAdd</Link>
              <Link to="/product/edit">productEdit</Link>
            </nav>
            <Routes>
              <Route path="/product" element={<Product />}>
                <Route index element={<Index />}>
                <Route path="add" element={<Add />}>
                <Route path="edit" element={<Edit />}>
              </Route>
            </Routes>
          </>
        )
      }

      function Product() {
        return (
          <>
            <h1>Product</h1>
            <Outlet />
          </>
        )
      }

      ReactDOM.render(
        <BrowserRouter>
          <App />
        </BrowserRouter>,
        root
      );
    ```

---

## 常用 Hook
  - ### `useLocation`
    會返回一個location Object物件，
    包含 pathname, search, hash, key, state 等資訊。
    ```jsx
      import { useLocation } from "react-router-dom";

      <Link to={{
        pathname: "/settings",
        state: {
          fromNavBar: true,
        }
      }}>

      let location = useLocation();
      console.log(location);
      // {
      //  "pathname": "/settings",
      //  "state": {
      //    "fromNavBar": true
      //  },
      //  "search": "",
      //  "hash": "",
      //  ...
      // }
    ```
  
  - ### `useNavigate`
    取代了 useHistory，第一個參數可以是路由或是數字，代表前往或是前進後退的頁數。
    ```jsx
      import { useNavigate } from "react-router-dom";
      let navigate = useNavigate();

      navigate('/home');
      navigate(-1);
      navigate('/success', { replace: true });
    ```
  
  - ### `useParams`
    取得URL中的參數。
    ```jsx
      import { useParams } from "react-router-dom";
      <Link to="/Product/123">
      <Router>
        <Route path="/Product/:id" component={ <Product /> }>
      </Router>

      let { id } = useParams();
    ```
  
  - ### `useRoutes`
    功能等同於 `<Routes>`，可用來製作 Router config。
    後面介紹Router config 用法。

---

## Router config 用法
  ```jsx
    import { BrowserRouter, useRoutes } from "react-router-dom";

    const routes = [
      {
        path: "/",
        element: <Dashboard />,
        children: [
          {
            path: "messages",
            element: <DashboardMessages />,
          },
          { path: "tasks", element: <DashboardTasks /> },
        ],
      },
      { path: "team", element: <AboutPage /> },
    ];

    function RenderRoutes() {
      const element = useRoutes(routes);
      return element;
    }

    function App() {
      return (
        ...
        <RenderRoutes />
        ...
      )
    };

    ReactDOM.render(
      <BrowserRouter>
        <App />
      </BrowserRouter>,
      root
    );
  ```

---

## 參考來源
  - [React Router v6 和 v5 有哪些地方不同?](https://ithelp.ithome.com.tw/articles/10282773)
  - [React Router v6 官網](https://reactrouter.com/)