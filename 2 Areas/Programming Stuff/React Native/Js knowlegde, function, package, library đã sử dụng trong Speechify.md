# Các thư viện
**Code push**
A React Native app is composed of JavaScript files and any accompanying [images](https://reactnative.dev/docs/image), which are bundled together by the [metro bundler](https://github.com/facebook/metro) and distributed as part of a platform-specific binary (i.e. an `.ipa` or `.apk` file). Once the app is released, updating either the JavaScript code (e.g. making bug fixes, adding new features) or image assets, requires you to recompile and redistribute the entire binary, which of course, includes any review time associated with the store(s) you are publishing to.

The CodePush plugin helps get product improvements in front of your end users instantly, by keeping your JavaScript and images synchronized with updates you release to the CodePush server. This way, your app gets the benefits of an offline mobile experience, as well as the "web-like" agility of side-loading updates as soon as they are available. It's a win-win!
**Moment**
Dùng để format lại thời gian theo dạng phù hợp
**Query string**
Parse and stringify URL [query strings](https://en.wikipedia.org/wiki/Query_string)
**react-native-device-info**
Rất nhiều hàm để lấy thông số của thiết bị. 
**react-native-in-app-review**
The Google Play In-App Review API, App store rating API lets you prompt users to submit Play Store or App store ratings and reviews without the inconvenience of leaving your app or game.
react native in app review, to rate on Play store, App Store, Generally, the in-app review flow (see figure 1 for play store, figure 2 for ios) can be triggered at any time throughout the user journey of your app. During the flow, the user has the ability to rate your app using the 1 to 5 star system and to add an optional comment for play store only. Once submitted, the review is sent to the Play Store or App store and eventually displayed.
**react-native-mail**
A React Native wrapper for Apple's `MFMailComposeViewController` from iOS and Mail Intent on android Supports emails with attachments.
**axios**
Axios is a _[promise-based](https://javascript.info/promise-basics)_ HTTP Client for [`node.js`](https://nodejs.org/) and the browser. It is _[isomorphic](https://www.lullabot.com/articles/what-is-an-isomorphic-application)_ (= it can run in the browser and nodejs with the same codebase). On the server-side it uses the native node.js `http` module, while on the client (browser) it uses XMLHttpRequests.
**url-parse**
`url-parse` was created in 2014 when the WHATWG URL API was not available in Node.js and the `URL` interface was supported only in some browsers. Today this is no longer true. The `URL` interface is available in all supported Node.js release lines and basically all browsers. Consider using it for better security and accuracy.

The `url-parse` method exposes two different API interfaces. The [`url`](https://nodejs.org/api/url.html) interface that you know from Node.js and the new [`URL`](https://developer.mozilla.org/en-US/docs/Web/API/URL/URL) interface that is available in the latest browsers
**lodash**
Lodash là một thư viện JavaScript mạnh mẽ dùng để xử lý Array, Object, Function, Collection ..v.v. 
**Redux Thunk là** một Middleware cho phép bạn viết các Action trả về một function thay vì một plain javascript object bằng cách trì hoãn việc đưa action đến reducer. **Redux Thunk** được sử dụng để xử lý các logic bất đồng bộ phức tạp cần truy cập đến Store hoặc đơn giản **là** việc lấy dữ liệu như Ajax request
**react-native-modal**
**react-native-splash-screen**
A splash screen is a graphical control element consisting of a window containing an image, a logo, and the current version of the software. A splash screen can appear while a game or program is launching
**react-native-fast-image**
ảnh được cache lại trong bộ nhớ tạm => load sẽ nhanh hơn, không có tình trạng giật khi render lại
# Kiến thức JS còn chưa tìm hiểu kĩ
**includes**
The **`includes()`** method determines whether an array includes a certain value among its entries, returning `true` or `false` as appropriate.
**charAt**
The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) object's **`charAt()`** method returns a new string consisting of the single UTF-16 code unit located at the specified offset into the string.
Ex: 
```javascript
const sentence = 'The quick brown fox jumps over the lazy dog.';
const index = 4; 
```
=> q 
**parseFloat**
The **`parseFloat()`** function parses an argument (converting it to a string first if needed) and returns a floating point number.
**parseInt**
Tương tự
**JSON.parse**
The **`JSON.parse()`** method parses a JSON string, constructing the JavaScript value or object described by the string. An optional **reviver** function can be provided to perform a transformation on the resulting object before it is returned.
**map**
`map` calls a provided `callbackFn` function **once for each element** in an array, in order, and constructs a new array from the results. `callbackFn` is invoked only for indexes of the array which have assigned values (including [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)).

It is _not_ called for missing elements of the array; that is:

-   indexes that have never been set;
-   indexes which have been deleted.

**Date.now()**
Lấy ra giá trị của thời gian hiện thời dưới dạng ms. 
**Template literal**
Ex: `[${appName} ${pro}for ${platform}] Feedback of version ${appVersion}`
**toLowerCase()**
converts a string to lowercase letters
**normalize('NFD')**
returns the Unicode Normalization Form of the string
`"NFC"`
Canonical Decomposition, followed by Canonical Composition.
`"NFD"`
Canonical Decomposition.
`"NFKC"`
Compatibility Decomposition, followed by Canonical Composition.
`"NFKD"`
Compatibility Decomposition.

Unicode assigns a unique numerical value, called a _code point_, to each character. For example, the code point for `"A"` is given as U+0041. However, sometimes more than one code point, or sequence of code points, can represent the same abstract character — the character `"ñ"` for example can be represented by either of:
-   The single code point U+00F1.
-   The code point for `"n"` (U+006E) followed by the code point for the combining tilde (U+0303)

**slice(start, end)**
The **`slice()`** method returns a [shallow copy](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy) of a portion of an array into a new array object selected from `start` to `end` (`end` not included) where `start` and `end` represent the index of items in that array. The original array will not be modified
**Object.key()**
The **`Object.keys()`** method returns an array of a given object's own enumerable property **names**, iterated in the same order that a normal loop would.
Ex: 
```javascript
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.keys(object1));
// expected output: Array ["a", "b", "c"]
```
**forEach**
Performs the specified action for each element in an array.
**concat()**
The **`concat()`** method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.
**lastIndexOf()**
The **`lastIndexOf()`** method, given one argument: a substring to search for, searches the entire calling string, and returns the index of the last occurrence of the specified substring. Given a second argument: a number, the method returns the last occurrence of the specified substring at an index less than or equal to the specified number.
**endsWith()**
The **`endsWith()`** method determines whether a string ends with the characters of a specified string, returning `true` or `false` as appropriate.
**matchAll**
Matches a string with a regular expression, and returns an iterable of matches containing the results of that search.
**isNaN**
Returns a Boolean value that indicates whether a value is the reserved value NaN (not a number).
**search**
Finds the first substring match in a regular expression search.
**push**
Appends new elements to the end of an array, and returns the new length of the array.
**toString**
Returns a string representation of an object.
**indexOf**
The **`indexOf()`** method returns the first index at which a given element can be found in the array, or -1 if it is not present.
Ex:
```javascript
const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

console.log(beasts.indexOf('bison'));
```
**trim()**
**some()**
The **`some()`** method tests whether at least one element in the array passes the test implemented by the provided function. It returns true if, in the array, it finds an element for which the provided function returns true; otherwise it returns false. It doesn't modify the array.
```javascript
const array = [1, 2, 3, 4, 5];

// checks whether an element is even
const even = (element) => element % 2 === 0;

console.log(array.some(even));
```
**filter()**
The **`filter()`** method **creates a new array** with all elements that pass the test implemented by the provided function.
```javascript
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]

```
**Array.isArray()**
The **`Array.isArray()`** method determines whether the passed value is an [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
**startsWith**
The **`startsWith()`** method determines whether a string begins with the characters of a specified string, returning `true` or `false` as appropriate.
**localeCompare()**
The **`localeCompare()`** method returns a number indicating whether a reference string comes before, or after, or is the same as the given string in sort order.
# Các hàm đặc biệt
**setTimeout, setInterval**
**3 cách clone object**
**Spread**
Ex: `const cloneFood = { ...food };`
**Object.assign**
`const cloneFood = Object.assign({}, food);`
**JSON**
`const cloneFood = JSON.parse(JSON.stringify(food))const cloneFood = JSON.parse(JSON.stringify(food))`

# Kiến thức React-Native, React chưa hiểu kĩ
**Dimension**
Thường dùng để lấy ra chiều dài, rộng của kích thước màn hình. 
Ex: `Dimensions.get('screen').width`
**Linking**
`Linking` gives you a general interface to interact with both incoming and outgoing app links.
**Platform**
APIs của RN để làm việc với 1 số nền tảng. 
**Alert**
Launches an alert dialog with the specified title and message.
**Props children**
https://viblo.asia/p/tim-hieu-ve-children-trong-react-oOVlYqWol8W


**Kiến thức về lodash**
**Kiến thức về TypeScript**
**Kiến thức về Nodejs**
**Async await - Promise**
**Kiến thức về AsyncStorage**
**Kiến thức về Redux, ReduxToolkits**
**Kiến thức về Regex**
**Kiến thức về React Hooks**
**Kiến thức về callback**
**Kiến thức về ES6, js**
**Kiến thức về Navigation**
**Kiến thức về unit test**
**Kiến thức về PropTypes**

# Thuật ngữ
**IAP**: In-app Purchase
**shallow copy**
A **shallow copy** of an object is a copy whose properties share the same references (point to the same underlying values) as those of the source object from which the copy was made. As a result, when you change either the source or the copy, you may also cause the other object to change too — and so, you may end up unintentionally causing changes to the source or copy that you don't expect. That behavior contrasts with the behavior of a [deep copy](https://developer.mozilla.org/en-US/docs/Glossary/Deep_copy), in which the source and copy are completely independent.