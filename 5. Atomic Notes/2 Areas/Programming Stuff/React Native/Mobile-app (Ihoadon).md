# *__tests__*
## App-test.js
### react-test-renderer
https://reactjs.org/docs/test-renderer.html#testrenderercreate
This package provides a React renderer that can be used to render React components to pure JavaScript objects, without depending on the DOM or a native mobile environment.

Essentially, this package makes it easy to grab a snapshot of the platform view hierarchy (similar to a DOM tree) rendered by a React DOM or React Native component without using a browser or [jsdom](https://github.com/tmpvar/jsdom)
# ***.vscode***
Không có gì
# ***.well-known***
Chưa rõ để làm gì.
# ***android***
Chưa
# ***e2e***
  https://www.careerlink.vn/cam-nang-viec-lam/kien-thuc-kinh-te/end-to-end-la-gi#:~:text=End%20To%20End%20Testing%20(E2ET)&text=Thu%E1%BA%ADt%20ng%E1%BB%AF%20End%20To%20End,th%E1%BB%91ng%20tr%C3%AAn%20m%E1%BB%8Di%20%E1%BB%A9ng%20d%E1%BB%A5ng.
Thuật ngữ **End To End Testing** được dùng như một phương pháp kiểm tra để xác định liệu việc thực hiện các ứng dụng có theo đúng yêu cầu hay không. Quy trình đầu cuối **End To End Testing** được tiến hành sau khi hoàn thành giai đoạn kiểm tra chức năng và kiểm tra hệ thống trên mọi ứng dụng.
# ***fastlane***
https://docs.fastlane.tools/
_fastlane_ is the easiest way to automate beta deployments and releases for your iOS and Android apps. 🚀 It handles all tedious tasks, like generating screenshots, dealing with code signing, and releasing your application
# ***ios***
Chưa
# ***src***
## ***assets***
### svg images
https://en.wikipedia.org/wiki/Scalable_Vector_Graphics

Scalable Vector Graphics (SVG) is an XML-based vector image format for defining two-dimensional graphics, having support for interactivity and animation. The SVG specification is an open standard developed by the World Wide Web Consortium (W3C) since 1999.

SVG images are defined in a vector graphics format and stored in XML text files. SVG images can thus be scaled in size without loss of quality, and SVG files can be searched, indexed, scripted, and compressed. The XML text files can be created and edited with text editors or vector graphics editors, and are rendered by the most-used web browsers.
##  ***components***
### ***Document***
#### DocItem
Thực ra nó chỉ là một cái ô hình vuông, bên trong có thông tin về hóa đơn. Hết
#### ModalDetail
##### RN-gesture-handler
https://docs.swmansion.com/react-native-gesture-handler/docs/
Gesture Handler aims to replace React Native's built in touch system called Gesture Responder System.

The motivation for building this library was to address the performance limitations of React Native's Gesture Responder System and to provide more control over the built-in native components that can handle gestures. We recommend this talk by Krzysztof Magiera in which he explains issues with the responder system.
##### RN-fetch-blob
https://github.com/joltup/rn-fetch-blob
A project committed to making file access and data transfer easier and more efficient for React Native developers.


##### RNFetchBlob.android.actionViewIntent
When sending an ACTION_VIEW intent with given file path and MIME type, system will try to open an App to handle the file. For example, open Gallery app to view an image, or install APK.
##### PermissionAndroid
https://reactnative.dev/docs/permissionsandroid
`PermissionsAndroid` provides access to Android M's new permissions model. The so-called "normal" permissions are granted by default when the application is installed as long as they appear in `AndroidManifest.xml`. However, "dangerous" permissions require a dialog prompt. You should use this module for those permissions.

#### ModalFilter
##### Yup
https://www.npmjs.com/package/yup
Yup is a JavaScript schema builder for value parsing and validation. Define a schema, transform a value to match, validate the shape of an existing value, or both. Yup schema are extremely expressive and allow modeling complex, interdependent validations, or value transformations.

Yup's API is heavily inspired by [Joi](https://github.com/hapijs/joi), but leaner and built with client-side validation as its primary use-case. Yup separates the parsing and validating functions into separate steps. `cast()` transforms data while `validate` checks that the input is the correct shape. Each can be performed together (such as HTML form validation) or seperately (such as deserializing trusted data from APIs).
### ***EProducts***
#### EproductListItem
Thực ra là 1 list sản phẩm của EproductItem thôi
### ***Extension***
#### EditAddressModal
Hình như ko dùng
#### EditInfoModal
Không có gì đặc biệt
#### FunctionItem
#### Setup2FA
#### Verify2FA
#### VerifyBio
### ***GovProducts***
Không có gì
### ***Home***
#### react-native-snap-carousel4
https://github.com/meliorence/react-native-snap-carousel
Carousel là loại quảng cáo xoay vòng trên Facebook. Người dùng có được nhiều nội dung hơn trong cùng một không gian thông qua chuỗi hình ảnh xoay vòng của loại quảng cáo này. Ngoài ra, người đăng cũng có thể kiểm soát trình tự của chuỗi quảng cáo xoay vòng theo ý thích hoặc dụng ý của doanh nghiệp
### ***Language***
Nope
### ***QRCode***
Nope
### ***SearchRecord***
#### rn-pdf
https://www.npmjs.com/package/react-native-pdf
-   read a PDF from url, blob, local file or asset and can cache it.
-   display horizontally or vertically
-   drag and zoom
-   double tap for zoom
-   support password protected pdf
-   jump to a specific page in the pdf
### ***Signature***
#### rn-signature-canvas
https://www.npmjs.com/package/react-native-signature-canvas
-   Supports Android and iOS and Expo
-   Pure JavaScript implementation with no native dependencies
-   Tested with RN 0.50
-   Core use [signature_pad.js](https://github.com/szimek/signature_pad)
-   Only depend on react and react native
-   Generates a base64 encoded png image of the signature Note: Expo support for React Native Signature Canvas v1.5.0 started with Expo SDK v33.0.0.

#### react-native-image-crop-picker
https://github.com/ivpusic/react-native-image-crop-picker
iOS/Android image picker with support for camera, video, configurable compression, multiple images and cropping
### ***UI***
#### Activity Indicator
Thực chất nó là cái nút load quay vòng khi mà data chưa load xong. Tùy biến theo thư viện có sẵn
#### AppKeyboardAvoidingView
##### useHeaderHeight
https://reactnavigation.org/docs/elements/#useheaderheight
Hook that returns the height of the nearest visible header in the parent screen.
##### typescript & operator
https://stackoverflow.com/questions/33875609/typescript-operator
This looks like it's from the Intersection Types portion of the Language Specification. Specifically, the & is an intersection type literal. As for what it does:

Intersection types represent values that simultaneously have multiple types. A value of an intersection type A & B is a value that is both of type A and type B. Intersection types are written using intersection type literals (section 3.8.7).

#### Card
Đơn giản nó chỉ là cái bọc ngoài cho bất kì 1 view nào thôi. Nó chỉ có mỗi background color, chả có gì thêm

#### Checked
Checkbox màu xanh thôi. Ko có gì đặc biệt
#### CountDown
Không dùng thì phải 
#### Curve
Thằng curve này hay vl. Cần nghiên cứu thêm
#### DatePicker
##### react-native-modal-datetime-picker
https://github.com/mmazzarolo/react-native-modal-datetime-picker
This library exposes a cross-platform interface for showing the native date-picker and time-picker inside a modal, providing a unified user and developer experience

##### Formik
https://formik.org/
Let's face it, forms are really verbose in React. To make matters worse, most form helpers do wayyyy too much magic and often have a significant performance cost associated with them. Formik is a small library that helps you with the 3 most annoying parts:

Getting values in and out of form state
Validation and error messages
Handling form submission
By colocating all of the above in one place, Formik will keep things organized--making testing, refactoring, and reasoning about your forms a breeze.

#### GradientButton
Cái này dễ, không cần phải nói nhiều. 

#### GradientIcon
Không dùng
#### HeaderBackgroud
##### react-navigation-header-buttons
https://www.npmjs.com/package/react-navigation-header-buttons
This package will help you render buttons in the navigation bar and handle the styling so you don't have to. It tries to mimic the appearance of native navbar buttons and attempts to offer simple and flexible interface for you to interact with. Typed with Flow and ships with TS typings. Supports iOS and Android, web support is experimental.
#### HeaderLeftBackButton
Thực chất chỉ là cái mũi tên quay đầu ngược lại mà thôi
#### HeaderRightComponent
Không có gì đặc biệt
#### Input
##### react-native-text-input-mask
https://blog.logrocket.com/using-input-masks-react-native/
React Native developers often implement various input forms in their mobile applications, which typically contain and accept various input elements and input strings, like names, mobile numbers, dates, times, or postal codes.

Many developers implement input masks with form input elements to add user-friendly input constraints. Input masks are string templates that guide users to enter valid data according to a pre-defined format, usually by blocking invalid keystrokes and displaying the allowed string format as a placeholder. For example, users can only enter numerical digits inside a masked PIN/OTP input box.
#### InputForm

#### Loader
Cũng kiểu activity indicator
#### MainButton 
Cunxg chi la button binh thuon
#### ModalSelectBox
#### MSPdfView
#### NewCountDown
#### NewLoader
#### NonCheck
#### Notification
#### OTPComfirmation
#### ProgressBar
#### SecondButton
#### SelectBox
#### ShareButton
#### StatusBarWithGradient
#### StatusBarWithOutGradient
#### Text
#### TextButton
#### TextInput
#### TouchableOpacity
#### WebViewModal

### DrawSignature
### DrawSignatureModal
### EKYC
### RecordItem
### TransactionSignModal

### TransactionSignResultModal
Nope
##  ***constants***
### UAT
https://itnavi.com.vn/blog/uat-la-gi
Kiểm thử chấp nhận của người dùng (user acceptance test - UAT) được định nghĩa là một loại kiểm thử được thực hiện bởi chính khách hàng để xác nhận hệ thống đã hoạt động đúng như mong đợi và thỏa mãn yêu cầu của người dùng hay chưa.UAT được thực hiện ở giai đoạn kiểm thử cuối cùng trước khi phần mềm được bàn giao và đưa vào hoạt động chính thức.

Mục đích của giai đoạn kiểm thử này là kiểm tra lại sản phẩm theo hướng của người dùng để đưa sản phẩm đến release. Giai đoạn này được thực hiện trong một môi trường thử nghiệm riêng biệt so với môi trường dev và sẽ có rất nhiều người dùng cuối tham gia.Để hiểu hơn về UAT, chúng ta cùng bóc nghĩa từng phần của cái tên này nhé!

### Image.resolveAssetSource()
https://reactnative.dev/docs/image.html#resolveassetsource
Resolves an asset reference into an object which has the properties `uri`, `width`, and `height`.
##  ***data***
Nope
##  ***filters***
Không có gì đặc sắc
##  ***hooks***
https://overreacted.io/making-setinterval-declarative-with-react-hooks/
Pay attention to this one. 
##  ***interfaces***
Nothing
##  ***models***
nothing
##  ***navigators***
### DocumentNav
Gồm: 
- DocumentScreen
- DocumentDetailScreen
### ExtensionNav
- ExtensionScreen
- SearchRecordScreen
- ProfileScreen
- EditInfoScreen
### HomeNav
Gồm: 
- Home
- Login
- Register
- ForgetPass
- ConfirmMethod
- UpdateInfoOtpCheck
- ChangePassword
- EProduct	
- GovProducts
- NewsList
- Scan
- SearchRecordNav
- AttachFile
- DocumentDetail
- ListRecordSignature
- PreviewSignDocument
- RegisterCert
- SignDocument
- SignedDocument
- ConfirmCert
### NotificationNav
- NotificationsScreen
- NotificationDetailScreen
### ProfileNav
- SettingScreen
- ProfileScreen
- EditInfoScreen
- AccountScreen
- SignatureManagementScreen
### QRCodeNav
- ScanScreen
### SearchRecordNav
Gồm: 
- AppSearchScreen
- ListRecordAppSearchScreen
- RecordItemDetailScreen
- SignatureItemLogScreen
- 
### SignatureNav
- SignatureScreen
- ListRecordSignatureScreen
- SignatureItemDetailScreen
- SignatureItemLogScreen
- AttachFileScreen
### MainNav
Không dùng
#### useFocusEffect
Hook to run an effect in a focused screen, similar to `React.useEffect`. This can be used to perform side-effects such as fetching data or subscribing to events. The passed callback should be wrapped in `React.useCallback` to avoid running the effect too often
### AppNav
Gồm: 
-	HomeNav
-	DocNav
-	SignatureNav
-	ProfileNav
#### useCallback
https://reactjs.org/docs/hooks-reference.html#usecallback
Returns a [memoized](https://en.wikipedia.org/wiki/Memoization) callback.

Pass an inline callback and an array of dependencies. `useCallback` will return a memoized version of the callback that only changes if one of the dependencies has changed. This is useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders (e.g. `shouldComponentUpdate`).
#### memoization
https://en.wikipedia.org/wiki/Memoization
In computing, memoization or memoisation is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again. Memoization has also been used in other contexts (and for purposes other than speed gains), such as in simple mutually recursive descent parsing.[1] Although related to caching, memoization refers to a specific case of this optimization, distinguishing it from forms of caching such as buffering or page replacement. In the context of some logic programming languages, memoization is also known as tabling.[2]
#### Deep Links
https://reactnavigation.org/docs/configuring-links
https://www.adjust.com/blog/dive-into-deeplinking/
Đọc kĩ về nó
##  ***screens***
### ***account***
### ***auth***
### ***document***
### ***extension***
### ***news***
### ***notification***
### ***qrcode***
### ***search***
### ***signature***
### ConfirmCertScreen
### EProductScreen
### GovProductScreen
### HomeScreen
### NewsListScreen
### PreviewSignDocScreen
### RegisterCertScreen
### SignDocumentScreen
### SignedDocumentScreen
### SplashScreen 
##  ***services***
### efyIdApi
#### base64
https://www.npmjs.com/package/react-native-base64
Base64 encoding and decoding helping util (does not support some Unicode characters).  
Created for React Native but can be used anywhere.
### FCMService
Bỏ qua
### LocalNotiService
#### push notification
https://github.com/zo0r/react-native-push-notification
@react-native-community/push-notification-ios
### LogConfig
Liên quan đến ReactOtron
### qrcode
#### !! 
https://stackoverflow.com/questions/784929/what-is-the-not-not-operator-in-javascript
https://stackoverflow.com/questions/784929/what-is-the-not-not-operator-in-javascript
### RootNav
### util
#### _.get (Lodash)
https://www.geeksforgeeks.org/lodash-_-get-method/
The _.get() method is used to get the value at path of object. If the resolved value is undefined, the defaultValue is returned in its place
##  ***store***
### ***actions***
Ko có gì đặc biệt
### ***reducers***
#### Immutable
Cần đọc kĩ lại phần này!
#### state.merge
https://stackoverflow.com/questions/35082390/react-redux-merge-state-with-given-array
To create a new object with the state in ES6 we can use the spread operator. Like this

#### TypedUseSelectorHook
This interface allows you to easily create a hook that is properly typed for your store's root state.

_@example_
#### Reducer<AppState, AllActionTypes>
A _reducer_ (also called a _reducing function_) is a function that accepts an accumulation and a value and returns a new accumulation. They are used to reduce a collection of values down to a single value

Reducers are not unique to Redux—they are a fundamental concept in functional programming. Even most non-functional languages, like JavaScript, have a built-in API for reducing. In JavaScript, it's `Array.prototype.reduce()`.

In Redux, the accumulated value is the state object, and the values being accumulated are actions. Reducers calculate a new state given the previous state and an action. They must be _pure functions_—functions that return the exact same output for given inputs. They should also be free of side-effects. This is what enables exciting features like hot reloading and time travel.

Reducers are the most important concept in Redux.
### ***sagas***

Khó. Chưa cần đọc

### ***selectors***
#### Reselect
https://github.com/reduxjs/reselect
Reselect exports a `createSelector` API, which generates memoized selector functions. `createSelector` accepts one or more "input" selectors, which extract values from arguments, and an "output" selector that receives the extracted values and should return a derived value. If the generated selector is called multiple times, the output will only be recalculated when the extracted values have changed.
### ***types***
#### Why immutable.js? 
https://grapeup.com/blog/benefits-of-using-immutable-js-with-react-redux-apps/#
Before using Immutable.js, the biggest issue with the Redux library often comes to returning a new object, which is nested in another object. In this case, using the Object.assign and spread operator syntax is not readable and may increase app complexity.

Some may suggest keeping your reducer’s state as flat as possible. That could be right, but sometimes, even if your state is flat, you would have to set something in a nested object. So, if you also struggle because of that, the immutable library comes to make your life easier
#### Record - Immutatble.js
https://gist.github.com/jareware/5f492d47fae45d577e922c431c267c67
Immutable.js provides a beautiful, [Clojure-inspired](https://facebook.github.io/immutable-js/#javascript-first-api) API for dealing with abstract Collections and Sequences, and several concrete data structures that implement that API, such as Lists, Maps and so on. The only ugly spot, so to speak, on the API is accessing Map values. With traditional JS objects, you're used to going:

const bear = { sound: 'growl' }
bear.sound // => 'growl'

But with Immutable.Map -- the thing you get when converting directly from JS to Immutable -- it's not as convenient:

import { fromJS } from 'immutable'
const bear = fromJS({ sound: 'growl' })
bear.sound // => undefined
bear.get('sound') // => 'growl'

That `.get()` stuff is somewhat awkward syntax for something that you'll be doing **a lot** across your codebase, especially as JS devs are used to the convenience of simply dot-accessing properties of objects.

Records bridge this convenience gap in property access:

import { Record } from 'immutable'
const Animal = Record({
  sound: 'unknown' // this is the default value if no 'sound' is set
})
const bear = new Animal({
  sound: 'growl'
})
bear.sound // => 'growl'
bear.get('sound') // => 'growl'

#### List - Immutable
You can create a List of data using either the `List()` constructor, or the `List.of()` method, depending on the type of data you’re using to create the List:

-   `List.of()` – use when creating a List from non-iterable data (e.g. a set of function arguments, a JavaScript object, or a string you want interpreted as a whole string);
-   `List()` – use when creating a List from iterable data (e.g. an array, or an Immutable Iterable object (List, Map, Set, etc.), or a string that you want interpreted as a series of characters).

_**Important:** a JavaScript string is an [iterable object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#Builtin_iterables "JavaScript iterables"), so if you create a List of strings using `List("string")`, you’ll actually get a List of characters (`['s', 't', 'r', 'i', 'n', 'g']`). To make Immutable interpret a string as a non-iterable value, use `List.of("string")` instead. See the examples below._

Immutable’s List constructors only create a List from a the top level of an Array. This means that a nested array will be turned into an Immutable List of arrays, whereas you might prefer a List of Lists.

To ensure all nested arrays are converted to Immutable Lists, use the `Immutable.fromJS()` function

##  ***types***
### type alias
https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases
We’ve been using object types and union types by writing them directly in type annotations. This is convenient, but it’s common to want to use the same type more than once and refer to it by a single name.

A _type alias_ is exactly that - a _name_ for any _type_
### enum
https://www.typescriptlang.org/docs/handbook/enums.html
Enums are one of the few features TypeScript has which is not a type-level extension of JavaScript.

Enums allow a developer to define a set of named constants. Using enums can make it easier to document intent, or create a set of distinct cases. TypeScript provides both numeric and string-based enums.

### typeof
https://www.typescriptlang.org/docs/handbook/2/keyof-types.html
The `keyof` operator takes an object type and produces a string or numeric literal union of its keys. The following type P is the same type as “x” | “y”

type Point = { x: number; y: number };

type P = keyof Point;

### interface
https://viblo.asia/p/interface-trong-typescript-phan-1-6J3Zgk3LZmB
_Interface trong typescript cho phép bạn định nghĩ thuộc tính là gì và phương thức là gì mà đối tượng cần để được thực thi (implement). Nếu đối tượng tuân thủ đúng khuôn mẫu interface thì đối tượng đã implement interface ấy sẽ được thi hành đúng. Nếu interface không được thi hành đúng đắn thì typescript sẽ phát sinh lỗi ngay lập tức. Để rõ hơn, bạn hãy xem những ví dụ và giải thích dưới đây:_
##  ***utils***
### screenShot.js
#### child_process
https://viblo.asia/p/tai-sao-ung-nodejs-lai-de-dang-de-mo-rong-RnB5p3WDlPG
Chúng ta có thể dễ dàng sinh ra một tiến trình con bằng cách sử dụng các mô đun child_ process và các tiến trình con đó có thể dễ dàng giao tiếp với nhau bằng một messaging system. Mô đun child_ process cho phép chúng ta truy cập các chức năng của Hệ điều hành bằng cách chạy bất kỳ lệnh hệ thống nào bên trong một tiến trình con, kiểm soát input stream và lắng nghe outout stream của nó. Chúng ta có thể kiểm soát các đối số được truyền vào lệnh và chúng ta có thể làm bất cứ điều gì chúng ta muốn với output của nó. Ví dụ, chúng ta có thể chuyển input của một lệnh này sang một lệnh khác, vì tất cả các input và output của các lệnh này có thể được hiện ra cho chúng ta bằng cách sử dụng các stream.

#### import __ from lodash
https://topdev.vn/blog/import-lodash-nhu-the-nao-moi-dung/
Tại sao lại chọn kiểu này? Không cần quan tâm đến user, cảm giác rất quyền lực như có găng tay vô cực, chỉ với `_.` chúng ta có tất cả mọi thứ.
Điểm yếu, đây là cách tuyệt đối nghiêm cấm, vì gần như là load nguyên cái thư viện

####  Using ADB to capture the screen
https://stackoverflow.com/questions/27766712/using-adb-to-capture-the-screen
```sql
adb exec-out screencap -p > screen.png
```

#### Element finder
https://www.protractortest.org/#/api?view=ElementFinder
The ElementFinder simply represents a single element of an ElementArrayFinder (and is more like a convenience object). As a result, anything that can be done with an ElementFinder, can also be done using an ElementArrayFinder.

The ElementFinder can be treated as a WebElement for most purposes, in particular, you may perform actions (i.e. click, getText) on them as you would a WebElement. Once an action is performed on an ElementFinder, the latest result from the chain can be accessed using the then method. Unlike a WebElement, an ElementFinder will wait for angular to settle before performing finds or actions.

ElementFinder can be used to build a chain of locators that is used to find an element. An ElementFinder does not actually attempt to find the element until an action is called, which means they can be set up in helper files before the page is available.
# **.buckconfig**
không có gì
# **.eslintrc.js**
https://eslint.org/docs/latest/user-guide/configuring/
Tra ở đây là rõ cách config cho eslint 
# **.flowconfig**
không có gì
# **.gitattributes**
chứa large file 
# **.gitignore**
không có gì 
# **.lintstagedrc.js**
https://github.com/okonet/lint-staged
Run linters against staged git files and don't let ![hankey](https://github.githubassets.com/images/icons/emoji/unicode/1f4a9.png) slip into your code base!
Linting makes more sense when run before committing your code. By doing so you can ensure no errors go into the repository and enforce code style. But running a lint process on a whole project is slow, and linting results can be irrelevant. Ultimately you only want to lint files that will be committed.

This project contains a script that will run arbitrary shell tasks with a list of staged files as an argument, filtered by a specified glob pattern.

# **.prettierrc.js**
không có gì
# **.svgrrc**
không có gì
# **.watchmanconfig**
Không có gì
# **app.json**
Không có gì
# **App.tsx**
## RN-screens
https://github.com/software-mansion/react-native-screens
Native navigation primitives for your React Native app.
Phục vụ cho thằng NativeStackNavigator
# **babel.config.js**
không có gì !
# **declaration.d.ts**
https://stackoverflow.com/questions/44717164/unable-to-import-svg-files-in-typescript
### react-native-svg
https://www.npmjs.com/package/react-native-svg
`react-native-svg` provides SVG support to React Native on iOS and Android, and a compatibility layer for the web.
### module d.ts
https://www.typescriptlang.org/docs/handbook/declaration-files/templates/module-d-ts.html
The .d.ts syntax intentionally looks like ES Modules syntax. ES Modules was ratified by TC39 in 2019, while it has been available via transpilers for a long time, however if you have a JavaScript codebase using ES Modules:
# **Gemfile**
Nope
# **Gemfile.lock**
Nope
# **i18n.ts**
https://viblo.asia/p/ap-dung-i18n-trong-rails-5-oOVlYqEnl8W
I18n là viết tắt của từ Internationalization(Quốc tế hóa) nếu như bạn để ý thì số 18 trong i18n chính là 18 ký tự đứng giữa chữ cái i đầu tiên và chữ cái n cuối cùng trong từ bị viết tắt đó. Đơn giản i18n hỗ trợ ta trong việc chuyển đổi đa ngôn ngữ cho ứng dụng và nó đã được rails hỗ trợ từ phiên bản 2.2, nhưng trong bài viết này mình xin phép tập trung vào i18n trong rails 5.

### i18n-next
https://www.i18next.com/
I18next is an internationalization-framework written in and for JavaScript. But it's much more than that.
i18next goes beyond just providing the standard i18n features such as (plurals, context, interpolation, format). It provides you with a complete solution to localize your product from web to mobile and desktop.

### react-i18n-next
https://react.i18next.com/
React-i18next là một framework internationalization (quốc tế hóa) mạnh mẽ cho Reactjs/Reactnative dựa trên i18next. Các mô-đun cung cấp nhiều thành phần, ví dụ: để xác nhận rằng các bản dịch cần thiết được tải hoặc nội dung của bạn được hiển thị khi ngôn ngữ thay đổi. Reac-i18next còn phù hợp cho tối ưu serverside rendering. Nó cung cấp thêm nhiều các extension ví dụ như làm việc với next.js. Vì Reac-i18next phụ thuộc vào i18next, bạn cũng có thể sử dụng nó trên bất kỳ các framework UI và máy chủ nào khác (node.js, .net, ...).
# **index.js**
### @react-native-firebase/messaging
https://www.npmjs.com/package/@react-native-firebase/messaging
React Native Firebase provides native integration of Firebase Cloud Messaging (FCM) for both Android & iOS. FCM is a cost free service, allowing for server-device and device-device communication. The React Native Firebase Messaging module provides a simple JavaScript API to interact with FCM.

### Headless JS
https://reactnative.dev/docs/headless-js-android
Headless JS is a way to run tasks in JavaScript while your app is in the background. It can be used, for example, to sync fresh data, handle push notifications, or play music.
# **InputForm.tsx**
Chưa có gì !
# **jest.config.js**
https://jestjs.io/docs/configuration
Chẳng có gì nhiều, thực ra đây chỉ là cách thức config cho jest test.

# **metro.config.js**
### react-native-svg-transformer
https://github.com/kristerkari/react-native-svg-transformer
React Native SVG transformer allows you to import SVG files in your React Native project the same way that you would in a Web application when using a library like SVGR to transform your imported SVG images into React components.
This makes it possible to use the same code for React Native and Web.
# **package.json**
https://instamobile.io/react-native-tutorials/full-clean-react-native-project/
Usually, you want to fully clean your project if you:

-   Ran a project on your machine that was in a different React Native version (to avoid the React Native Mistmatch error)
-   Ran the same project previously, but in a different React Native version
-   Bumped up package versions in the **_package.json_** file
-   Modified **_ios/Podfile_**
-   Opened the metro bundler in the wrong folder
-   Changed your codebase to point to a different Firebase project
-   Encounter build issues in Xcode or Android Studio

Fully removing the cache of your React Native environment is a good way to clean out your build after some time running the project so that you are sure your build includes only the most up-to-date files based on your source code.

### husky
https://viblo.asia/p/nang-cao-chat-luong-code-va-hieu-qua-lam-viec-nhom-voi-husky-lint-staged-commitlint-4dbZNnMnZYM
Husky là một tool mà nó có thể bắt được event khi ta thao tác với Git repository (add, commit,...) và từ đó ta có thể thực hiện các hành động tương ứng, hoặc ngăn không cho commit. Husky và Lint-staged là 1 cặp bài trùng thường đi cùng với nhau, cực kì hữu dụng trong việc đảm bảo code khi được commit lên repository luôn được chạy qua những công đoạn kiểm tra để chắc chắn "code sạch, code đẹp"
# **react-native.config.js**
https://github.com/react-native-community/cli/blob/main/docs/projects.md
Hiểu đơn giản nó là cách chúng ta chỉ định custom configuration cho 1 dự án React-Native. 
# **ReactotronConfig.js**
### reactotron-react-native
https://github.com/infinitered/reactotron
Reactotron is a macOS, Windows, and Linux app for inspecting your React JS and React Native apps.
Use it to:

-   view your application state
-   show API requests & responses
-   perform quick performance benchmarks
-   subscribe to parts of your application state
-   display messages similar to `console.log`
-   track global errors with source-mapped stack traces including saga stack traces!
-   dispatch actions like a government-run mind control experiment
-   hot swap your app's state using Redux or mobx-state-tree
-   track your sagas
-   show image overlay in React Native
-   track your Async Storage in React Native

### reactotron-redux-saga

### redux-saga
https://viblo.asia/p/tim-hieu-ve-redux-saga-bWrZnODmlxw
Redux-Saga là một thư viện redux middleware, giúp quản lý những side effect trong ứng dụng redux trở nên đơn giản hơn. Bằng việc sử dụng tối đa tính năng Generators (function*) của ES6, nó cho phép ta viết async code nhìn giống như là synchronos.

Vậy side effect là cái gì nhỉ? Như mọi người đã biết tất cả các xử lý trong Reducers đều là đồng bộ, nhưng thực tế là có những thao tác mà ta bắt buộc phải xử lý bất đồng bộ, ví dụ như là đợi 1 request dùng để fetch dữ liệu về rồi sau đó mới thực hiện tiếp các thao tác khác (thay đổi state, dispatch 1 action bất kỳ...) đó chính là side effect.

You plug it into your app as a dev dependency so it adds nothing to your product builds

### reactotron-redux

Nói chung ta có thể đọc về cách setup project vs otron tại đây: 
https://dev.to/ajmal_hasan/reactotron-setup-in-react-native-redux-applications-4jj3
OK!
# **tsconfig.json**
https://www.typescriptlang.org/docs/handbook/tsconfig-json.html
The presence of a tsconfig.json file in a directory indicates that the directory is the root of a TypeScript project. The tsconfig.json file specifies the root files and the compiler options required to compile the project.
JavaScript projects can use a jsconfig.json file instead, which acts almost the same but has some JavaScript-related compiler flags enabled by default.
A project is compiled in one of the following ways:
Using tsconfig.json or jsconfig.json
By invoking tsc with no input files, in which case the compiler searches for the tsconfig.json file starting in the current directory and continuing up the parent directory chain.
By invoking tsc with no input files and a --project (or just -p) command line option that specifies the path of a directory containing a tsconfig.json file, or a path to a valid .json file containing the configurations.
When input files are specified on the command line, tsconfig.json files are ignored.
### paths: 
https://www.typescriptlang.org/tsconfig#paths
A series of entries which re-map imports to lookup locations relative to the baseUrl. There is a larger coverage of paths in the handbook.

paths lets you declare how TypeScript should resolve an import in your require/imports.