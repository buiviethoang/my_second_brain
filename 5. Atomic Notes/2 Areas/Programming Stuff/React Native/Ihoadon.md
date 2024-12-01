## redux-persist
https://viblo.asia/p/luu-redux-state-vao-local-storage-voi-redux-persist-3P0lPezv5ox
Redux Persist nhận vào Redux state object của bạn và lưu nó vào các bộ lưu trữ nội bộ. Sau đó khi app khởi động thì nó sẽ lấy các state này ra và lưu trở lại vào Redux.
## navigation.push
https://reactnavigation.org/docs/stack-actions/#:~:text=push%E2%80%8B,can%20be%20present%20multiple%20times
The push action adds a route on top of the stack and navigates forward to it. This differs from navigate in that navigate will pop back to earlier in the stack if a route of the given name is already present there. push will always add on top, so a route can be present multiple times.

name - string - Name of the route to push onto the stack.
params - object - Screen params to pass to the destination route.

## ?.
https://www.tutorialspoint.com/strange-syntax-what-does-mean-in-javascript
Now what happens to our chaining statement, it will yield a typeError saying cannot access property undefined of human. Does there exist any way in such situations to make our code not throw any errors. Yes, and this is where ‘?.’ aka optional chaining comes to our rescue.

What optional chaining does is quite simple, it behaves like normal chaining in normal conditions but when we try to access any property off of undefined instead of making our code to throw an error, it terminates the chaining then and there and returns undefined so that the remaining chunk of code functions normally

## StackActions.replace
https://reactnavigation.org/docs/stack-actions/
The replace action allows to replace a route in the navigation state. It takes the following arguments:

name - string - A destination name of the route that has been registered somewhere.
params - object - Params to pass to the destination route.

## Yup
https://github.com/jquense/yup
Yup is a schema builder for runtime value parsing and validation. Define a schema, transform a value to match, assert the shape of an existing value, or both. Yup schema are extremely expressive and allow modeling complex, interdependent validations, or value transformation.

## formik
https://formik.org/docs/overview
Let's face it, forms are really verbose in React. To make matters worse, most form helpers do wayyyy too much magic and often have a significant performance cost associated with them. Formik is a small library that helps you with the 3 most annoying parts:

Getting values in and out of form state
Validation and error messages
Handling form submission
By colocating all of the above in one place, Formik will keep things organized--making testing, refactoring, and reasoning about your forms a breeze.

## useFormik
https://formik.org/docs/api/useFormik
useFormik() is a custom React hook that will return all Formik state and helpers directly. Despite its name, it is not meant for the majority of use cases. Internally, Formik uses useFormik to create the Formik component (which renders a React Context Provider). If you are trying to access Formik state via context, use useFormikContext. Only use this hook if you are NOT using Formik or withFormik.

## !! 
https://brianflove.com/2014-09-02/whats-the-double-exclamation-mark-for-in-javascript/
If you have ever noticed a double exclamation mark (!!) in someone's JavaScript code you may be curious what it's for and what it does. It's really simple: it's short way to cast a variable to be a boolean (true or false) value. Let me explain.

# Day 9
## tooltip
https://www.npmjs.com/package/react-native-walkthrough-tooltip
React Native Walkthrough Tooltip is a fullscreen modal that highlights whichever element it wraps.  
When not visible, the wrapped element is displayed normally.

## (?= ) - lookahead assertion regex
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Assertions
Lookahead assertion: Matches "x" only if "x" is followed by "y". For example, /Jack(?=Sprat)/ matches "Jack" only if it is followed by "Sprat".
/Jack(?=Sprat|Frost)/ matches "Jack" only if it is followed by "Sprat" or "Frost". However, neither "Sprat" nor "Frost" is part of the match results.

##  read-vietnamese-number
https://www.npmjs.com/package/read-vietnamese-number
Thư viện chuyển đổi số thành chữ trong Tiếng Việt. Có các tính năng như:

-   Đọc được số âm, số thập phân
-   Số lớn tùy ý (chỉ cần thêm đủ các đơn vị phù hợp)
-   Có nhiều tùy chọn: đơn vị tính, dấu phân tách, cách đọc số,...

Hỗ trợ ngôn ngữ JavaScript và TypeScript, tương thích với ECMAScript 6 trở lên.

## reselect
https://viblo.asia/p/tim-hieu-ve-selectors-reselect-QpmleJmn5rd


## qs
https://www.npmjs.com/package/qs
A querystring parsing and stringifying library with some added security.

## useCallback
https://codestus.com/posts/huong-dan-su-dung-usecallback-trong-react
useCallback là được sử dụng để tối ưu quá trình render của React functional components. Nó sẽ rất hữu ích đối với trường hợp một thành phần (component) liên tục được hiển thị lại không cần thiết trong quá trình xử lý sự kiện người dùng và có hành vi chức năng phức tạp. Chúng ta sẽ xem xét thông qua ví dụ đơn giản về cách triển khai hook này để xem cách nó có thể giúp chúng ta đạt hiệu quả thế nào trong quá trình xử lý re-rendering của component.

Hãy nhớ rằng React đã rất nhanh, tối ưu hiệu xuất chỉ nên sử dụng cho những component có khả năng chậm, xử lý tác vụ nặng. Khi đó, chúng ta sẽ xem xét xử dụng useCallback làm một phần hỗ trợ tối ưu hiện xuất trong các hook.

# Day 10
## createAsyncThunk
https://redux-toolkit.js.org/api/createAsyncThunk
A function that accepts a Redux action type string and a callback function that should return a promise. It generates promise lifecycle action types based on the action type prefix that you pass in, and returns a thunk action creator that will run the promise callback and dispatch the lifecycle actions based on the returned promise.

This abstracts the standard recommended approach for handling async request lifecycles.

It does not generate any reducer functions, since it does not know what data you're fetching, how you want to track loading state, or how the data you return needs to be processed. You should write your own reducer logic that handles these actions, with whatever loading state and processing logic is appropriate for your own app.

## useLayoutEffect
https://viblo.asia/p/useeffect-vs-uselayouteffect-maGK7OBeKj2

## refs 
https://viblo.asia/p/refs-trong-react-la-gi-va-mot-so-truong-hop-su-dung-refs-RnB5p4y65PG

# Day 13
## The JavaScript Reduce Method Explained
https://www.digitalocean.com/community/tutorials/js-finally-understand-reduce
Reduce is a method that can be difficult to understand especially with all the vague explanations that can be found on the web. There are a lot of benefits to understanding reduce as it is often used in state management (think Redux).

The signature for the reduce array method in JavaScript is:

arr.reduce(callback, initialValue);
