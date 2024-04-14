# webpack.config.js
**ckeditor**
https://ckeditor.com/docs/ckeditor5/latest/installation/index.html
https://quynhweb.pro/ckeditor-la-gi/
Đây là trình soạn thảo theo mã nguồn mở theo kiểu WYSIWYG CKSource. Để chạy được chún ta chỉ cần tích hợp vào website là có thể chạy được.

Ckeditor là mã nguồn mở được viết bằng JavaScript vì thế ai cũng có thể chỉnh sửa được. Và bên cạnh đó nó cũng tương thích với mọi trình duyệt như Chrome, Firefox, Opera…
**# WYSIWYG (what you see is what you get)**
WYSIWYG (pronounced wiz-ee-wig) is a type of editing software that allows users to see and edit content in a form that appears as it would when displayed on an interface, webpage, slide presentation or printed document. WYSIWYG is an acronym for "what you see is what you get."

**web-pack**
https://webpack.js.org/concepts/
Len day ma doc

# config.overrides.js
**How to update webpack config for a react project created using create-react-app?**
https://stackoverflow.com/questions/63280109/how-to-update-webpack-config-for-a-react-project-created-using-create-react-app

**customize-cra**
https://github.com/arackaf/customize-cra
customize-cra takes advantage of react-app-rewired's config-overrides.js file. By importing customize-cra functions and exporting a few function calls wrapped in our override function, you can easily modify the underlying config objects (webpack, webpack-dev-server, babel, etc.) that make up create-react-app.

**customize-cra-react-refresh**
https://github.com/pmmmwh/react-refresh-webpack-plugin
A Webpack plugin to enable "Fast Refresh" (also previously known as Hot Reloading) for React components.

# App.tsx
**React-query**
https://tanstack.com/query/v4/docs/overview

Out of the box, React applications do not come with an opinionated way of fetching or updating data from your components so developers end up building their own ways of fetching data. This usually means cobbling together component-based state and effect using React hooks, or using more general purpose state management libraries to store and provide asynchronous data throughout their apps.

While most traditional state management libraries are great for working with client state, they are not so great at working with async or server state. This is because server state is totally different

**Suspend**
https://reactjs.org/docs/code-splitting.html
Any component may suspend as a result of rendering, even components that were already shown to the user. In order for screen content to always be consistent, if an already shown component suspends, React has to hide its tree up to the closest `<Suspense>` boundary. However, from the user’s perspective, this can be disorienting.

**React.memo**
If your component renders the same result given the same props, you can wrap it in a call to React.memo for a performance boost in some cases by memoizing the result. This means that React will skip rendering the component, and reuse the last rendered result.

React.memo only checks for prop changes. If your function component wrapped in React.memo has a useState, useReducer or useContext Hook in its implementation, it will still rerender when state or context change.

# setupTest.ts
**@testing-library/jest-dom/extend-expect**
https://github.com/testing-library/jest-dom
Custom jest matchers to test the state of the DOM

# seerviceWorker.ts
**# Service Worker API**
https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API
Service workers essentially act as proxy servers that sit between web applications, the browser, and the network (when available). They are intended, among other things, to enable the creation of effective offline experiences, intercept network requests and take appropriate action based on whether the network is available, and update assets residing on the server. They will also allow access to push notifications and background sync APIs.

# index.ts
**React.StrictMode**
https://reactjs.org/docs/strict-mode.html
`StrictMode` is a tool for highlighting potential problems in an application. Like `Fragment`, `StrictMode` does not render any visible UI. It activates additional checks and warnings for its descendants.

**React router**
https://v5.reactrouter.com/web/guides/quick-start
To get started with React Router in a web app, you’ll need a React web app. If you need to create one, we recommend you try [Create React App](https://github.com/facebook/create-react-app). It’s a popular tool that works really well with React Router.

**BrowserRouter**
https://v5.reactrouter.com/web/api/BrowserRouter
A Router that uses the HTML5 history API (pushState, replaceState and the popstate event) to keep your UI in sync with the URL.

# routes.tsx 
**React.lazy()**
**Code splitting**
http://thaunguyen.com/blog/reactjs/reactjs-code-splitting-la-gi

# LoginContainer.tsx
