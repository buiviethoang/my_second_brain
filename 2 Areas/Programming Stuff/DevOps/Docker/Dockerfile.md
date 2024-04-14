### FROM
Chỉ định rằng image nào sẽ được dùng làm image cơ sở để quá trình build image thực thiện các câu lệnh tiếp theo. Các image base này sẽ được tải về từ Public Repository hoặc Private Repository riêng của mỗi người tùy theo setup
**Cú pháp**
```none
FROM <image> [AS <name>]
FROM <image>[:<tag>] [AS <name>]
FROM <image>[@<digest>] [AS <name>]
```
```none
FROM ubuntu
hoặc
FROM ubuntu:latest
```
### LABEL
Chỉ thị **LABEL** được dùng để thêm các thông tin meta vào **Docker Image** khi chúng được build. Chúng tồn tại dưới dạng các cặp _key_ - _value_, được lưu trữ dưới dạng chuỗi. Có thể chỉ định nhiều label cho một Docker Image, và tất nhiên mỗi cặp _key_ - _value_ phải là duy nhất. Nếu cùng một _key_ mà được khai báo nhiều giá trị (value) thì giá trị được khai báo gần đây nhất sẽ ghi đè lên giá trị trước đó.
```none
LABEL <key>=<value> <key>=<value> <key>=<value> ... <key>=<value> 
```
```none
LABEL com.example.some-label="lorem"
LABEL version="2.0" description="Lorem ipsum dolor sit amet, consectetur adipiscing elit."
```
Để xem thông tin meta của một Docker Image, ta sử dụng dòng lệnh:
```none
docker inspect <image id>
```
### MAINTAINER
Chỉ thị **MAINTAINER** dùng để khai báo thông tin tác giả người viết ra file Dockerfile.
```none
MAINTAINER <name> [<email>]
```
```none
MAINTAINER NamDH <namduong3699@gmail.com>
```
Hiện nay, theo tài liệu chính thức từ bên phía [Docker](https://docs.docker.com/engine/reference/builder/#maintainer-deprecated) thì việc khai báo **MAINTAINER** đang dần được thay thế bằng **LABEL maintainer** bới tính linh hoạt của nó khi ngoài thông tin về tên, email của tác giả thì ta có thể thêm nhiều thông tin tùy chọn khác qua các thẻ metadata và có thể lấy thông tin dễ dàng với câu lệnh `docker inspect ...`.

### RUN
Chỉ thị **RUN** dùng để chạy một lệnh nào đó trong quá trình build image và thường là các câu lệnh Linux. Tùy vào image gốc được khai báo trong phần **FROM** thì sẽ có các câu lệnh tương ứng. Ví dụ, để chạy câu lệnh update đối với Ubuntu sẽ là `RUN apt-get update -y` còn đối với CentOS thì sẽ là `Run yum update -y`. Kết quả của câu lệnh sẽ được commit lại, kết quả commit đó sẽ được sử dụng trong bước tiếp theo của Dockerfile
```none
RUN <command>
RUN ["executable", "param1", "param2"]
```
```none
RUN /bin/bash -c 'source $HOME/.bashrc; echo $HOME'
-------- hoặc --------
RUN ["/bin/bash", "-c", "echo hello"]
```
Ở cách thức `shell form` bạn có thể thực hiện nhiều câu lệnh cùng một lúc với dấu `\`:
```none
FROM ubuntu
RUN apt-get update
RUN apt-get install curl -y
```
Hoặc: 
```none
FROM ubuntu
RUN apt-get update; \
    apt-get install curl -y
```

### ADD
Chỉ thị **ADD** sẽ thực hiện sao chép các tập, thư mục từ máy đang build hoặc remote file URLs từ `src` và thêm chúng vào filesystem của image `dest`.
```none
ADD [--chown=<user>:<group>] <src>... <dest>
ADD [--chown=<user>:<group>] ["<src>",... "<dest>"]
```
-   **src** có thể khai báo nhiều file, thư mục, …
-   **dest** phải là đường dẫn tuyệt đối hoặc có quan hệ chỉ thị đối với WORKDIR.

```none
ADD hom* /mydir/
ADD hom?.txt /mydir/
ADD test.txt relativeDir/
```
```none
ADD --chown=55:mygroup files* /somedir/
ADD --chown=bin files* /somedir/
ADD --chown=1 files* /somedir/
ADD --chown=10:11 files* /somedir/
```
### COPY
Chỉ thị **COPY** cũng giống với **ADD** là copy file, thư mục từ `<src>` và thêm chúng vào `<dest>` của container. Khác với **ADD**, nó không hỗ trợ thêm các file remote file URLs từ các nguồn trên mạng.
```none
COPY [--chown=<user>:<group>] <src>... <dest>
COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]
```

### ENV
Chỉ thị **ENV** dùng để khai báo các biến môi trường. Các biến này được khai báo dưới dạng _key_ - _value_ bằng các chuỗi. Giá trị của các biến này sẽ có hiện hữu cho các chỉ thị tiếp theo của Dockerfile.
```none
ENV <key>=<value> ...
```
```none
ENV DOMAIN="viblo.asia"
ENV PORT=80
ENV USERNAME="namdh" PASSWORD="secret"
```
Ngoài ra cũng có thể thay đổi giá trị của biến môi trường bằng câu lệnh khởi động container:
```none
docker run --env <key>=<value>
```
**ENV** chỉ được sử dụng trong các command sau:
-   ADD
-   COPY
-   ENV
-   EXPOSE
-   FROM
-   LABEL
-   STOPSIGNAL
-   USER
-   VOLUME
-   WORKDIR

### CMD
Chỉ thị **CMD** định nghĩa các câu lệnh sẽ được chạy sau khi container được khởi động từ image đã build. Có thể khai báo được nhiều nhưng chỉ có duy nhất **CMD** cuối cùng được chạy.
```none
CMD ["executable","param1","param2"]
CMD ["param1","param2"] 
CMD command param1 param2
```
```none
FROM ubuntu
CMD echo Viblo
```
### USER
Có tác dụng set `username` hoặc `UID` để sử dụng khi chạy image và khi chạy các lệnh có trong `RUN`, `CMD`, `ENTRYPOINT` sau nó.
```none
USER <user>[:<group>]
hoặc
USER <UID>[:<GID>]
```
```none
FROM alpine:3.4
RUN useradd -ms /bin/bash namdh
USER namdh
```
### EXPOSE
```
EXPOSE <port> [<port>/<protocol>...]
```
The `EXPOSE` instruction informs Docker that the container listens on the specified network ports at runtime. You can specify whether the port listens on TCP or UDP, and the default is TCP if the protocol is not specified.

### WORKDIR
The **`WORKDIR` command** is used to define the _working directory_ of a Docker container at any given time. The command is specified in the Dockerfile.
```
WORKDIR /project
```
