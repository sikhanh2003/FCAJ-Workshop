---
title: "Sự kiện 7"
date: "2024-01-01"
weight: 7
chapter: false
pre: " <b> 4.7. </b> "
---

# Báo cáo Tổng kết: "AWS Cloud Mastery Series #2: DevOps on AWS"

### Mục tiêu Sự kiện

- Hiểu tư duy cốt lõi (core mindset) của DevOps bên cạnh các công cụ và CI/CD pipelines
- Khám phá mô hình "T-Shaped Skills" cho các cloud engineers hiện đại
- Đi sâu vào Infrastructure as Code (IaC) với CloudFormation và CDK
- Học các chiến lược tối ưu hóa chi phí (cost-optimization) thực tế cho AWS Amplify và Database hosting
- Khám phá các phương pháp kiểm thử hạ tầng (testing infrastructure) cục bộ (locally) và trực quan hóa các metrics thông qua CloudWatch

### Diễn giả

- **Đội ngũ AWS FCAJ (First Cloud Journey)**
- **Các chuyên gia DevOps AWS Việt Nam**

### Những Điểm nổi bật

#### DevOps là một Tư duy (Mindset), Không chỉ là Công cụ

Một trong những điểm mở đầu mạnh mẽ nhất là DevOps về cơ bản là văn hóa. Mặc dù công cụ là cần thiết, sự cộng tác giữa các vai trò mới là thứ thúc đẩy thành công.

- **T-Shaped Skills:** Buổi chia sẻ nhấn mạnh rằng các engineer nên đi sâu vào một lĩnh vực (thanh dọc) nhưng sở hữu kiến thức đủ rộng (thanh ngang) để cộng tác hiệu quả trong team.
- **Vai trò & Sự cộng tác:** Có được bức tranh rõ ràng hơn về cách các vai trò DevOps khác nhau tương tác trong dự án thực tế, chuyển từ lý thuyết sang làm việc nhóm thực tế.

#### Thông tin chi tiết về Hạ tầng & Công cụ Thực tế

Workshop đã đi xa hơn các định nghĩa chuẩn để cung cấp các mẹo cụ thể, "thực chiến" ("in-the-trenches"):

- **Lựa chọn IaC:** Củng cố việc sử dụng CloudFormation và AWS CDK để quản lý hạ tầng sạch sẽ, có thể lặp lại.
- **Chiến lược Amplify:** Một điểm nhấn chính là quyết định kiến trúc để host Frontend trên Amplify trong khi quản lý Backend thông qua CloudFormation (thay vì deploy full-stack Amplify) để kiểm soát và quản lý chi phí tốt hơn.

### Chương trình Sự kiện (Agenda)

#### **Phiên Buổi sáng (8:00 AM – 12:00 PM)**

- **8:00 – 9:00 AM** | Chào mừng & Văn hóa DevOps

  - Định nghĩa DevOps: Mindset vs. Toolset (Tư duy vs. Bộ công cụ)
  - Mô hình T-Shaped Skills cho developers
  - Hiểu các vai trò DevOps trong một team dự án

- **9:00 – 10:30 AM** | _Các nền tảng về CI/CD & Pipeline_

  - Tổng quan về CI/CD pipelines
  - Làm rõ: Tại sao DevOps lại hơn hẳn chỉ là CI/CD
  - **Demo:** Hướng dẫn chạy Pipeline (Pipeline walkthrough)

- **10:30 – 10:45 AM** | Nghỉ giải lao

- **10:45 AM – 12:00 PM** | _Infrastructure as Code (IaC)_

  - CloudFormation vs. Terraform (So sánh khái niệm)
  - Sử dụng AWS CDK cho hạ tầng có thể lập trình (programmable infrastructure)
  - **Mẹo:** Kiểm thử hạ tầng trước khi deploy lên cloud để giảm chi phí phát triển

- **12:00 – 1:00 PM** | Nghỉ trưa

---

#### **Phiên Buổi chiều (1:00 PM – 4:00 PM)**

- **1:00 – 2:30 PM** | _Các dịch vụ Hosting & Compute Nâng cao_

  - Khám phá sâu về AWS Amplify
  - Mẹo Kiến trúc: FE trên Amplify + BE thông qua CloudFormation/CDK
  - Database Hosting: Sử dụng EC2 cho databases vs. RDS (Các trường hợp sử dụng cụ thể)

- **2:30 – 2:45 PM** | Nghỉ giải lao

- **2:45 – 4:00 PM** | _Giám sát (Monitoring) & Khả năng quan sát (Observability)_

  - Đi sâu vào CloudWatch
  - **Kỹ thuật:** Nhúng CloudWatch metrics trực tiếp vào App UI (In-app dashboards)
  - Hỏi đáp (Q&A) & Tổng kết

### Những Bài học Chính

#### Những thông tin chiến lược về Văn hóa DevOps

- **Văn hóa là Tiên quyết:** DevOps là sự kết hợp của văn hóa, công cụ và kỷ luật vận hành. Sự thay đổi tư duy (mindset shift) quan trọng như việc triển khai kỹ thuật.
- **Phát triển Kỹ năng:** Áp dụng bộ kỹ năng T-Shaped là thiết yếu cho sự phát triển nghề nghiệp và cộng tác nhóm hiệu quả.
- **Phạm vi:** DevOps rộng hơn nhiều so với việc chỉ thiết lập một CI/CD pipeline; nó bao trùm toàn bộ vòng đời và các vòng phản hồi (feedback loops).

#### Các Mẹo Kỹ thuật Thực tế (Những "Viên ngọc ẩn")

- **Tối ưu hóa Chi phí với Amplify:** Thường hiệu quả về chi phí và linh hoạt hơn khi tách Frontend (Amplify) khỏi Backend (CloudFormation/CDK) thay vì dựa vào "phép màu" của Amplify cho mọi thứ.
- **Sự linh hoạt của Database:** Mặc dù RDS là tiêu chuẩn, có những kịch bản chính đáng mà việc host database trên EC2 là một chiến lược khả thi cho các ràng buộc cụ thể.
- **Kiểm thử Cục bộ (Local Testing):** Mã nguồn hạ tầng có thể và nên được kiểm thử trước khi deployment. Thực hành này giảm đáng kể chi phí cloud trong giai đoạn phát triển.
- **Tăng cường Observability:** Chúng ta có thể tận dụng CloudWatch để tạo các in-app dashboards, hiển thị các metrics liên quan trực tiếp cho người dùng hoặc admin UI, không chỉ trên AWS Console.

### Áp dụng vào Công việc

- **Áp dụng T-Shaped Learning:** Tập trung vào việc đào sâu chuyên môn cốt lõi của tôi trong khi tích cực học hỏi các công nghệ lân cận để hỗ trợ team tốt hơn.
- **Tinh chỉnh Quy trình IaC:** Triển khai kiểm thử hạ tầng local vào quy trình làm việc hiện tại để giảm thiểu tài nguyên cloud lãng phí.
- **Các quyết định Kiến trúc:** Đánh giá lại các dự án hiện tại để xem liệu mô hình "Amplify FE + Custom BE" có thể tối ưu hóa chi phí hay không.
- **Dashboarding:** Thử nghiệm việc kéo các CloudWatch metrics vào frontend ứng dụng để có khả năng hiển thị vận hành (operational visibility) tốt hơn.

### Trải nghiệm Sự kiện

Buổi chia sẻ này của đội ngũ AWS FCAJ cực kỳ rõ ràng và thực tế. Nó đã thành công trong việc thu hẹp khoảng cách giữa các khái niệm DevOps cấp cao và các chiến thuật kỹ thuật có thể hành động ngay.

#### Học hỏi từ các Chuyên gia

- Các diễn giả đã cung cấp những "lời nói thật" ("real talk") về kiến trúc, chẳng hạn như khi nào *không* nên sử dụng các dịch vụ được quản lý (managed services) nhất định (như full-stack Amplify) nếu nó không phù hợp với ngân sách hoặc các yêu cầu kiểm soát.
- Việc phân tích mô hình T-Shaped đã cho tôi một định hướng rõ ràng cho sự phát triển chuyên môn cá nhân.

#### Khả năng Áp dụng Thực tế

- Mẹo về việc kiểm thử hạ tầng local là một bước ngoặt (game-changer) cho quy trình phát triển của tôi.
- Trực quan hóa dữ liệu CloudWatch bên trong app là một tính năng tôi dự định triển khai ngay lập tức.

> Nhìn chung, buổi này đã củng cố sự hiểu biết của tôi về các nền tảng DevOps. Nó làm rõ rằng trong khi CI/CD là động cơ, thì văn hóa và các lựa chọn kiến trúc (như IaC và observability) chính là vô lăng điều khiển.---
title: "Sự kiện 7"
date: "2024-01-01"
weight: 7
chapter: false
pre: " <b> 4.7. </b> "
---

# Báo cáo Tổng kết: "AWS Cloud Mastery Series #2: DevOps on AWS"

### Mục tiêu Sự kiện

- Hiểu tư duy cốt lõi (core mindset) của DevOps bên cạnh các công cụ và CI/CD pipelines
- Khám phá mô hình "T-Shaped Skills" cho các cloud engineers hiện đại
- Đi sâu vào Infrastructure as Code (IaC) với CloudFormation và CDK
- Học các chiến lược tối ưu hóa chi phí (cost-optimization) thực tế cho AWS Amplify và Database hosting
- Khám phá các phương pháp kiểm thử hạ tầng (testing infrastructure) cục bộ (locally) và trực quan hóa các metrics thông qua CloudWatch

### Diễn giả

- **Đội ngũ AWS FCAJ (First Cloud Journey)**
- **Các chuyên gia DevOps AWS Việt Nam**

### Những Điểm nổi bật

#### DevOps là một Tư duy (Mindset), Không chỉ là Công cụ

Một trong những điểm mở đầu mạnh mẽ nhất là DevOps về cơ bản là văn hóa. Mặc dù công cụ là cần thiết, sự cộng tác giữa các vai trò mới là thứ thúc đẩy thành công.

- **T-Shaped Skills:** Buổi chia sẻ nhấn mạnh rằng các engineer nên đi sâu vào một lĩnh vực (thanh dọc) nhưng sở hữu kiến thức đủ rộng (thanh ngang) để cộng tác hiệu quả trong team.
- **Vai trò & Sự cộng tác:** Có được bức tranh rõ ràng hơn về cách các vai trò DevOps khác nhau tương tác trong dự án thực tế, chuyển từ lý thuyết sang làm việc nhóm thực tế.

#### Thông tin chi tiết về Hạ tầng & Công cụ Thực tế

Workshop đã đi xa hơn các định nghĩa chuẩn để cung cấp các mẹo cụ thể, "thực chiến" ("in-the-trenches"):

- **Lựa chọn IaC:** Củng cố việc sử dụng CloudFormation và AWS CDK để quản lý hạ tầng sạch sẽ, có thể lặp lại.
- **Chiến lược Amplify:** Một điểm nhấn chính là quyết định kiến trúc để host Frontend trên Amplify trong khi quản lý Backend thông qua CloudFormation (thay vì deploy full-stack Amplify) để kiểm soát và quản lý chi phí tốt hơn.

### Chương trình Sự kiện (Agenda)

#### **Phiên Buổi sáng (8:00 AM – 12:00 PM)**

- **8:00 – 9:00 AM** | Chào mừng & Văn hóa DevOps

  - Định nghĩa DevOps: Mindset vs. Toolset (Tư duy vs. Bộ công cụ)
  - Mô hình T-Shaped Skills cho developers
  - Hiểu các vai trò DevOps trong một team dự án

- **9:00 – 10:30 AM** | _Các nền tảng về CI/CD & Pipeline_

  - Tổng quan về CI/CD pipelines
  - Làm rõ: Tại sao DevOps lại hơn hẳn chỉ là CI/CD
  - **Demo:** Hướng dẫn chạy Pipeline (Pipeline walkthrough)

- **10:30 – 10:45 AM** | Nghỉ giải lao

- **10:45 AM – 12:00 PM** | _Infrastructure as Code (IaC)_

  - CloudFormation vs. Terraform (So sánh khái niệm)
  - Sử dụng AWS CDK cho hạ tầng có thể lập trình (programmable infrastructure)
  - **Mẹo:** Kiểm thử hạ tầng trước khi deploy lên cloud để giảm chi phí phát triển

- **12:00 – 1:00 PM** | Nghỉ trưa

---

#### **Phiên Buổi chiều (1:00 PM – 4:00 PM)**

- **1:00 – 2:30 PM** | _Các dịch vụ Hosting & Compute Nâng cao_

  - Khám phá sâu về AWS Amplify
  - Mẹo Kiến trúc: FE trên Amplify + BE thông qua CloudFormation/CDK
  - Database Hosting: Sử dụng EC2 cho databases vs. RDS (Các trường hợp sử dụng cụ thể)

- **2:30 – 2:45 PM** | Nghỉ giải lao

- **2:45 – 4:00 PM** | _Giám sát (Monitoring) & Khả năng quan sát (Observability)_

  - Đi sâu vào CloudWatch
  - **Kỹ thuật:** Nhúng CloudWatch metrics trực tiếp vào App UI (In-app dashboards)
  - Hỏi đáp (Q&A) & Tổng kết

### Những Bài học Chính

#### Những thông tin chiến lược về Văn hóa DevOps

- **Văn hóa là Tiên quyết:** DevOps là sự kết hợp của văn hóa, công cụ và kỷ luật vận hành. Sự thay đổi tư duy (mindset shift) quan trọng như việc triển khai kỹ thuật.
- **Phát triển Kỹ năng:** Áp dụng bộ kỹ năng T-Shaped là thiết yếu cho sự phát triển nghề nghiệp và cộng tác nhóm hiệu quả.
- **Phạm vi:** DevOps rộng hơn nhiều so với việc chỉ thiết lập một CI/CD pipeline; nó bao trùm toàn bộ vòng đời và các vòng phản hồi (feedback loops).

#### Các Mẹo Kỹ thuật Thực tế (Những "Viên ngọc ẩn")

- **Tối ưu hóa Chi phí với Amplify:** Thường hiệu quả về chi phí và linh hoạt hơn khi tách Frontend (Amplify) khỏi Backend (CloudFormation/CDK) thay vì dựa vào "phép màu" của Amplify cho mọi thứ.
- **Sự linh hoạt của Database:** Mặc dù RDS là tiêu chuẩn, có những kịch bản chính đáng mà việc host database trên EC2 là một chiến lược khả thi cho các ràng buộc cụ thể.
- **Kiểm thử Cục bộ (Local Testing):** Mã nguồn hạ tầng có thể và nên được kiểm thử trước khi deployment. Thực hành này giảm đáng kể chi phí cloud trong giai đoạn phát triển.
- **Tăng cường Observability:** Chúng ta có thể tận dụng CloudWatch để tạo các in-app dashboards, hiển thị các metrics liên quan trực tiếp cho người dùng hoặc admin UI, không chỉ trên AWS Console.

### Áp dụng vào Công việc

- **Áp dụng T-Shaped Learning:** Tập trung vào việc đào sâu chuyên môn cốt lõi của tôi trong khi tích cực học hỏi các công nghệ lân cận để hỗ trợ team tốt hơn.
- **Tinh chỉnh Quy trình IaC:** Triển khai kiểm thử hạ tầng local vào quy trình làm việc hiện tại để giảm thiểu tài nguyên cloud lãng phí.
- **Các quyết định Kiến trúc:** Đánh giá lại các dự án hiện tại để xem liệu mô hình "Amplify FE + Custom BE" có thể tối ưu hóa chi phí hay không.
- **Dashboarding:** Thử nghiệm việc kéo các CloudWatch metrics vào frontend ứng dụng để có khả năng hiển thị vận hành (operational visibility) tốt hơn.

### Trải nghiệm Sự kiện

Buổi chia sẻ này của đội ngũ AWS FCAJ cực kỳ rõ ràng và thực tế. Nó đã thành công trong việc thu hẹp khoảng cách giữa các khái niệm DevOps cấp cao và các chiến thuật kỹ thuật có thể hành động ngay.

#### Học hỏi từ các Chuyên gia

- Các diễn giả đã cung cấp những "lời nói thật" ("real talk") về kiến trúc, chẳng hạn như khi nào *không* nên sử dụng các dịch vụ được quản lý (managed services) nhất định (như full-stack Amplify) nếu nó không phù hợp với ngân sách hoặc các yêu cầu kiểm soát.
- Việc phân tích mô hình T-Shaped đã cho tôi một định hướng rõ ràng cho sự phát triển chuyên môn cá nhân.

#### Khả năng Áp dụng Thực tế

- Mẹo về việc kiểm thử hạ tầng local là một bước ngoặt (game-changer) cho quy trình phát triển của tôi.
- Trực quan hóa dữ liệu CloudWatch bên trong app là một tính năng tôi dự định triển khai ngay lập tức.

> Nhìn chung, buổi này đã củng cố sự hiểu biết của tôi về các nền tảng DevOps. Nó làm rõ rằng trong khi CI/CD là động cơ, thì văn hóa và các lựa chọn kiến trúc (như IaC và observability) chính là vô lăng điều khiển.