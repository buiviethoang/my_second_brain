2025-08-23 09:23
Status: #baby
Tags: [[system design]]
## Main

OA (Service-Oriented Architecture – **Kiến trúc hướng dịch vụ**) là một phong cách kiến trúc phần mềm trong đó các **chức năng nghiệp vụ** của hệ thống được đóng gói thành các **dịch vụ** độc lập. Các dịch vụ này có thể được sử dụng lại, kết hợp, và giao tiếp với nhau thông qua các giao thức chuẩn (thường là mạng).

## 🌐 Đặc điểm chính của SOA

1. **Dịch vụ hóa (Service Abstraction)**
    
    - Chức năng nghiệp vụ được đóng gói thành dịch vụ, che giấu chi tiết bên trong.
        
2. **Khả năng tái sử dụng (Reusability)**
    
    - Dịch vụ có thể được dùng lại trong nhiều ứng dụng/hệ thống khác nhau.
        
3. **Khả năng tương tác (Interoperability)**
    
    - Các dịch vụ có thể giao tiếp với nhau bất kể nền tảng, ngôn ngữ hay công nghệ (thường qua SOAP, REST, XML, JSON, HTTP, JMS...).
        
4. **Tính lỏng lẻo (Loose Coupling)**
    
    - Giảm sự phụ thuộc giữa các dịch vụ; mỗi dịch vụ có thể thay đổi/triển khai độc lập.
        
5. **Khả năng tổ hợp (Composability)**
    
    - Dịch vụ nhỏ có thể kết hợp thành quy trình nghiệp vụ lớn (business process orchestration).


## 🏛 Thành phần trong kiến trúc SOA

1. **Service Provider (Nhà cung cấp dịch vụ)**
    
    - Cung cấp chức năng, công bố dịch vụ.
        
2. **Service Consumer (Người sử dụng dịch vụ)**
    
    - Ứng dụng hoặc dịch vụ khác gọi dịch vụ đã công bố.
        
3. **Service Registry/Repository (Đăng ký dịch vụ)**
    
    - Kho lưu trữ thông tin về các dịch vụ để consumer tìm kiếm.
        
4. **Service Bus (Enterprise Service Bus – ESB)**
    
    - Lớp trung gian để quản lý giao tiếp, tích hợp, điều phối (routing, transformation, security, monitoring).


## ⚙️ Ví dụ minh họa

Trong một hệ thống thương mại điện tử:

- **Dịch vụ Thanh toán (Payment Service)**
    
- **Dịch vụ Vận chuyển (Shipping Service)**
    
- **Dịch vụ Quản lý Khách hàng (Customer Service)**
    
- **Dịch vụ Kho hàng (Inventory Service)**
    

Các dịch vụ này hoạt động độc lập nhưng có thể phối hợp để hoàn thành quy trình “đặt hàng”.



## ✅ Ưu điểm

- Linh hoạt, dễ mở rộng và thay thế.
    
- Tái sử dụng cao.
    
- Dễ tích hợp hệ thống dị biệt.
    
- Hỗ trợ các quy trình nghiệp vụ phức tạp.
    

## ❌ Nhược điểm

- Triển khai phức tạp, chi phí cao.
    
- Hiệu năng có thể giảm do nhiều lớp trung gian.
    
- Cần cơ chế quản lý dịch vụ (governance) chặt chẽ.


👉 Ngày nay, SOA là “tiền thân” của **Microservices Architecture**, nhưng microservices đi xa hơn ở mức độ độc lập, triển khai tự động (CI/CD), và tính linh hoạt trong môi trường cloud-native.


![[Pasted image 20250823092619.png]]


![[Pasted image 20250823092758.png]]

### SOA vs Microservices

| Tiêu chí               | SOA (Service-Oriented Architecture)                                     | Microservices                                                                              |
| ---------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Phạm vi**            | Kiến trúc cấp **doanh nghiệp** – tích hợp nhiều hệ thống lớn khác nhau. | Kiến trúc cấp **ứng dụng** – chia nhỏ một ứng dụng thành các dịch vụ nhỏ.                  |
| **Kích thước dịch vụ** | Dịch vụ thường lớn (coarse-grained), có thể bao gồm nhiều chức năng.    | Dịch vụ rất nhỏ (fine-grained), tập trung vào **một chức năng** duy nhất.                  |
| **Cơ chế giao tiếp**   | Chủ yếu dùng **ESB (Enterprise Service Bus)**, SOAP, XML.               | Chủ yếu dùng **API REST/HTTP, gRPC, JSON**, messaging (Kafka, RabbitMQ).                   |
| **Kết nối**            | Có xu hướng **chặt chẽ hơn** vì phụ thuộc ESB.                          | **Lỏng lẻo hơn** (API trực tiếp, event-driven, không phụ thuộc bus trung tâm).             |
| **Triển khai**         | Thường triển khai tập trung, nặng nề.                                   | Dịch vụ triển khai độc lập, tự động hóa (CI/CD, container, Kubernetes).                    |
| **Quản lý dữ liệu**    | Dữ liệu thường được **chia sẻ qua DB chung**.                           | Mỗi microservice quản lý **DB riêng** (Database per Service).                              |
| **Khả năng mở rộng**   | Mở rộng theo **toàn bộ dịch vụ** lớn.                                   | Mở rộng **từng microservice** riêng biệt.                                                  |
| **Công nghệ**          | Thường dùng trong hệ thống truyền thống: SOAP, WSDL, ESB.               | Gắn liền với cloud-native: Docker, Kubernetes, REST/gRPC, CI/CD.                           |
| **Độ phức tạp**        | Quản trị dịch vụ, governance phức tạp.                                  | Quản lý nhiều dịch vụ nhỏ, cần DevOps mạnh.                                                |
| **Ví dụ**              | Tích hợp hệ thống ngân hàng, ERP, CRM.                                  | Netflix, Uber, Amazon – mỗi chức năng (auth, payment, recommendation) là một microservice. |

- **SOA**: Giải pháp lớn, nặng, thích hợp cho **tích hợp hệ thống doanh nghiệp**.
    
- **Microservices**: Nhẹ, linh hoạt, phù hợp cho **ứng dụng hiện đại, cloud-native**.


## References