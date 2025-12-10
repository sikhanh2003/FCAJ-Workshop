---
title: "Blog 2"
date: "2024-01-01"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Tuỳ chỉnh chính sách lưu giữ bản ghi liên hệ trong Amazon Connect

*bởi Mo Miah và Jack Tilson vào 01 OCT 2025 trong chuyên mục Advanced (300), Amazon Connect, Technical How-to*

-----

## Giới thiệu

Các trung tâm liên hệ, đặc biệt là ở các công ty Business Process Outsourcing (BPO), vận hành nhiều dòng nghiệp vụ (LOB) với các yêu cầu pháp lý hoặc hợp đồng khác nhau về việc lưu giữ bản ghi cuộc gọi.

Không tuân thủ quy định ngành hoặc trách nhiệm hợp đồng có thể dẫn đến **phạt tiền, tranh chấp pháp lý và tổn hại uy tín**. Ngược lại, lưu giữ bản ghi vượt quá thời hạn cần thiết có thể gây ra **chi phí lưu trữ không cần thiết và lo ngại về quyền riêng tư dữ liệu**.

Tổ chức cần đáp ứng nghĩa vụ tuân thủ trong khi tối ưu hóa chi phí vận hành.

Trong bài viết này, bạn sẽ học cách áp dụng **nhiều chính sách lưu giữ** cho bản ghi liên hệ trên các LOB khác nhau trong một phiên bản Amazon Connect duy nhất.

## Tổng quan giải pháp

Amazon Connect cung cấp khả năng ghi âm liên hệ tích hợp, cho phép khách hàng ghi lại cuộc trò chuyện giữa đại diện và khách hàng một cách an toàn. Những bản ghi này được lưu trữ trong một bucket Amazon S3 được tạo riêng cho phiên bản của bạn. **Cấu hình Lifecycle của Amazon S3** có thể quản lý vòng đời của những bản ghi này, cho phép bạn định nghĩa các quy tắc hết hạn để tự động xóa các bản ghi đã quá hạn trong Amazon S3 thay bạn.

Trong giải pháp này, một **thuộc tính liên hệ tùy chỉnh** trong Contact Flow của Amazon Connect sẽ xác định thời hạn lưu trữ mong muốn cho từng liên hệ. Thuộc tính này sau đó được stream đến **Amazon Kinesis**, cùng với bản ghi Contact, và kích hoạt một **AWS Lambda function**. Lambda sử dụng **tính năng gắn tag đối tượng của Amazon S3** để gắn nhãn các đối tượng bản ghi dựa trên giá trị thuộc tính liên hệ. Do đó, các đối tượng bản ghi được thiết lập để hết hạn theo tag tương ứng, theo các quy tắc Lifecycle S3 đã cấu hình cho bucket.

Với phương pháp này, bạn có thể triển khai chính sách lưu giữ tuỳ chỉnh cho bản ghi liên hệ để tuân thủ quy định lưu giữ dữ liệu, giảm chi phí lưu trữ và tối ưu hoá sử dụng tài nguyên.



### Sơ đồ kiến trúc tổng quan

![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image001.png)

Hình 1 – Sơ đồ kiến trúc

### Các bước luồng chi tiết

1.  Liên hệ đến Amazon Connect trên một dòng nghiệp vụ (LOB) cụ thể.
2.  Một thuộc tính liên hệ `retention` được gắn vào liên hệ trong contact flow — giá trị thuộc tính (**short, long**) được gán tuỳ theo LOB.
3.  Amazon Kinesis stream bản ghi contact ra Amazon S3.
4.  Một AWS Lambda function được kích hoạt như một phần của quá trình chuyển sang Amazon S3. Function này cập nhật chính sách Lifecycle của Amazon S3 (sử dụng gắn tag đối tượng) cho đối tượng dựa trên thuộc tính `retention` (**short, long**) của bản ghi contact.
5.  Bản ghi trong Amazon S3 sẽ được thiết lập để hết hạn theo chính sách lifecycle tương ứng.

-----

Trong bài viết này, chúng ta sẽ triển khai:

  * Một template CloudFormation cung cấp:
      * Một Amazon Connect Contact Flow để demo và kiểm thử giải pháp.
      * Một Amazon Kinesis Data Stream làm kênh truyền dữ liệu Contact Trace Record (CTR) ra khỏi Amazon Connect.
      * Hai AWS Lambda function chịu trách nhiệm cấu hình Amazon S3 Lifecycle Policies và gắn tag các bản ghi mới theo thời hạn lưu trữ tương ứng.

Kiến trúc này có thể tích hợp vào một phiên bản Amazon Connect hiện có mà bạn lựa chọn, cùng với bucket S3 lưu trữ bản ghi tương ứng.

## Yêu cầu tiên quyết

Xác nhận rằng bạn có quyền phù hợp để thực hiện các tác vụ trong hướng dẫn này. Nếu gặp vấn đề về quyền truy cập, liên hệ quản trị viên AWS để cấp quyền cần thiết cho vai trò của bạn.

Tóm tắt các hành động bạn cần có quyền trong tài khoản AWS chứa phiên bản Amazon Connect của bạn:

  * **CloudFormation:** Khởi chạy và xoá stacks.
  * **Amazon Connect:** Tạo và cấu hình contact flow, truy cập instance.
  * **IAM:** Tạo và xem IAM roles.
  * **Lambda:** Tạo, chỉnh sửa, cấu hình event source và triển khai function.
  * **Kinesis:** Tạo Kinesis Data Streams.

## Hướng dẫn chi tiết

Hướng dẫn này phù hợp cả khi bạn đã có Amazon Connect instance hoặc đang bắt đầu lần đầu.

Các bước sau giả định bạn có tài khoản AWS và một Amazon Connect instance. Để tạo một instance mới, tham khảo Lab 1 trong workshop Getting Started with Amazon Connect. Nếu bạn cần tài khoản AWS, hoàn thành các bước yêu cầu trước đó.

### Khởi chạy template CloudFormation

CloudFormation template có thể viết bằng JSON hoặc YAML, và là công cụ Infrastructure as Code (IaC) trên AWS. Template cho hướng dẫn này có thể tải xuống bằng nút dưới đây.

\[[Button to download CloudFormation template](https://aws-contact-center-blog.s3.us-west-2.amazonaws.com/multiple-call-recording-retention-policies/CallRecordingRetention.yaml)]

Bạn sẽ thấy một form từ dịch vụ CloudFormation. Cung cấp **Stack name** mô tả. Các tham số này liên kết template tới instance Amazon Connect và bucket bản ghi của bạn.

![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image004-2.png)

### Bước 1: Xác định

Chúng ta sẽ thu thập và ghi lại các thông tin cần thiết cho bước tiếp theo.

**a) BasicQueueId**

1.  Đăng nhập vào Amazon Connect Console với quyền administrator hoặc người dùng có security profile phù hợp để xem queues và contact flows.
2.  Chọn **Queues** dưới phần **Routing**.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image006-1-1024x526.png)
3.  Chọn **BasicQueue** từ danh sách.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image008-1.png)
4.  Chọn **Show additional queue information**.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image010-1.png)
5.  Lấy **Queue ID** từ phần cuối cùng của ARN.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image012.png)
6.  Ghi lại giá trị này.

**b) ConnectInstanceID**

1.  Từ cùng ARN trên, bạn có thể suy ra **Connect Instance ID**. Từ màn hình trước, tập trung vào phần instance của ARN.
    *Bạn cũng có thể lấy Connect Instance ARN từ trang Overview của instance trong AWS Management Console.*
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image014.png)
2.  Ghi lại giá trị này hoặc nhập vào trường `ConnectInstanceId` khi điền tham số template CloudFormation.

**c) KinesisDataStreamName**

1.  Bạn có thể để tên mặc định **“multiple-retention-ctr”**, hoặc đổi tên theo ý thích.

**d) RecordingBucketName**

1.  Chọn instance Amazon Connect từ trang Amazon Connect trong AWS Management Console.
2.  Click vào instance alias.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image017.png)
3.  Truy cập phần **Data storage** trong điều hướng của trang instance. Tại đây bạn có thể nhận tên bucket S3 lưu bản ghi. Bạn chỉ cần tên bucket chứ không cần toàn bộ đường dẫn.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image019.png)
4.  Ghi lại hoặc nhập tên này vào trường `RecordingBucketName` trong form tham số template.

### Bước 2: Triển khai giải pháp

Sau khi thu thập các mục trên, điền form tham số CloudFormation.

1.  Hoàn thành các trường trong template trước khi tiếp tục.
  ![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image022.png)
2.  Chọn **Next** để tiếp tục.
3.  Ở trang **Configure stack options**, giữ mặc định (trừ khi bạn muốn thay đổi) và chọn **Next**.
4.  Xem lại các thông tin và tham số ở trang **Review and create**. Như trước, bạn có thể giữ mặc định, ngoại trừ phần xác nhận ở cuối trang.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image024.png)
5.  Chọn **Submit** để bắt đầu khởi tạo.
6.  Quá trình tạo stack sẽ bắt đầu. Bạn sẽ thấy trạng thái **CREATE_COMPLETE**. Bạn cũng có thể kiểm tra tab **Events** và **Resources** để xem các tài nguyên đã được khởi tạo.

### Bước 3: Bật streaming dữ liệu từ Amazon Connect

> **LƯU Ý:** Amazon Connect chỉ hỗ trợ gửi CTR data tới một Kinesis Data Stream duy nhất. Nếu bạn đã gửi CTR đến một Kinesis Data Stream khác, bạn có thể cập nhật cấu hình event trigger trong Lambda `TagS3Object` để được kích hoạt khi record stream đến stream hiện tại của bạn. Điều này giúp Lambda trở thành một consumer bổ sung cho stream hiện có, không làm gián đoạn workload đã tồn tại.

Nếu bạn chưa cấu hình CTR streaming, tiếp tục theo hướng dẫn dưới.

Instance Amazon Connect nên được cấu hình gửi Contact Trace Records (CTR) đến Kinesis Data Stream **“multiple-retention-ctr”**. Bạn có thể bật điều này trong phần **Data streaming** của cấu hình instance trong AWS Management Console.

Không cần cấu hình thêm ở Contact Flow hoặc Queue để streaming này hoạt động — đây là thiết lập cấp instance.

1.  Truy cập phần **Data streaming** trong navigation của Amazon Connect service page. Kiểm tra xem Data streaming đã được bật chưa.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image028.png)
2.  Chọn hộp để bật và chọn Kinesis data stream phù hợp.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image030.png)
3.  Chọn **Save**.

### Contact Flow (thay đổi đã thực hiện – phần này mang tính tham khảo)

Hình sau cho thấy cách gán thuộc tính liên hệ (trong ví dụ sau, người gọi nhấn 1 sẽ được gán short retention).
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image032-1024x667.png)
\\

### Đoạn mã Lambda
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image034.png)
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image036.png)
\\

Đoạn mã này trích xuất giá trị thuộc tính `retention` và tạo một tag với key **'retention'** và value lấy từ **'retentionvalue'**, áp dụng tag cho đối tượng Amazon S3 sử dụng API **'PutObjectTagging'**.

Ở giai đoạn này, giải pháp đã sẵn sàng để bạn áp dụng vào contact flows của mình bằng cách đặt thuộc tính liên hệ `retention` ở nơi cần thiết trong triển khai.

## Kiểm tra sử dụng (Usage validation)

Sau khi triển khai và hiểu các thành phần, chúng ta sẽ thử một cuộc gọi kiểm thử.

### Bước 1: Gán số điện thoại cho flow “Configure multiple retention policies”

Bước này liên kết Contact Flow triển khai bởi CloudFormation template với số điện thoại để kiểm thử.

1.  Đăng nhập Amazon Connect Console với quyền admin hoặc profile phù hợp để cấu hình phone numbers.
2.  Điều hướng tới **Phone numbers** dưới phần **Channels**.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image038.png)
3.  Chọn số muốn dùng để kiểm thử. Nếu chưa có số, dùng nút **Claim a number**.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image040.png)
4.  Chọn Contact Flow **Configure multiple retention policies**.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image042.png)
5.  Chọn **Save** để lưu thay đổi.

### Bước 2: Gọi số điện thoại

Thử nghiệm – bạn có thể nhấn 1 hoặc 2 để đặt thời hạn retention. Trong ví dụ này, nhấn 1 để chọn short retention. Liên hệ sẽ vào BasicQueue trong Amazon Connect.

1.  Gọi số từ điện thoại, chọn tuỳ chọn mong muốn.
2.  Từ Contact Control Panel (CCP) hoặc Agent Workspace, trả lời cuộc gọi trong vài giây.
3.  Ngắt kết nối cuộc gọi.

### Bước 3: Kiểm tra tag đối tượng bản ghi trên Amazon S3

Sau khi cuộc gọi kết thúc, bạn có thể kiểm tra đối tượng S3 để đảm bảo tag được gắn như mong đợi. Lưu ý có thể mất vài phút để tag hiển thị.

1.  Truy cập bucket S3 chứa bản ghi, điều hướng tới đối tượng bản ghi mới nhất.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image044.png)
2.  Chọn file bản ghi trong Amazon S3. Kéo xuống tab **Properties**, tag `retention` sẽ xuất hiện, với giá trị **"long"** hoặc **"short"** tuỳ theo lựa chọn (và thuộc tính liên hệ đã được đặt) trong cuộc gọi kiểm thử.
![](/AWS-FCJ-Workshop-2025/images/3-BlogsTranslated/image046.png)
Điều này cho thấy kiểm thử thành công. Thuộc tính liên hệ đã được đặt chính xác, CTR record được stream tới Lambda và dẫn đến bản ghi được gắn tag đúng. S3 Lifecycle Policy sẽ xóa bản ghi vào thời điểm phù hợp mà không cần can thiệp người dùng. Để biết thêm về S3 Lifecycle Policies, xem tài liệu chính thức.

> **Lưu ý:** Không cần chọn retention policy qua IVR (IVR selection). Mỗi flow có thể cấu hình trong Contact Flow designer để thiết lập thuộc tính liên hệ tương ứng một cách âm thầm, sử dụng block **Set Contact Attributes**.

## Dọn dẹp (Clean up)

Để rollback triển khai CloudFormation, có hai bước — điều này sẽ dọn dẹp các tài nguyên được tạo trong hướng dẫn.

### Bước 1: Xoá stack CloudFormation

Truy cập stack CloudFormation được triển khai và **delete the stack**. Bước này sẽ xoá IAM, Lambda và Kinesis Data Streams. Ngoại lệ có thể là Contact Flow ví dụ, xử lý ở bước tiếp theo.

### Bước 2: Lưu trữ (archive) contact flow demo trong Amazon Connect

Để giảm rủi ro gây gián đoạn cho Contact Centre, Contact Flows không thể xoá bởi CloudFormation. Để loại bỏ flow demo, đăng nhập vào instance Amazon Connect với người dùng có Security Profile phù hợp và **archive** flow đó.

Kinesis Stream sẽ tự động gỡ liên kết khỏi cấu hình Data streaming của instance Amazon Connect khi bạn xoá Kinesis Stream trong bước trước.

Không có chi phí liên quan tới lưu trữ Contact Flows, vì vậy archive sẽ không gây chi phí phụ.

Sau khi hoàn tất, tất cả tài nguyên liên quan (ngoại trừ bất kỳ bản ghi cuộc gọi nào được tạo) sẽ được dọn sạch.

## Kết luận

Việc triển khai nhiều chính sách lưu giữ bản ghi cuộc gọi trong một Amazon Connect instance mang lại lợi ích kinh doanh đáng kể. Bằng cách tận dụng Amazon Connect và các dịch vụ AWS, tổ chức có thể cân bằng **tuân thủ và hiệu quả chi phí**.

Giải pháp này tăng hiệu quả vận hành, đảm bảo quyền riêng tư dữ liệu và cung cấp tính linh hoạt để thích nghi với yêu cầu kinh doanh thay đổi. Kết quả là một giải pháp tuỳ chỉnh, tối ưu chi phí và tuân thủ quy định, vận hành trên nền tảng mở rộng.

## Tìm hiểu thêm

  * Mới với Amazon Connect? Tham khảo [Getting started with Amazon Connect User Guide](https://www.google.com/search?q=%23).
  * Muốn cập nhật tính năng Amazon Connect? Xem các webinar, how-to và demo theo yêu cầu tại [Amazon Connect Enablement YouTube channel](https://www.google.com/search?q=%23).
  * Muốn thử các Workshop Amazon Connect? Xem [Amazon Connect Workshops](https://www.google.com/search?q=%23).
  * Muốn biết các sự kiện sắp tới? Xem [Customer Experience Workshops & Events](https://www.google.com/search?q=%23) và đăng ký.
