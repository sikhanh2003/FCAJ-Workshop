---
title: "Sự kiện 11"
date: "2024-01-01"
weight: 11
chapter: false
pre: " <b> 4.11. </b> "
---

# Báo cáo Tổng kết: “BUILDING AGENTIC AI - Context Optimization with Amazon Bedrock”

### Mục tiêu Sự kiện

- Hiểu kiến trúc và khả năng của **Amazon Bedrock AgentCore**.
- Khám phá sự chuyển dịch từ các chatbots đơn giản sang **Agentic Workflows** có khả năng suy luận và thực thi phức tạp.
- Học cách tích hợp các external models (mô hình bên ngoài) và tối ưu hóa ngữ cảnh (context) cho các AI agents hiệu năng cao.
- **Hands-on Workshop:** Trải nghiệm sử dụng "Cloud Agents" (thông qua CloudThinker) để kết nối, truy xuất và phân tích các tài nguyên AWS để đưa ra các phát hiện (findings) về **Chi phí (Cost)** và **Bảo mật (Security)** có thể hành động được.

### Diễn giả

- **Mr. Nguyễn Gia Hưng** – Head of Solutions Architect, AWS
- **Mr. Kiên Nguyễn** – Solutions Architect, AWS
- **Mr. Việt Phạm** – Founder & CEO (Chia sẻ các use cases về Agentic Workflow thực tế)
- **Đội ngũ CloudThinker:** Mr. Thắng Tôn (COO), Mr. Henry Bùi (Head of Engineering)
- **Mr. Kha Văn** – Community Leader (Dẫn dắt phần Hands-on Workshop)

### Những Điểm nổi bật

#### 1. Bedrock AgentCore: Bộ máy Điều phối (Orchestration Engine)
Phiên chia sẻ của **Mr. Kiên Nguyễn** đã cung cấp cái nhìn sâu sắc về kỹ thuật của **Amazon Bedrock AgentCore**.
- **Tích hợp Vượt trội:** Tôi đã hiểu rõ tại sao AgentCore lại nổi bật. Nó không chỉ là việc gọi một LLM; mà là khả năng **tích hợp các external models** một cách mượt mà và định tuyến tác vụ hiệu quả.
- **Chức năng "Cốt lõi":** Nó xử lý các công việc nặng nhọc như bộ nhớ (memory), prompt engineering, và thực thi API, cho phép các developers tập trung vào business logic thay vì glue code.

#### 2. Xây dựng Agentic Workflows Thực tế
**Mr. Việt Phạm** đã trình bày hành trình xây dựng một agentic workflow trên AWS.
- Khác với các ví dụ lý thuyết, phiên này đã chứng minh các thách thức và giải pháp thực tế trong việc kết nối nhiều agents để thực hiện các tác vụ gắn kết.
- Nó đã thu hẹp khoảng cách giữa việc "có một LLM" và "có một nhân viên tự động hóa có thể hoạt động được".

#### 3. Đi sâu với CloudThinker & Cloud Agents
Trọng tâm của sự kiện đối với tôi là phần giới thiệu về **CloudThinker** và khái niệm **Cloud Agents** được trình bày bởi Mr. Thắng Tôn và Mr. Henry Bùi.
- **Tối ưu hóa Ngữ cảnh (Context Optimization):** Đã học cụ thể cách tối ưu hóa context window (mức độ L300) để các agents không bị quá tải khi xử lý lượng lớn dữ liệu hạ tầng.
- **Điều phối Agentic (Agentic Orchestration):** Cách nhiều agents phối hợp để hiểu trạng thái của môi trường cloud.

### Chương trình Sự kiện (Agenda)

- **9:00 - 9:10** | Khai mạc - *Nguyễn Gia Hưng*
- **9:10 - 9:40** | **AWS Bedrock AgentCore** - *Kiên Nguyễn*
    - Đi sâu vào các khả năng của AgentCore và tích hợp external model.
- **9:40 - 10:00** | **[Use Case] Xây dựng Agentic Workflow trên AWS** - *Việt Phạm*
- **10:00 - 10:40** | **CloudThinker: Orchestration & Context Optimization**
    - Giới thiệu bởi *Thắng Tôn*
    - Technical Deep Dive (L300) bởi *Henry Bùi*
- **10:40 - 11:00** | Nghỉ giải lao (Tea Break) & Networking
- **11:00 - 12:00** | **CloudThinker Hack: Hands-on Workshop** - *Kha Văn*
    - Kết nối agents tới tài nguyên AWS và phân tích để tối ưu hóa Cost/Sec.
- **12:00 Trở đi** | Networking & Ăn trưa

### Những Bài học Chính

#### Insight Kỹ thuật: Lợi thế của AgentCore
Tính năng nổi bật của Bedrock AgentCore là sự mạnh mẽ trong **model orchestration**. Nó trừu tượng hóa sự phức tạp của việc kết nối một LLM với các nguồn dữ liệu và API bên ngoài. Tôi đã hiểu rõ cách nó cho phép phương pháp tiếp cận "plug-and-play" cho các external models, đây là một lợi thế đáng kể so với việc xây dựng các lớp orchestration tùy chỉnh từ đầu.

#### Ứng dụng Thực tế: Mô hình "Cloud Agent"
Khái niệm sử dụng AI Agents để kiểm toán hạ tầng cloud là một bước ngoặt.
- Thay vì kiểm tra thủ công các dashboards, chúng ta coi trạng thái hạ tầng là "Ngữ cảnh" (Context).
- Agent truy xuất cấu hình tài nguyên, "đọc" nó dựa trên các best practices, và tạo ra các findings.

#### Trải nghiệm Workshop: Từ Truy xuất đến Kết quả (Findings)
Phiên thực hành do **Mr. Kha Văn** và đội ngũ CloudThinker dẫn dắt cực kỳ thực tế.
- **Kết nối:** Chúng tôi đã kết nối thành công CloudThinker với môi trường AWS của mình.
- **Truy xuất:** Các agents đã lấy dữ liệu tài nguyên (metadata, configurations).
- **Phân tích:** Phần ấn tượng nhất là thấy các agents phân tích dữ liệu này để đưa ra các đề xuất cụ thể về **Tối ưu hóa Chi phí** và **Bảo mật**. Nó không phải là lời khuyên chung chung; nó được điều chỉnh cho chính các tài nguyên mà chúng tôi đã quét. 

### Áp dụng vào Công việc

- **Thử nghiệm với AgentCore:** Bắt đầu tạo mẫu (prototyping) các công cụ nội bộ sử dụng Bedrock AgentCore để tận dụng khả năng tích hợp external model của nó.
- **Kiểm toán Tự động:** Khám phá phương pháp tiếp cận "Cloud Agent" cho các dự án của riêng tôi—xây dựng các agents đơn giản có thể truy vấn AWS APIs và tóm tắt tình trạng bảo mật hoặc các bất thường về chi phí một cách tự động.
- **Quản lý Ngữ cảnh:** Áp dụng các kỹ thuật tối ưu hóa ngữ cảnh đã học từ phiên của Henry Bùi để đảm bảo các ứng dụng AI của tôi duy trì hiệu năng và hiệu quả chi phí khi xử lý các tập dữ liệu lớn.

### Trải nghiệm Sự kiện

Sự kiện này đã cân bằng hoàn hảo giữa lý thuyết và thực hành. Từ cái nhìn tổng quan về kiến trúc của Kiên Nguyễn về Bedrock AgentCore đến việc thấy nó được áp dụng trong quy trình làm việc của Việt Phạm, và cuối cùng là tự tay thực hiện với CloudThinker/Kha Văn, đã củng cố kiến thức vững chắc.

Khả năng của **Cloud Agents** trong việc tự chủ quét, truy xuất và cung cấp các findings về Cost và Security là điều tôi dự định sẽ tìm hiểu sâu hơn. Nó chứng minh rằng Agentic AI đã sẵn sàng cho các vận hành phức tạp, không chỉ là hội thoại.

> **Suy nghĩ Cuối cùng:** Agentic AI đang chuyển dịch từ "Trò chuyện với dữ liệu" sang "Hành động trên hạ tầng". Khả năng tích hợp các external models và truy xuất ngữ cảnh cloud trực tiếp (live cloud context) là chìa khóa để mở khóa sức mạnh này.