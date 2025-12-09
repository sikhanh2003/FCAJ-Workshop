---

title: "Sự kiện 6"
date: "2024-01-01"
weight: 6
chapter: false
pre: " <b> 4.6. </b> "
----------------------

# Báo cáo Tổng kết: “AWS Cloud Mastery Series #1: AI/ML/GenAI on AWS”

### Mục tiêu Sự kiện

* Cung cấp góc nhìn thực tiễn và mang tính chiến lược về AI/ML và Generative AI trên AWS
* Trình bày cách tích hợp các foundation model và dịch vụ pretrained vào giải pháp doanh nghiệp
* Giới thiệu best practices về prompt engineering, RAG (Retrieval-Augmented Generation) và orchestration cho các ứng dụng production
* Giúp người tham dự tiếp cận các công cụ tăng tốc AI của AWS như Bedrock và các dịch vụ liên quan
* Trang bị hướng dẫn thiết thực để thiết kế hệ thống AI có tính mở rộng, an toàn và tối ưu chi phí trên cloud

### Diễn giả

* Đội ngũ giảng viên và kỹ sư AWS Cloud Mastery Series (AWS Vietnam)
* Nhóm facilitators phụ trách demo kỹ thuật Amazon Bedrock và SageMaker

### Điểm nổi bật

#### Tổng quan Hệ sinh thái AI/ML của AWS

Buổi workshop mở đầu bằng bản đồ hệ thống AI/ML của AWS, giúp làm rõ cách các lớp dịch vụ phối hợp:
từ pretrained services để prototyping nhanh, đến SageMaker cho vòng đời mô hình, và Bedrock cho các ứng dụng GenAI nâng cao.

#### Generative AI với Amazon Bedrock

Phần trọng tâm tập trung vào Bedrock và các mô hình GenAI cho doanh nghiệp:

* So sánh và lựa chọn foundation models (Claude, Llama, Titan) dựa trên chi phí, độ trễ, khả năng suy luận và mức độ phù hợp doanh nghiệp.
* Best practices trong prompt engineering: prompt có cấu trúc, chain-of-thought, few-shot để tăng độ ổn định.
* Kiến trúc RAG: kết hợp knowledge base giúp tăng tính xác thực và giảm hallucination.
* Bedrock Agentcore: điều phối workflow phức tạp, hỗ trợ reasoning nhiều bước và tích hợp tool.

#### Dịch vụ AI Pretrained & Công cụ Thực hành

Workshop cũng trình bày các dịch vụ AI sẵn dùng để xây dựng nhanh ứng dụng mà không cần huấn luyện mô hình:

* Amazon Comprehend — phân tích văn bản, NLP
* Amazon Rekognition — phân tích ảnh và video
* Amazon Textract — OCR và trích xuất tài liệu
* Amazon Translate / Transcribe / Polly — dịch thuật, chuyển giọng nói, đọc văn bản
* Amazon Kendra — tìm kiếm doanh nghiệp
* Amazon Personalize — gợi ý và cá nhân hóa

Diễn giả đặc biệt nhấn mạnh khi nào nên dùng pretrained service và khi nào cần custom model.

### Lịch trình Sự kiện

**8:30 – 9:00 AM** | Welcome & Introduction
• Giao lưu & networking
• Overview mục tiêu học tập
• Ice-breaker
• Tổng quan bức tranh AI/ML tại Việt Nam

**9:00 – 10:30 AM** | *AWS AI/ML Services Overview*
• Amazon SageMaker và vòng đời ML
• Chuẩn bị & gán nhãn dữ liệu
• Huấn luyện, tuning, triển khai model
• MLOps tích hợp
• **Live Demo:** SageMaker Studio

**10:30 – 10:45 AM** | Coffee Break

**10:45 AM – 12:00 PM** | *Generative AI with Amazon Bedrock*
• So sánh Foundation Models: Claude, Llama, Titan
• Prompt engineering: chain-of-thought, few-shot
• RAG & thiết kế knowledge base
• Bedrock Agents cho workflow nhiều bước
• Guardrails kiểm soát output AI
• **Live Demo:** Xây chatbot GenAI bằng Bedrock

**12:00 PM** | Lunch Break

### Bài học Chính

#### Mẫu kỹ thuật & Best Practices

* Áp dụng kiến trúc nhiều lớp: pretrained service cho quick win, SageMaker cho ML lifecycle, Bedrock cho GenAI nâng cao
* RAG là nền tảng cho GenAI doanh nghiệp — giúp mô hình dựa vào dữ liệu thật và giảm sai lệch
* Cách viết prompt ảnh hưởng trực tiếp đến chất lượng và chi phí — prompt gọn, rõ giúp tối ưu latency
* Orchestration qua Agentcore giúp GenAI thực hiện workflow phức tạp và gọi tool an toàn

#### Vận hành & Quản trị AI

* Governance phải được tích hợp từ đầu: quyền truy cập, bảo mật, và khả năng giải thích
* Lựa chọn foundation model cần cân nhắc chi phí–độ trễ–độ chính xác
* Logging, auditing và evaluation pipelines là bắt buộc để theo dõi model drift

### Ứng dụng vào Công việc

* Bắt đầu nhỏ: dùng pretrained service và RAG đơn giản trước khi đầu tư huấn luyện mô hình lớn
* Lưu trữ dữ liệu trên S3 và xây search/index (Kendra hoặc OpenSearch) cho RAG retrieval
* Điều phối workflow qua Agentcore hoặc Lambda-based controller để đảm bảo tính ổn định
* Áp dụng CI/CD cho model artifact và prompt versioning
* Đặt ra chỉ số đo chất lượng, độ trễ và chi phí; dùng CloudWatch để theo dõi

### Trải nghiệm Sự kiện

Buổi workshop mang lại sự cân bằng giữa lý thuyết và thực hành — giúp tôi kết nối các khái niệm GenAI trừu tượng với các mẫu thiết kế có thể áp dụng ngay trong dự án thực tế.

#### Những điều tôi học được

* Hiểu rõ hơn "bản đồ hệ thống" AI/ML trên AWS và thời điểm sử dụng từng lớp dịch vụ
* Kỹ thuật prompt engineering giúp tăng chất lượng output và giảm chi phí
* RAG và knowledge base đóng vai trò then chốt trong việc tăng tính tin cậy
* Orchestration với Bedrock Agentcore mở ra hướng xây ứng dụng GenAI nhiều bước

#### Kết nối & Cộng đồng

* Gặp gỡ kỹ sư AWS và những người đang làm AI thực chiến tại văn phòng AWS Việt Nam
* Nhận được tài liệu tham khảo, repo mẫu và gợi ý workshop nâng cao

> Workshop là cầu nối quan trọng giữa lý thuyết GenAI và thực hành triển khai trên AWS — giúp tôi định hình các bước tiếp theo để xây dựng hệ thống AI có tính mở rộng, an toàn và tối ưu chi phí.
