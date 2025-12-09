---
title: "Proposal"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# APT Magic  
## Nền tảng AI Serverless cho tạo ảnh cá nhân hóa và tương tác xã hội

### 1. Tóm tắt điều hành
**APT Magic** là một ứng dụng web serverless sử dụng AI, cho phép người dùng tạo, tùy chỉnh và chia sẻ nội dung nghệ thuật như hình ảnh được tạo bởi mô hình AI. Nền tảng tích hợp trực tiếp với các foundation models thông qua **Amazon Bedrock**, đồng thời cung cấp trải nghiệm web mượt mà nhờ **Next.js (SSR)** được triển khai bằng **AWS Amplify**.

Phiên bản MVP tập trung vào việc tạo ảnh theo thời gian thực và chia sẻ nội dung, trong khi **Thiết kế Tương Lai** hướng đến khả năng mở rộng với **SageMaker Inference**, **Step Functions**, và quy trình **AWS MLOps** để tự động hóa quản lý mô hình và điều phối toàn hệ thống.

APT Magic hiện được phát triển với kiến trúc AWS-native hiện đại, tiết kiệm chi phí và an toàn, phù hợp cho lượng người dùng nhỏ đến trung bình; sau đó sẽ mở rộng thành nền tảng AI quy mô doanh nghiệp.

---

### 2. Vấn đề đặt ra
#### Thách thức là gì?
Hầu hết các nền tảng tạo ảnh AI đều tốn kém, phụ thuộc vào API của bên thứ ba và thiếu khả năng tùy chỉnh sâu.  
Nhà phát triển và người sáng tạo thường gặp vấn đề về độ trễ, thiếu minh bạch trong quản lý mô hình, và ít quyền kiểm soát dữ liệu người dùng.

#### Giải pháp
APT Magic sử dụng **kiến trúc serverless của AWS** để cung cấp:

- Tạo ảnh AI thời gian thực với mô hình **Amazon Bedrock – Stability AI**.  
- Xác thực người dùng và quản lý nội dung bảo mật với **Amazon Cognito** và **DynamoDB**.  
- Điều phối API linh hoạt bằng **AWS Lambda** và **API Gateway**.  
- Phân phối nội dung tốc độ cao với **CloudFront CDN** kết hợp **WAF** để bảo vệ.  

Các nâng cấp tương lai sẽ bao gồm **Step Functions**, **SQS/SNS**, **SageMaker Inference**, và CI/CD tiết kiệm chi phí với **CodeBuild**, **CodePipeline**, **CloudFormation** — biến APT Magic thành một nền tảng MLOps tự động hóa toàn diện.

---

### 3. Kiến trúc giải pháp

#### **Kiến trúc MVP**
MVP được xây dựng theo hướng **hoàn toàn serverless**, tập trung vào khả năng mở rộng, dễ bảo trì và tối ưu chi phí.

**Các dịch vụ AWS chủ chốt:**
- **Route53 + CloudFront + WAF** — đảm bảo truy cập toàn cầu an toàn và cache hiệu quả.
- **Amplify (Next.js SSR)** — triển khai giao diện và tầng server-side rendering.
- **API Gateway + Lambda Functions** — xử lý backend (image processing, subscription, post APIs).
- **Amazon Cognito** — Xác thực và phân quyền người dùng.
- **Amazon S3 + DynamoDB** — Lưu trữ dữ liệu và hình ảnh.
- **Amazon Bedrock** — Tích hợp mô hình tạo ảnh (Stability AI).
- **Secrets Manager, CloudWatch, CloudTrail** — Bảo mật, giám sát và ghi log.

**Bảo mật**
- **PrivateLink** cho kết nối an toàn giữa Lambda và backend services.  
- **WAF + IAM** để lọc truy cập và kiểm soát quyền chi tiết.  

![APT Magic MVP Architecture](/AWS-FCJ-Workshop-2025/images/2-Proposal/aptMagic_mvp.jpg)

---

#### **Thiết kế tương lai (Kiến trúc nâng cao)**
Ở giai đoạn tiếp theo, APT Magic sẽ phát triển thành **nền tảng điều phối AI**, bổ sung các lớp tự động hóa, độ bền hệ thống và quản lý vòng đời mô hình.

**Các dịch vụ sẽ được bổ sung:**
- **AWS Step Functions** — điều phối workflow bất đồng bộ như:
  - Tạo ảnh nhiều bước (kiểm tra prompt → inference → upload kết quả).
  - Xác nhận thanh toán → xử lý mô hình → gửi thông báo.
- **Amazon SQS** — truyền tải thông điệp giữa các Lambda async.
- **Amazon SNS** — gửi thông báo thời gian thực cho người dùng hoặc admin.
- **Amazon ElastiCache (Redis)** — caching và hạn chế tốc độ request.
- **Amazon SageMaker Inference** — triển khai các mô hình tùy chỉnh, fine-tuned.
- **AWS CodePipeline + SageMaker Pipelines** — tự động hóa toàn bộ MLOps.
- **AWS PrivateLink + VPC Endpoints** — đảm bảo dữ liệu đi trong mạng riêng.
- **AWS WAF & Shield Advanced** — bảo vệ khỏi DDoS và nâng cao an ninh.

- **CI/CD + MLOps**
  - **CodePipeline + CodeBuild + CloudFormation** để triển khai hạ tầng tự động.  

![APT Magic Future Architecture](/AWS-FCJ-Workshop-2025/images/2-Proposal/digram_architecture.jpg)

---

### 4. Triển khai kỹ thuật

#### **Các giai đoạn triển khai**
**Giai đoạn 1 – MVP (Hiện tại / Đã hoàn thành)**
- Triển khai Amplify (Next.js SSR) + API Gateway + Lambda.
- Tích hợp API Stability AI qua Bedrock.
- Thiết lập CI/CD bằng CodePipeline + CloudFormation.
- Kích hoạt Cognito cho user auth và S3 + DynamoDB để lưu trữ.

**Giai đoạn 2 – Mở rộng theo thiết kế tương lai**
- Thêm Step Functions + SQS/SNS để quản lý workflow AI bất đồng bộ.
- Tích hợp ElastiCache để caching và rate limiting.
- Kết nối SageMaker Inference cho các mô hình tùy chỉnh.
- Dùng SageMaker Pipelines để tự động training và deploy.
- Tăng cường bảo mật với Shield Advanced + GuardDuty + PrivateLink.
- Kết nối GitLab Runner với CodeBuild để hợp nhất CI/CD.

---

### 5. Timeline & Milestones

| Giai đoạn | Mô tả | Thời gian ước tính | Mốc triển khai (Milestone) |
|-----------|-------|--------------------|-----------------------------|
| **Tháng 1: Thiết lập & Core API** | Triển khai hạ tầng IaC, Cognito, API Gateway, DynamoDB, và các hàm Lambda cơ bản. | 4 Tuần | Core Backend hoạt động, Auth/User Management hoàn thành. |
| **Tháng 2: AI & Payment Integration** | Tích hợp LLM Claude Haiku 3 Amazon Bedrock (Stability AI), Replicate API hoàn thiện hàm *Image Processing* và tích hợp cổng thanh toán bên thứ ba. | 4 Tuần | Demo xử lý ảnh AI đầu cuối (end-to-end) thành công. |
| **Tháng 3: Front-end & CI/CD** | Phát triển UI/UX (Amplify/Next.js), hoàn thiện pipeline CI/CD, và cấu hình Giám sát/Bảo mật (CloudWatch/WAF). | 4 Tuần | Nền tảng hoàn chỉnh, sẵn sàng cho kiểm thử người dùng. |
| **Tháng 4: Tối ưu & Go-Live** | Kiểm thử hiệu năng (Stress Test), tối ưu chi phí, và triển khai Production. | 4 Tuần | **Go-Live** (Sản phẩm chính thức ra mắt). |


---

### 6. Ước tính chi phí (AWS Pricing Estimate)

#### Tổng Chi Phí
- **Hàng tháng:** $9.80  
- **Trả trước:** $0.00  
- **12 tháng:** $117.60  

---

#### Tổng quan dịch vụ

| Dịch vụ | Khu vực | Chi phí tháng | Trả trước | Chi phí 12 tháng | Ghi chú |
|--------|---------|---------------|-----------|-------------------|---------|
| Amazon Route 53 | Asia Pacific (Singapore) | $0.50 | $0.00 | $6.00 | 1 Hosted Zone, 1 domain, 1 VPC liên kết |
| Amazon CloudFront | Asia Pacific (Singapore) | $0.00 | $0.00 | $0.00 | Không có cấu hình cụ thể |
| AWS WAF | Asia Pacific (Singapore) | $6.00 | $0.00 | $72.00 | 1 Web ACL; 1 rule mỗi ACL |
| AWS Amplify | Asia Pacific (Singapore) | $0.00 | $0.00 | $0.00 | Build instance: Standard (8GB/4vCPU); thời lượng request 500ms |
| AWS CloudFormation | Asia Pacific (Singapore) | $0.00 | $0.00 | $0.00 | Không có extension; không có thao tác |
| Amazon API Gateway | Asia Pacific (Singapore) | $0.13 | $0.00 | $1.59 | 10k requests/tháng; message WebSocket 1KB; request size 30KB |
| AWS Lambda | Asia Pacific (Singapore) | $1.67 | $0.00 | $20.04 | 1 triệu invokes; x86; 512MB ephemeral storage |
| Amazon CloudWatch | Asia Pacific (Singapore) | $0.85 | $0.00 | $10.22 | 1 metric; 0.5GB logs in; 0.5GB logs tới S3 |
| S3 Standard | Asia Pacific (Singapore) | $0.23 | $0.00 | $2.76 | 10GB storage; 20k PUT; 40k GET |
| DynamoDB On-Demand | Asia Pacific (Singapore) | $0.42 | $0.00 | $5.04 | 1GB storage; item 1KB; chế độ on-demand |
| **Tổng (Ước tính)** | — | **$9.80** | **$0.00** | **$117.60** | Theo AWS Pricing Calculator |

---

#### Metadata
- **Tiền tệ:** USD  
- **Locale:** en_US  
- **Ngày tạo:** 12/9/2025  
- **Share URL:** [AWS Calculator Link](https://calculator.aws/#/estimate?id=f8f785603d5dea16be2d60ad39e4733fc352a108) 
- **Lưu ý pháp lý:** AWS Pricing Calculator chỉ cung cấp ước tính; chi phí thực tế có thể thay đổi theo mức sử dụng.

---

#### Bảng Giá Mô Hình AI

| Mô hình | Độ phân giải / Sử dụng Token | Chất lượng | Giá cho mỗi yêu cầu (USD) | Ghi chú |
|---------|-----------------------------|------------|---------------------------|---------|
| Titan Image Generator v2 | < 512×512 | Tiêu chuẩn | 0.008 | Giá cố định cho 1 ảnh |
| Titan Image Generator v2 | < 512×512 | Cao cấp | 0.01 | Giá cố định cho 1 ảnh |
| Titan Image Generator v2 | > 1024×1024 | Tiêu chuẩn | 0.01 | Giá cố định cho 1 ảnh |
| Titan Image Generator v2 | > 1024×1024 | Cao cấp | 0.012 | Giá cố định cho 1 ảnh |
| Stable Diffusion 3.5 Large | Bất kỳ | N/A | 0.08 | Giá cố định cho 1 ảnh |
| Claude (text + image) | 40 token đầu vào + 1 ảnh | N/A | 0.00195 | Giá cho 1 yêu cầu gồm văn bản và 1 ảnh 1024×1024 |

#### Tùy chọn bổ sung

| Chế độ | Tăng cường | Giá (USD) |
|--------|------------|-----------|
| text→img | không tăng cường | 0.08 |
| text→img | có tăng cường | 0.08195 |
| img→img | không tăng cường | 0.012 |
| img→img | có tăng cường | 0.094 |

 ---

### 7. Đánh giá rủi ro

| Rủi ro | Mức độ ảnh hưởng | Khả năng xảy ra | Giảm thiểu |
|--------|------------------|------------------|-------------|
| Độ trễ khi gọi mô hình AI | Trung bình | Cao | Dùng ElastiCache + Step Functions |
| Chi phí tăng vì inference | Cao | Trung bình | Kiểm soát Bedrock usage, autoscaling SageMaker |
| Lỗi cấu hình CI/CD | Trung bình | Thấp | Áp dụng rollback của CloudFormation |
| Lỗ hổng bảo mật | Cao | Trung bình | WAF, GuardDuty, PrivateLink, IAM least privilege |
| Phụ thuộc API bên thứ ba | Trung bình | Trung bình | Dùng fallback inference từ S3 |

---

### 8. Giá trị đạt được

#### Lợi ích kỹ thuật:
- Hoàn thiện pipeline serverless cho tạo ảnh AI.
- Nền tảng điều phối dễ mở rộng, phù hợp tích hợp MLOps.
- Cải thiện độ trễ và tính ổn định nhờ caching và workflows async.

#### Giá trị dài hạn:
- Nền tảng mở rộng lên mô hình **AI as a Service**.  
- Khung MLOps sẵn sàng cho tự động hóa training/retraining.  
- Hạ tầng tái sử dụng cho nhiều sản phẩm AI trong tương lai.

---


