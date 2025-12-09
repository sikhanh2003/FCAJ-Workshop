---
title: "Sự kiện 10"
date: "2024-01-01"
weight: 10
chapter: false
pre: " <b> 4.10. </b> "
---

# Báo cáo Tổng kết: "AWS Cloud Mastery Series #3: The Security Pillar"

### Mục tiêu Sự kiện

- Phân tích **AWS Well-Architected Security Pillar** thành các nhiệm vụ kỹ thuật (engineering tasks) có thể thực hiện được.
- Chuyển đổi tư duy từ "Perimeter Security" (Bảo mật vành đai) sang **"Identity-Centric Security"** (Bảo mật tập trung vào định danh).
- Phân tích các vector mối đe dọa cloud (cloud threat vectors) cụ thể phổ biến tại thị trường Việt Nam.
- Nắm vững vòng đời **Automated Incident Response** (Phản hồi sự cố tự động) (Detect -> Isolate -> Investigate -> Recover).
- Thiết lập lộ trình triển khai các kiến trúc **Defense-in-Depth** và **Zero Trust**.

### Đối tượng Tham gia

- **Chính:** Cloud Architects & Security Engineers chịu trách nhiệm gia cố hạ tầng (infrastructure hardening).
- **Phụ:** DevOps Engineers & Developers mong muốn triển khai "Security by Design".

### Những Điểm nổi bật

#### "Bối cảnh Việt Nam" & Trách nhiệm chung

Buổi chia sẻ bắt đầu với cái nhìn thực tế về bối cảnh địa phương. Các diễn giả nhấn mạnh rằng trong khi AWS quản lý bảo mật *của* (of) đám mây, khách hàng thường thất bại trong bảo mật *bên trong* (in) đám mây do những cấu hình sai đơn giản.
- **Insight Chính:** Các vụ vi phạm phổ biến nhất tại Việt Nam không đến từ các khai thác zero-day, mà từ các access keys bị lộ và các S3 buckets bị cấp quyền quá rộng (overly permissive).
- **Thay đổi Tư duy:** Bảo mật không phải là "người gác cổng" (gatekeeper) làm chậm quá trình phát triển; nó là "người kiến tạo" (enabler) cho phép các team di chuyển nhanh với sự tự tin.

#### 5 Trụ cột Phòng thủ

Cốt lõi của workshop đã mổ xẻ bảo mật thành 5 lớp riêng biệt, chuyển từ phòng ngừa sang phản ứng:

1.  **Identity (Firewall kiểu mới):** Nếu identity bị xâm phạm, network firewalls sẽ trở nên vô dụng.
2.  **Detection (Phát hiện):** Bạn không thể chiến đấu với những gì bạn không thấy. 
3.  **Infrastructure:** Giảm thiểu phạm vi ảnh hưởng (blast radius).
4.  **Data:** Bảo vệ "tài sản cốt lõi" (crown jewels) thông qua mã hóa (encryption).
5.  **Incident Response:** Phản hồi thủ công quá chậm; code phải chiến đấu với code.

### Chương trình Sự kiện (Agenda)

#### **Nền tảng & Identity**

- **08:30 – 08:50** | **Thực tế về các mối đe dọa Cloud**
  - Hiểu sâu sắc về "Shared Responsibility Model" (Mô hình Trách nhiệm chung).
  - Các case study về những cấu hình sai phổ biến.

- **08:50 – 09:30** | **Trụ cột 1: Identity & Access Management (IAM)**
  - Chuyển dịch khỏi Long-term Access Keys (IAM Users).
  - Áp dụng Temporary Credentials (IAM Roles & Identity Center).
  - **Quy tắc cứng:** Áp dụng Least Privilege (Quyền tối thiểu) và bắt buộc MFA ở mọi nơi.

#### **Khả năng quan sát (Visibility) & Gia cố (Hardening)**

- **09:30 – 10:10** | **Trụ cột 2: Detection & Monitoring**
  - Tập trung hóa logs với CloudTrail & Security Hub.
  - Sử dụng GuardDuty để phát hiện mối đe dọa thông minh.
  - **Mẫu (Pattern):** Detection-as-Code (tự động hóa cảnh báo).

- **10:10 – 10:40** | **Trụ cột 3: Bảo vệ Hạ tầng (Infrastructure Protection)**
  - Chiến lược phân đoạn mạng (Network segmentation) (Public vs. Private subnets).
  - Bảo vệ Layer 7 với AWS WAF & Shield.

#### **Dữ liệu & Phản hồi**

- **10:40 – 11:10** | **Trụ cột 4: Bảo vệ Dữ liệu (Data Protection)**
  - Mã hóa lưu trữ (at rest) (KMS) và đường truyền (in transit) (TLS).
  - Quản lý xoay vòng secrets với Secrets Manager.

- **11:10 – 11:40** | **Trụ cột 5: Incident Response (IR)**
  - Xây dựng các IR Playbooks tự động (ví dụ: tự động thu hồi credentials bị xâm phạm).
  - Điều tra số sau sự cố (Post-incident forensics): Snapshotting và cô lập (isolation).

- **11:40 – 12:00** | **Tổng kết & Lộ trình**

### Những Bài học Chính (The Security Playbook)

#### 1. Identity là Tuyến phòng thủ Đầu tiên
- **Ngừng sử dụng IAM Users:** Chuyển sang **IAM Identity Center (SSO)**. Các thông tin xác thực tĩnh dài hạn (Long-term static credentials) là một gánh nặng rủi ro.
- **Sử dụng SCPs:** Service Control Policies (SCPs) đóng vai trò là "guardrails" (thanh chắn bảo vệ) cho toàn bộ tổ chức, ngăn chặn bất kỳ ai (kể cả admin) thực hiện các hành động nguy hiểm như tắt CloudTrail.

#### 2. Encryption là Tuyến phòng thủ Cuối cùng
- Ngay cả khi mạng bị xâm nhập và identity bị đánh cắp, dữ liệu vẫn phải ở trạng thái không thể đọc được.
- **KMS là cực kỳ quan trọng:** Hiểu về Key Policies và việc xoay vòng (rotation) là bắt buộc đối với bất kỳ kiến trúc sư nào.

#### 3. Automation là Cách duy nhất để mở rộng quy mô Phản hồi
- Thời gian phản ứng của con người được đo bằng phút/giờ; các cuộc tấn công của bot được đo bằng mili giây.
- **EventBridge + Lambda:** Chúng tôi đã học các pattern để tự động cô lập một EC2 instance hoặc thu hồi một IAM role ngay khi GuardDuty phát hiện mối đe dọa.

#### 4. Chia để trị (Segmentation)
- Không bao giờ đặt mọi thứ trong một VPC hoặc một Account.
- Sử dụng **VPC Segmentation** và **Security Groups** để đảm bảo rằng nếu một thành phần bị xâm phạm, kẻ tấn công không thể di chuyển ngang (move laterally) sang các thành phần khác.

### Áp dụng vào Công việc

- **Kiểm toán ngay lập tức:** Chạy *IAM Access Analyzer* để xác định các roles không sử dụng và các truy cập từ bên ngoài.
- **Ghi log mọi thứ:** Đảm bảo CloudTrail được bật ở *tất cả* các regions, không chỉ các region đang hoạt động.
- **Vệ sinh Secret (Secret Hygiene):** Loại bỏ tất cả API keys được hardcoded trong code và di chuyển chúng sang AWS Secrets Manager.
- **Tinh chỉnh WAF:** Xem xét lại các rules của WAF để đảm bảo rate-limiting đang hoạt động nhằm ngăn chặn các cuộc tấn công DDoS/Brute-force đơn giản.

### Trải nghiệm Sự kiện

Workshop này là một lời nhắc nhở mạnh mẽ rằng **Bảo mật là một quá trình liên tục, không phải là đích đến**.

#### Từ Lý thuyết đến Thực hành
Buổi chia sẻ đã làm rất tốt việc giải mã các chủ đề phức tạp như "Zero Trust". Thay vì các từ khóa sáo rỗng (buzzwords), chúng tôi đã thấy các triển khai thực tế: security groups chặt chẽ, temporary credentials, và logging nghiêm ngặt.

#### Giá trị của Tự động hóa
Điều ấn tượng nhất là **Incident Response automation**. Việc chứng kiến một Lambda function tự động ngăn chặn (contain) một mối đe dọa mô phỏng đã làm nổi bật khoảng cách giữa "monitoring" (theo dõi màn hình) và "observability/response" (hệ thống tự phục hồi).

> **Suy nghĩ Cuối cùng:** "Trên đám mây, bạn không bảo vệ vành đai; bạn bảo vệ dữ liệu và định danh." Buổi chia sẻ này đã cung cấp bản thiết kế (blueprint) để làm chính xác điều đó.