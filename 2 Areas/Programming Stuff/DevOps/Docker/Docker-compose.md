## Khái niệm
Là công cụ giúp ta thiết lập và quản lý nhiều container, network, volume (gọi chung là các service) và thiết lập cấu hình cho các service một cách nhanh chóng và đơn giản bằng việc chạy theo các chỉ định trong file docker-compose.yml
## Những chức năng chính
-   Tạo và quản lý nhiều môi trường độc lập trong một máy host đảm bảo độc lập các phân vùng ổ nhớ tránh say ra xung đột
-   Chỉ tạo lại container thay đổi, nhận biết các container không thay đổi và sử dụng lại
-   Định nghĩa và sử dụng biến môi trường trong file YAML
### Docker-compose.yml
Là một file lưu [dạng yaml](https://en.wikipedia.org/wiki/YAML), file này lưu các chỉ thị để docker compose đọc file này và thực thi các chỉ thị đó, các chỉ thị như tạo container từ image, tạo network, cấu hình cho các dịch vụ

**3 phần chính**: 
- phần đầu là khai báo phiên bản docker composer
- Phần tiếp theo là khai báo tạo các mạng
- Phần tiếp theo là tạo các services

Tạo xong file docker compose, giờ chúng ta sẽ run file này để tạo ra các service đã định nghĩa.

Ta vào thư mục chứa file docker-compose.yml và chạy lệnh

`docker-compose up`

Muốn dừng các services đang chạy thì ta dùng lệnh

`docker-compose stop`

Để kết thúc các services đang chạy và xóa hoàn toàn container ta dùng lệnh

`docker-compose down`

Theo dõi Logs các services

`docker-compose logs [SERVICES]`

```bash
version: '3'
services:
	web:
		# Path to dockerfile.
		# '.' represents the current directory in which
		# docker-compose.yml is present.
		build: .
		# Mapping of container port to host
		ports:
		- "5000:5000"
		# Mount volume
		volumes:
		- "/usercode/:/code"
		# Link database container to app container
		# for reachability.
		links:
		- "database:backenddb"
		
	database:
		# image to fetch from docker hub
		image: mysql/mysql-server:5.7
		# Environment variables for startup script
		# container will use these variables
		# to start the container with these define variables.
		environment:
		- "MYSQL_ROOT_PASSWORD=root"
		- "MYSQL_USER=testuser"
		- "MYSQL_PASSWORD=admin123"
		- "MYSQL_DATABASE=backend"
		# Mount init.sql file to automatically run
		# and create tables for us.
		# everything in docker-entrypoint-initdb.d folder
		# is executed as soon as container is up nd running.
		volumes:
		- "/usercode/db/init.sql:/docker-entrypoint-initdb.d/init.sql"
```

-   **`version ‘3’`:** This denotes that we are using version 3 of Docker Compose, and Docker will provide the appropriate features. At the time of writing this article, version 3.7 is latest version of Compose.
-   **`services`:** This section defines all the different containers we will create. In our example, we have two services, web and database.   
-   **`web`:** This is the name of our Flask app service. Docker Compose will create containers with the name we provide.   
-   **`build`:** This specifies the location of our Dockerfile, and `.` represents the directory where the `docker-compose.yml` file is located.
-   **`ports`:** This is used to map the container’s ports to the host machine.    
-   **`volumes`:** This is just like the `-v` option for mounting disks in Docker. In this example, we attach our code files directory to the containers’ `./code` directory. This way, we won’t have to rebuild the images if changes are made.    
-   **`links`:** This will link one service to another. For the bridge network, we must specify which container should be accessible to which container using links.    
-   **`image`:** If we don’t have a Dockerfile and want to run a service using a pre-built image, we specify the image location using the `image` clause. Compose will fork a container from that image.  
-   **`environment`:** The clause allows us to set up an environment variable in the container. This is the same as the `-e` argument in Docker when running a container

#### Addition reference
`health check`: Configure a check that’s run to determine whether or not containers for this service are “healthy
`dns`: Custom DNS servers. Can be a single value or a list.
`restart`: `no` is the default [restart policy](https://docs.docker.com/config/containers/start-containers-automatically/#use-a-restart-policy), and it does not restart a container under any circumstance. When `always` is specified, the container always restarts. The `on-failure` policy restarts a container if the exit code indicates an on-failure error. `unless-stopped` always restarts a container, except when the container is stopped (manually or otherwise).
``` 
domainname, hostname, ipc, mac_address, privileged, read_only, shm_size, stdin_open, tty, user, working_dir[🔗](https://docs.docker.com/compose/compose-file/compose-file-v3/#domainname-hostname-ipc-mac_address-privileged-read_only-shm_size-stdin_open-tty-user-working_dir)

Each of these is a single value, analogous to its [docker run](https://docs.docker.com/engine/reference/run/) counterpart. Note that `mac_address` is a legacy option.
```
`extra_hosts`: Add hostname mappings. Use the same values as the docker client `--add-host` parameter
An entry with the ip address and hostname is created in `/etc/hosts` inside containers for this service, e.g
![[Pasted image 20211223222845.png]]
`logging`: Logging configuration for the service
