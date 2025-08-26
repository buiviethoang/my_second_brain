2025-08-23 21:56
Status: #baby
Tags: 
## Main

CI/CD là viết tắt của **Continuous Integration (CI)** và **Continuous Delivery/Deployment (CD)** – một tập hợp các thực hành trong phát triển phần mềm giúp tự động hóa và rút ngắn chu trình phát triển, kiểm thử, và triển khai.

## **Continuous Integration (CI)**

- **Ý tưởng:** Lập trình viên thường xuyên (thậm chí nhiều lần mỗi ngày) tích hợp code của mình vào nhánh chính (main/master).
    
- **Công việc chính:**
    
    - Tự động build ứng dụng.
        
    - Tự động chạy test (unit test, integration test).
        
    - Phát hiện lỗi sớm khi merge code.
        
- **Lợi ích:**
    
    - Giảm rủi ro “conflict lớn” khi nhiều dev merge cùng lúc.
        
    - Đảm bảo code luôn ở trạng thái build/test được.

## **Continuous Delivery (CD)**

- **Ý tưởng:** Code sau khi vượt qua pipeline CI có thể **triển khai đến môi trường staging hoặc production bất cứ lúc nào** (nhưng vẫn cần thao tác _deploy_ thủ công).
    
- **Mục tiêu:** Luôn giữ phần mềm ở trạng thái có thể phát hành.


## **Continuous Deployment (CD)**

- **Ý tưởng:** Nâng cao hơn so với Delivery – sau khi qua CI pipeline, code sẽ **tự động deploy** sang production **mà không cần can thiệp thủ công**.
    
- **Ví dụ:** Commit → CI pipeline chạy test → Build Docker image → Deploy production tự động.

## **Pipeline CI/CD thường có:**

1. **Source**: Code được commit/push lên GitHub/GitLab/Bitbucket.
    
2. **Build**: Compile, build artifact (JAR, Docker image...).
    
3. **Test**: Unit test, integration test, UI test.
    
4. **Package**: Đóng gói, đẩy artifact lên repository (Nexus, Artifactory, Docker Registry).
    
5. **Deploy**: Triển khai lên dev/staging/production.
    
6. **Monitor**: Theo dõi log, metrics, cảnh báo.

## **Công cụ CI/CD phổ biến**

- **CI/CD server**: Jenkins, GitLab CI/CD, GitHub Actions, CircleCI, TravisCI, Azure DevOps.
    
- **Deploy**: Docker, Kubernetes, Helm, ArgoCD, Spinnaker.
    
- **Monitoring**: Prometheus, Grafana, ELK stack.



## References