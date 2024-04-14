# Src
## Api
## Assets
### fontawesome
**@font-face**
https://www.w3schools.com/cssref/css3_pr_font-face_rule.asp
With the `@font-face` rule, web designers do not have to use one of the "web-safe" fonts anymore.
**url() format()**
https://sass-lang.com/documentation/syntax/special-functions#url
Đọc doc của fontawesome thì hay hơn đấy

### plugins
**use strict**
https://www.w3schools.com/js/js_strict.asp
Strict mode is declared by adding "use strict"; to the beginning of a script or a function.
**strict mode**
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode
 Strict Mode là một quy mẫu nghiêm khắc của Javascript. Nếu như coi việc viết code bình thường là Normal Mode, thì Strict Mode sẽ có thêm nhiều quy định khác so với Normal Mode. Việc đó khiến cho một thao tác vốn bình thường có thể chạy ngon lành trở nên lỗi, và throw ra errors.

Nhìn chung, Strict được tạo ra nhằm:

Ngăn chặn sử dụng, và throw errors khi người lập trình thực hiện những xử lý được coi là unsafe, những xử lý mà có thể là ngoài ý muốn.
Vô hiệu hoá các tính năng có thể gây nhầm lẫn, hoặc không nên được sử dụng.
Ngăn chặn sử dụng một số từ mà có thể sẽ được sử dụng làm keywork trong tương lai.

*Chưa hiểu phần này lấy ở thư viện nào. Chỉ biết là nó có load vào trong App.js*
### styles
cái này hình như để load file css của bootstrap vs 1 vài cái khác
## Components
### AcountCard
![[Pasted image 20220930220437.png]]
### AccountDropDown
![[Pasted image 20220930224206.png]]
### AppBreadcrumb
![[Pasted image 20221001100620.png]]
### AppCard
### AppModal/ModalDelete
![[Pasted image 20220930224952.png]]
### Apppage
![[Pasted image 20220930222210.png]]
### Apppagination
![[Pasted image 20221001100808.png]]
### AppTabs
![[Pasted image 20221001102916.png]]
### AreaFilter
### CardDetail
![[Pasted image 20221001110006.png]]
### CardDetailHaveButton
![[Pasted image 20221001110128.png]]
### CheckBox
![[Pasted image 20221001100752.png]]
### Connection
### DataTableCheckbox
### DevicesTable
### EBulletinHistoryTable
### EbulletinTable
![[Pasted image 20221001111019.png]]
### Empty
### Footer
![[Pasted image 20220930221357.png]]
### FormSection
### Header
vs Background or random
![[Pasted image 20220930223852.png]]
![[Pasted image 20220930224000.png]]
### HeaderMobile
![[Pasted image 20220930221917.png]]
### Keen
https://preview.keenthemes.com/metronic/demo1/custom/apps/user/edit-user.html
### Loading
### LoadingOverlay
### Navbar
![[Pasted image 20221001095551.png]]
### NotFound
### NotificationDropdown
![[Pasted image 20220930224225.png]]
### PageContent
![[Pasted image 20220930222305.png]]
### ReadonlyTextFiled
### ScrollTop
![[Pasted image 20221001102221.png]]
### SearchBarNoFormik
### SelectArea
![[Pasted image 20220930231508.png]]
### SelectRadioStation
![[Pasted image 20221001101903.png]]
### State
### SideBar
![[Pasted image 20220930222116.png]]
### Table/DataTable
![[Pasted image 20221001100715.png]]
### TextField
### TextFieldRightButtonAddon
### WeekdaySelect
## General
### Constants
Éo có gì cả. Giống dự án RN. Mà có khi ít constants hơn ấy
### Custom-fields
#### BaseDropdownSelect
#### BaseSearchBar
![[Pasted image 20221001095823.png]]
#### BaseSearchBarSuggestion
#### BaseTextField
![[Pasted image 20221001101018.png]]
#### BigInputField
#### CheckboxField
#### DateTimePickerField
#### InputArea
#### RadioField
#### SwitchField
#### TextareaInputField
### helpers
**Sweetalert2**
https://sweetalert2.github.io/
### types
Nope
### utils
Nope
### Global.js
Nope
## Hooks
Không có gì. Chỉ là custom 1 vài cái hooks cho sử dụng được ở nhiều components mà thôi
https://reactjs.org/docs/hooks-custom.html
## libs
Không có gì đặc biêt. Chỉ nói về redux và những cái mình đã biết rồi
## pages
### AccountManager
#### Screen
**Home**
![[Pasted image 20221001103831.png]]
**Overview**
![[Pasted image 20221001105723.png]]
#### Component
**ModalEdit**
![[Pasted image 20221001104136.png]]
**ModalDelete**
Tuowng tuw
**ModalChangePassword**
**ModalOTP**
**ModalUpdate**
**PasswordInput**
### AreaManager
Tương tự như Provider Manager
### BulletinList
### BulletinManager
#### Screen
**Create**
![[Pasted image 20221001111241.png]]
**History**
**Manager**
![[Pasted image 20221001111019.png]]
**Schedule**
#### Component
**AudioPlayer**
**ChooseSource**
**ChooseSourceTypeButton**
**ConfirmModal**
**CurvedTab**
**DatePicker**
**DevicesPicker**
**TimePicker**
**Visualizer**
**WeekdayPicker**
### Category
### Dashboard
#### Component
**Apexcharts**
https://apexcharts.com/docs/react-charts/
![[Pasted image 20221001092900.png]]
**Donut chart**
![[Pasted image 20221001092849.png]]
**BulletinCarousel**
![[Pasted image 20221001093110.png]]
**react-bootstrap/ProgressBar**
https://react-bootstrap.github.io/components/progress/
**QuangNinh**
![[Pasted image 20221001093338.png]]
**react-highcharts-official**
https://www.npmjs.com/package/highcharts-react-official
**highcharts**
https://www.highcharts.com/docs/index
**highcharts contries data**
https://code.highcharts.com/mapdata/
**classname/bind**
https://www.npmjs.com/package/classnames
**Info Component**
![[Pasted image 20221001093443.png]]
![[Pasted image 20221001093452.png]]

#### Screen/HomeScreen
![[Screenshot from 2022-10-01 09-28-27.png]]

![[Screenshot from 2022-10-01 09-48-28.png]]
#### other 
**useRouteMatch**
[`useRouteMatch`](https://v5.reactrouter.com/web/api/Hooks/useroutematch)
The `useRouteMatch` hook attempts to [match](https://v5.reactrouter.com/web/api/match) the current URL in the same way that a `<Route>` would. It’s mostly useful for getting access to the match data without actually rendering a `<Route>`.
**Route > exact**
https://v5.reactrouter.com/web/api/Route/exact-bool
### DeviceDetail
#### Component
**DeviceInfo**
![[Pasted image 20221001103346.png]]
**EvenInfo**

**ScheduleInfo**
![[Pasted image 20221001103419.png]]

### DeviceManager
#### Screen
**DeviceManagerScreen**
![[Pasted image 20221001102744.png]]
**DeviceDetailScreen**
Trong phan DeviceDetail
**DeviceConfigureScreen**
DeviceDetail
### DeviceMap
### EditBulletin
### Feedback
### GroupManager
### History
### Login
### ProgramManager
### ProviderManager
#### Components
**TableListProviders**
![[Pasted image 20221001101221.png]]
**TableListAccounts**
![[Pasted image 20221001101236.png]]
**ModalCreateProviders**
![[Pasted image 20221001101322.png]]
**Modal Create Account**
![[Pasted image 20221001101346.png]]
**SelectProviderDropdown**
![[Pasted image 20221001101749.png]]
**reactstrap**
https://reactstrap.github.io/?path=/story/home-installation--page
#### Screen
![[Pasted image 20221001102309.png]]
### RadioStationManager
#### Component
**ModalAddStation**
![[Pasted image 20221001100127.png]]
**RadioStationTable**
![[Pasted image 20221001100423.png]]
**ModalUpdateStation**
![[Pasted image 20221001100919.png]]
#### Screen
![[Screenshot from 2022-10-01 09-53-35.png]]
### Report
## routes
### GuestRoute.js
Route đăng nhập khi mới vào (Chỉ có mỗi login, quên mật khẩu vs lại 404 not found thôi
### PrivateRoute.js
Route cần đăng nhập
### TwoFactorAuthRoute.js
Đọc thêm
## App.css
**css unit**
https://viblo.asia/p/css-units-em-rem-pt-px-vw-vh-vmin-vmax-ex-ch-Az45brNV5xY
**pointer event**
https://developer.mozilla.org/en-US/docs/Web/CSS/pointer-events
**prefers-reduced-motion**
https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion
The prefers-reduced-motion CSS media feature is used to detect if the user has requested that the system minimize the amount of non-essential motion it uses.
**@media**
https://www.w3schools.com/cssref/css3_pr_mediaquery.asp
The `@media` rule is used in media queries to apply different styles for different media types/devices.
**animation**
https://developer.mozilla.org/en-US/docs/Web/CSS/animation
https://www.w3schools.com/css/css3_animations.asp

## App.js
**window**
https://developer.mozilla.org/en-US/docs/Glossary/Global_object
**jquery**
https://wiki.matbao.net/jquery-la-gi-tong-quan-ve-jquery-va-huong-dan-su-dung-jquery/
jQuery là thư viện được viết từ JavaScript, jQuery giúp xây dựng các chức năng bằng Javascript dễ dàng, nhanh và giàu tính năng hơn.
**window.$**
https://stackoverflow.com/questions/16922592/what-does-window-jquery-and-window-mean
**Suspense**
Suspense lets components “wait” for something before rendering. Today, Suspense only supports one use case: loading components dynamically with React.lazy. In the future, it will support other use cases like data fetching.
https://reactjs.org/docs/react-api.html#suspense
**Router hiểu rõ hơn**
https://fullstack.edu.vn/blog/phan-1routing-trong-reactjs-1.html
Đọc kỹ. Có hết
**react-toastify**
https://www.npmjs.com/package/react-toastify
**react-router or react-router-dom**
https://stackoverflow.com/questions/42684809/react-router-vs-react-router-dom-when-to-use-one-or-the-other
## i18n.js
Nope
## index.js / css
File css chưa hiểu lắm. Cần tìm hiểu thêm về sau. 
## reportWebVitals.js
https://create-react-app.dev/docs/measuring-performance/
Mot so cai lien quan den do dac hieu nang du an. xem theem
https://github.com/GoogleChrome/web-vitals
## setupTests.js
ko cos gi
## styles.scss
**What is WebKit and how is it related to CSS?**
https://stackoverflow.com/questions/3468154/what-is-webkit-and-how-is-it-related-to-css
Every browser is backed by a rendering engine to draw the HTML/CSS web page.

-   ~~IE → [Trident](http://en.wikipedia.org/wiki/Trident_%28layout_engine%29)~~ (discontinued)
-   Edge → ~~[EdgeHTML](https://en.wikipedia.org/wiki/EdgeHTML) (clean-up fork of Trident)~~ (Edge switched to [Blink](https://en.wikipedia.org/wiki/Blink_%28web_engine%29) in 2019)
-   Firefox → [Gecko](http://en.wikipedia.org/wiki/Gecko_%28layout_engine%29)
-   ~~Opera → [Presto](http://en.wikipedia.org/wiki/Presto_%28layout_engine%29)~~ (no longer uses Presto since Feb 2013, consider Opera = Chrome, therefore [Blink](https://en.wikipedia.org/wiki/Blink_%28web_engine%29) nowadays)
-   Safari → [WebKit](http://en.wikipedia.org/wiki/WebKit)
-   Chrome → [Blink](https://en.wikipedia.org/wiki/Blink_%28web_engine%29) (a fork of [Webkit](http://en.wikipedia.org/wiki/WebKit)).
# Thunder Client for VS Code
Hand-crafted lightweight Rest Client for Testing APIs
## 405 Method Not Allowed
The HyperText Transfer Protocol (HTTP) **`405 Method Not Allowed`** response status code indicates that the server knows the request method, but the target resource doesn't support this method.

# Create-react-app vs Nextjs
https://stackoverflow.com/questions/62967958/what-is-the-difference-between-nextjs-and-create-react-app
