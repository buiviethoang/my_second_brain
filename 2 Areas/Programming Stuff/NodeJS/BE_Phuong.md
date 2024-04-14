# Test
## mocked
### ***cacheManager*
### ***config.service.mock*
### ***customerErrorHttp*
### ***emailConfirmation*
### ***jwt.service.mock*
### ***userData.mock*
## ***app.e2e-spec.ts*
## ***jest-e2e.json***
# Directory File
## ***Dockerfile*
đọc lại docker
## ***nest-cli.json*
https://docs.nestjs.com/cli/monorepo
đọc thêm ở đây
**Monorepo**
https://viblo.asia/p/monorepos-la-gi-va-tao-nhanh-mot-monorepos-bang-nx-RnB5pWwblPG
Microservices hiện nay được đề cập tới trong thế giới phần mềm, công nghệ được kỳ vọng cao và đánh giá như một xu hướng cho tương lai (Open API, service provider, …). Một số ý kiến cho rằng, microservices không có gì mới lạ, chẳng qua nó là SOA (kiến trúc hướng dịch vụ) được đánh bóng, đổi tên mà thôi. Mặc dù việc triển khai microservices dưới dạng multi-repo mang lại nhiều lợi ích tuy nhiên theo một số ý kiển, cách triển khai mã nguồn này có thể gây khó khăn trong một số trường hợp và thay vì triển khai cấu trúc mã nguồn dưới dạng chia thành nhiều repo riêng biệt, họ chọn cách tổ chức chỉ trong một repository duy nhất hay còn gọi là monorepo
## ***ormconfig.ts*
**ORM**
https://viblo.asia/p/object-relational-mapping-djeZ1PQ3KWz
Trong cách phát triển ứng dụng web hiện nay chắc hẳn các bạn đã quen với với từ khóa ORM(Object Relational Mapping). Khi mà thời đại của các framework ứng với các ngôn ngữ đang lên ngôi một cách mạnh mẽ, ORM gần như là sự lựa chọn tuyệt vời của các nhà phát triển hiện nay.

ORM giúp chúng ta dễ dàng thao tác với dữ liệu vớiDatabase hơn, giúp chúng ta dễ code, dễ maintain hơn . . . Ở bài viết này tôi sẽ giới thiệu chung về ORM, đi sâu vào phân tích các điểm ưu điểm, nhược điểm và khi nào áp dụng chúng trong các dự án thực tế.

Để cho dễ theo dõi từ thời điểm này của bài viết tôi xin được dùng ORM thay cho cụm từ Object Relational Mapping
**Dotenv**
https://viblo.asia/p/lam-viec-voi-environment-variables-trong-nodejs-maGK7ONeKj2
Nếu bạn quan tâm đến việc làm cho ứng dụng của bạn chạy trên bất kỳ máy tính hoặc cloud computing nào , thì bạn nên sử dụng Environment Variables để setting các giá trị cho từng môi trường mà bạn mong muốn.
**typeorm**
https://typeorm.io/
TypeORM is an ORM that can run in NodeJS, Browser, Cordova, PhoneGap, Ionic, React Native, NativeScript, Expo, and Electron platforms and can be used with TypeScript and JavaScript (ES5, ES6, ES7, ES8). Its goal is to always support the latest JavaScript features and provide additional features that help you to develop any kind of application that uses databases - from small applications with a few tables to large scale enterprise applications with multiple databases.
## ***tsconfig.build.json*
Cái này là mặc định của thằng nestjs nhé.  Xem thêm 
https://github.com/nestjs/typescript-starter/blob/master/tsconfig.build.json

{Lỗi git init xong không tạo nhánh mới ở github được
Git push -u -f origin main => Phải force mới được }

# Src
## auth
### dtos
#### dto? 
https://shareprogramming.net/dto-la-gi-dung-dto-trong-nhung-truong-hop-nao/
DTO hay tên gọi đầy đủ là Data Tranfer Object là một design pattern lần đầu tiên được giới thiệu bởi Martin Fowler trong cuốn sách EAA. Mục đích sử dụng chính của DTO đó là giảm số lần gọi các method giữa các tiến trình xử lý.
#### login
**class-validator**
https://www.npmjs.com/package/class-validator
Allows use of decorator and non-decorator based validation. Internally uses [validator.js](https://github.com/chriso/validator.js) to perform validation. Class-validator works on both browser and node.js platforms
#### refresh
#### userRegister
### guard
### interface
### strategy
## company
### dtos
### enum
## cronjob

## database
### migration
### **db.module.ts**
**repository design pattern**
https://viblo.asia/p/the-repository-design-pattern-AeJ1vONQGkby
Repository Pattern là lớp trung gian giữa tầng Business Logic và Data Access, giúp cho việc truy cập dữ liệu chặt chẽ và bảo mật hơn.
Repository đóng vai trò là một lớp kết nối giữa tầng Business và Model của ứng dụng.
Thông thường thì các phần truy xuất, giao tiếp với database năm rải rác ở trong code, khi bạn muốn thực hiện một thao tác lên database thì phải tìm trong code cũng như tìm các thuộc tính trong bảng để xử lý. Điều này gây lãng phí thời gian và công sức rất nhiều.
Với Repository design pattern, thì việc thay đổi ở code sẽ không ảnh hưởng quá nhiều công sức chúng ra chỉnh sửa.
## email
## emailConfirm
## enforce
## guards
## helper
## interceptors
## media
## otp
## permission
## position
## provinces
## question
**Repository.find()**
**In([...fields])**
## survey
**queryRunner.connect**
**queryRunner.startTransaction**
**queryRunner.manager.delete**
**queryRunner.insert().into().values().execute()**
**queryRunner.from().innerJoin().andSelect().getMany()**
## survey-result
### entity
**@PrimaryGeneratedColumn**
**@Column**
**@ManyToOne**
**@JoinColumn**
### service
**||**
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR
If expr1 can be converted to true, returns expr1; else, returns expr2.
***TypeORM***
**andWhere**
**addOrderBy**
**limit**
**offset**
**manager**
**createQueryRunner**
**connect**
**startTransaction**
**commitTransaction**
**rollbackTransaction**
**release**


**DeepPartial**
https://stackoverflow.com/questions/61132262/typescript-deep-partial
read link
**Promise.all()**
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all
This method can be useful for aggregating the results of multiple promises. It is typically used when there are multiple related asynchronous tasks that the overall code relies on to work successfully — all of whom we want to fulfill before the code execution continues.
**delete**
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete
The JavaScript delete operator removes a property from an object; if no more references to the same property are held, it is eventually released automatically.

**database transaction? **
https://fauna.com/blog/database-transaction
In short, a database transaction is a sequence of multiple operations performed on a database, and all served as a single logical unit of work — taking place wholly or not at all. In other words, there’s never a case that _only half of the operations_ are performed and the results save


## user
**@Expose**
https://docs.nestjs.com/techniques/serialization
You can use the @Expose() decorator to provide alias names for properties, or to execute a function to calculate a property value (analogous to getter functions), as shown below.
**@UseInterceptors**
https://docs.nestjs.com/interceptors
In order to set up the interceptor, we use the @UseInterceptors() decorator imported from the @nestjs/common package. Like pipes and guards, interceptors can be controller-scoped, method-scoped, or global-scoped.
**Content-disposition**
https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition
In a regular HTTP response, the Content-Disposition response header is a header indicating if the content is expected to be displayed inline in the browser, that is, as a Web page or as part of a Web page, or as an attachment, that is downloaded and saved locally.

**response.attachment()**
https://www.geeksforgeeks.org/express-js-res-attachment-function/
The **res.attachment()** function is used to set the HTTP response Content-Disposition header field to ‘attachment’. If the name of the file is given as filename, then it sets the Content-Type based on the extension name through res.type() function and finally sets the Content-Disposition ‘filename = ‘ parameter
**response.send()**
https://www.geeksforgeeks.org/express-js-res-send-function/
The **res.send()** function basically sends the HTTP response. The body parameter can be a String or a Buffer object or an object or an Array.
**ClassSerializerInterceptor**
https://docs.nestjs.com/techniques/serialization
Nest provides a built-in capability to help ensure that these operations can be performed in a straightforward way. The ClassSerializerInterceptor interceptor uses the powerful class-transformer package to provide a declarative and extensible way of transforming objects. The basic operation it performs is to take the value returned by a method handler and apply the instanceToPlain() function from class-transformer. In doing so, it can apply rules expressed by class-transformer decorators on an entity/DTO class, as described below.

**FileInterceptor**
https://docs.nestjs.com/techniques/file-upload
To upload a single file, simply tie the FileInterceptor() interceptor to the route handler and extract file from the request using the @UploadedFile() decorator

**@ApiConsume**
https://docs.nestjs.com/openapi/operations
You can enable file upload for a specific method with the @ApiBody decorator together with @ApiConsumes(). Here's a full example using the File Upload technique

**createReadStream**
https://nodejs.org/api/fs.html#filehandlecreatereadstreamoptions
**process.cwd()**
The `process.cwd()` method returns the current working directory of the Node.js process.
**join**
join all arguments together and normalize the resulting path.
**response.set**
Set header field to val, or pass an object of header fields.

Examples:

res.set('Foo', ['bar', 'baz']); res.set('Accept', 'application/json'); res.set({ Accept: 'text/plain', 'X-API-Key': 'tobi' });

Aliased as res.header().

**StreamableFile**
https://docs.nestjs.com/techniques/streaming-files
A StreamableFile is a class that holds onto the stream that is to be returned. To create a new StreamableFile, you can pass either a Buffer or a Stream to the StreamableFile constructor.

**@UploadedFile**
https://docs.nestjs.com/techniques/file-upload
To upload a single file, simply tie the FileInterceptor() interceptor to the route handler and extract file from the request using the @UploadedFile() decorator
**@Exclude**
https://docs.nestjs.com/techniques/serialization
Let's assume that we want to automatically exclude a `password` property from a user entity. We annotate the entity as follows:
**@JoinTable**
**Number()**
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
Number is a primitive wrapper object used to represent and manipulate numbers like 37 or -9.25.

The Number constructor contains constants and methods for working with numbers. Values of other types can be converted to numbers using the Number() function
**bcrypt**
https://en.wikipedia.org/wiki/Bcrypt
bcrypt is a password-hashing function designed by Niels Provos and David Mazières, based on the Blowfish cipher and presented at USENIX in 1999.[1] Besides incorporating a salt to protect against rainbow table attacks, bcrypt is an adaptive function: over time, the iteration count can be increased to make it slower, so it remains resistant to brute-force search attacks even with increasing computation power.

The bcrypt function is the default password hash algorithm for OpenBSD[2] and was the default for some Linux distributions such as SUSE Linux.[3]

**queryBuilder.distinct**
**queryBuilder.getRawMany**
## user-company-history
### controller
**@UseGuards**
https://docs.nestjs.com/guards
Đọc kỹ
**Error - typescript**
https://www.typescriptlang.org/docs/handbook/2/understanding-errors.html
**Unknown**
https://stackoverflow.com/questions/51439843/unknown-vs-any
Unknown can assign to any type
But other types except unknown and any cant be assigned to unknown
**(export) declare**
https://stackoverflow.com/questions/35019987/what-does-declare-do-in-export-declare-class-actions
var creates a new variable. declare is used to tell TypeScript that the variable has been created elsewhere. If you use declare, nothing is added to the JavaScript that is generated - it is simply a hint to the compiler.

For example, if you use an external script that defines var externalModule, you would use declare var externalModule to hint to the TypeScript compiler that externalModule has already been set up

**@Request, @Body, @Param**
**ParseIntPipe**
**TypeOrmModule.forFeature**

### service
**@InjectRepository**
**Entity, DTO, Domain model**
https://viblo.asia/p/entity-domain-model-va-dto-sao-nhieu-qua-vay-YWOZroMPlQ0
Đọc đi, hay đấy

***TypeORM*
**createQueryBuilder**
**leftJoinAndMapOne**
**leftJoinAndSelect**
**where**
**getManyAndCount**
**getOne**
**update**
**set**
**execute**
***Repository*
**Repository.save|create**
**Repository.findOneBy**
## utils
### emailTemplate
Nope
### exportUtil
**Exceljs**
https://www.npmjs.com/package/exceljs
Read, manipulate and write spreadsheet data and styles to XLSX and JSON.

Reverse engineered from Excel spreadsheet files as a project.

**js.unshift()**
https://www.w3schools.com/jsref/jsref_unshift.asp
Add new elements to an array

*Phần này khá đặc thù, đọc kỹ thư viện ExcelJS*

### otpTemplate
Nope
### utils
**Array.from**
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from
The Array.from() static method creates a new, shallow-copied Array instance from an iterable or array-like object.

**class-transformer**
https://github.com/typestack/class-transformer
Its ES6 and Typescript era. Nowadays you are working with classes and constructor objects more than ever. Class-transformer allows you to transform plain object to some instance of class and versa. Also it allows to serialize / deserialize object based on criteria. This tool is super useful on both frontend and backend.

**1=1 in SQL**
https://kiencang.net/sql-injection-la-gi/
SQL Injection dựa trên 1=1 là luôn luôn đúng

Chúng ta biết rằng, mục đích ban đầu của code là tạo ra một câu lệnh SQL để chọn một người dùng với môt id người dùng cho trước.

Nếu không có gì để ngăn chặn người dùng nhập “sai”, người dùng có thể nhập vào dữ liệu “thông minh” như thế này: 105 or 1=1
Kết quả của Server
SELECT * FROM Users WHERE UserId = 105 or 1=1

Câu lệnh SQL trên là hợp lệ. Nó sẽ trả về tất cả các hàng từ bảng Users, vì **WHERE 1=1** là luôn luôn đúng.

**Array.fill()**
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/fill
The fill() method changes all elements in an array to a static value, from a start index (default 0) to an end index (default array.length). It returns the modified array.


## main file
### ***app.controller.spec.ts***
The unit tests for the controller.
### ***app.controller.ts***
A basic controller with a single route.
### ***app.module.ts***
The root module of the application.
### ***app.service.ts***
A basic service with a single method.
### ***main.ts***
The entry file of the application which uses the core function `NestFactory` to create a Nest application instance.

### Dependency injection
https://viblo.asia/p/dependency-injection-la-gi-va-khi-nao-thi-nen-su-dung-no-LzD5d0d05jY
Dependency injection là một kĩ thuật trong đó một object (hoặc một static method) cung cấp các dependencies của một object khác. Một dependency là một object mà có thể sử dụng (một service). Tuy nhiên định nghĩa trên vẫn khá là khó hiểu, vậy nên hãy cùng tìm hiểu để hiểu rõ hơn về nó nào.

### process.env.TZ
https://stackoverflow.com/questions/8083410/how-can-i-set-the-default-timezone-in-node-js
According to this google group thread, you can set the TZ environment variable before calling any date functions. Just tested it and it works.
### preflight request
https://livebook.manning.com/book/cors-in-action/chapter-4/8
Let’s think about a preflight request in the context of the ATM example from chapter 3. Banks sometimes put their ATMs inside a room behind a locked door. The door can only be unlocked by swiping your ATM card (or if a kind person lets you in, but let’s ignore that for now). Once you’re inside, you can walk up to the ATM and withdraw money. The simple act of swiping your card to unlock the door doesn’t automatically give you money, but it’s a quick check to verify that you have permission to use the ATM.

In a similar fashion, a preflight request asks for the server’s permission to send the request. The preflight isn’t the request itself. Instead, it contains metadata about it, such as which HTTP method is used and if the client added additional request headers. The server inspects this metadata to decide whether the browser is allowed to send the request.
### app.enableCors
https://docs.nestjs.com/security/cors
Cross-origin resource sharing (CORS) is a mechanism that allows resources to be requested from another domain. Under the hood, Nest makes use of the Express cors package. This package provides various options that you can customize based on your requirements.

### cookie-parser
https://anonystick.com/blog-developer/cookie-parser-la-gi-middleware-can-thiet-ma-hoa-cookie-trong-expressjs-2020112687915577
Cookie parser là một thằng trung gian hay gọi là middleware trong Expressjs được sử dụng để phân tích cú pháp cookie và cũng là một phần mềm trung gian phổ biến khi những lập trình viên khởi tạo dự án sử dụng nodejs và expressjs

### DocumentBuilder
https://docs.nestjs.com/openapi/introduction
The OpenAPI specification is a language-agnostic definition format used to describe RESTful APIs. Nest provides a dedicated module which allows generating such a specification by leveraging decorators.


https://docs.nestjs.com/first-steps
Xem trên doc của nest