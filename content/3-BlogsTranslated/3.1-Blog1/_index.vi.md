---
title: "Blog 1"
date: "2024-01-01"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AWS Big Data Blog

## Giới thiệu Apache Airflow 3 trên Amazon MWAA: Tính năng và khả năng mới

bởi Anurag Srivastava, Ankit Sahu, Kamen Sharlandjiev, Sriharsh Adari, Mohammad Sabeel, và Satya Chikkala vào 01 OCT 2025 trong chuyên mục Advanced (300), Amazon Managed Workflows for Apache Airflow (Amazon MWAA)

Hôm nay, Amazon Web Services (AWS) công bố khả năng sẵn sàng chung của Apache Airflow 3 trên Amazon Managed Workflows for Apache Airflow (Amazon MWAA). Bản phát hành này thay đổi cách các tổ chức sử dụng Apache Airflow để điều phối pipeline dữ liệu và quy trình nghiệp vụ trên đám mây, mang đến bảo mật nâng cao, hiệu năng cải thiện, và các khả năng điều phối workflow hiện đại cho khách hàng Amazon MWAA.

Amazon MWAA tích hợp các tính năng của Airflow 3 để hiện đại hóa quản lý workflow cho khách hàng AWS. Sau khi cộng đồng Apache phát hành Airflow 3 vào tháng 4/2025, AWS đã đưa các khả năng này vào Amazon MWAA. Airflow giờ có giao diện người dùng (UI) được thiết kế lại hoàn toàn, trực quan hơn, giúp đơn giản hóa việc điều phối workflow cho người dùng ở mọi trình độ. Với Task Execution Interface (Task API), task có thể chạy cả trong Airflow và như script Python độc lập, tăng khả năng di chuyển mã và thử nghiệm. Backfill do scheduler quản lý chuyển các thao tác từ CLI sang scheduler, cung cấp điều khiển và quan sát tập trung qua UI của Airflow. Cải tiến bảo mật cho CLI thay thế truy cập trực tiếp vào cơ sở dữ liệu bằng các gọi API, duy trì bảo mật đồng nhất giữa các giao diện. Airflow hiện hỗ trợ workflow theo sự kiện, cho phép kích hoạt từ các dịch vụ AWS và nguồn bên ngoài. Amazon MWAA cũng thêm hỗ trợ cho Python 3.12, mang đến các khả năng ngôn ngữ mới nhất cho phát triển workflow.

Bài viết này đi sâu vào các tính năng của Airflow 3 trên Amazon MWAA và nêu ra những nâng cấp giúp cải thiện khả năng điều phối workflow của bạn. Dịch vụ vẫn giữ mô hình thanh toán theo sử dụng (pay-as-you-go) của Amazon MWAA mà không cần cam kết trước. Bạn có thể bắt đầu ngay bằng cách truy cập console Amazon MWAA và khởi tạo môi trường Apache Airflow mới thông qua AWS Management Console, AWS CLI, AWS CloudFormation hoặc AWS SDK trong vài phút.

### Các tiến bộ về kiến trúc trong Airflow 3 trên Amazon MWAA

Airflow 3 trên Amazon MWAA giới thiệu các cải tiến kiến trúc đáng kể giúp nâng cao bảo mật, hiệu năng và linh hoạt. Những tiến bộ này tạo nền tảng vững chắc hơn cho việc điều phối workflow trong khi vẫn duy trì khả năng tương thích ngược với các workflow hiện có.

#### Bảo mật nâng cao

Amazon MWAA với Airflow 3 thay đổi mô hình bảo mật bằng cách biến việc tách riêng các thành phần thành thực hành tiêu chuẩn thay vì tuỳ chọn. Trong Airflow 2, DAG processor (thành phần phân tích và xử lý file DAG) chạy trong tiến trình scheduler theo mặc định, nhưng có thể tách ra thành tiến trình riêng để cải thiện khả năng mở rộng và cô lập bảo mật. Airflow 3 mặc định thực hiện tách này, duy trì thực hành bảo mật nhất quán trên các triển khai.

#### API server và Task API

Trên nền tảng bảo mật đó, Amazon MWAA với Airflow 3 giới thiệu một thành phần API server mới, đóng vai trò trung gian giữa task instance và cơ sở dữ liệu metadata của Airflow. Thay đổi này nâng cao posture bảo mật của workflow bằng cách giảm thiểu truy cập trực tiếp từ task tới metadata DB. Các task hiện hoạt động với quyền truy cập cơ sở dữ liệu ít nhất (least privilege), giảm rủi ro một task ảnh hưởng tới các task khác và cải thiện độ ổn định hệ thống nhờ giảm số kết nối trực tiếp tới database.

Giao tiếp được chuẩn hóa qua các endpoint API rõ ràng tạo nền tảng cho điều phối workflow an toàn, có thể mở rộng và linh hoạt hơn. Task Execution Interface (Task API) giúp task chạy cả trong Airflow và như các script Python độc lập, cải thiện khả năng di chuyển mã và khả năng test.

#### Từ lập lịch dựa trên dữ liệu sang lập lịch theo sự kiện

Sự tiến hoá của Airflow sang lập lịch theo sự kiện bắt đầu với việc giới thiệu lập lịch nhận biết dữ liệu (data-aware scheduling) trong Airflow 2.4, cho phép DAG được kích hoạt dựa trên sự sẵn có dữ liệu thay vì chỉ theo lịch thời gian. Amazon MWAA với Airflow 3 xây dựng trên nền tảng này bằng một chuyển đổi bao gồm đổi tên datasets thành assets và giới thiệu các khả năng nâng cao, bao gồm phân vùng asset, tích hợp sự kiện bên ngoài và thiết kế workflow tập trung vào asset.

Việc chuyển từ datasets sang assets không chỉ là đổi tên đơn thuần. Một data asset là tập hợp các dữ liệu liên quan logic, có thể đại diện cho nhiều sản phẩm dữ liệu khác nhau, bao gồm bảng cơ sở dữ liệu, mô hình ML được lưu, dashboard nhúng, hoặc thư mục chứa nhiều file.

Amazon MWAA với Airflow 3 giới thiệu cú pháp tập trung vào asset mới, biểu thị một bước chuyển quan trọng trong cách thiết kế workflow. Decorator `@asset` giúp developer đặt data asset vào trung tâm thiết kế workflow, tạo ra pipeline hướng asset trực quan hơn.

Ví dụ sau minh hoạ lập lịch DAG nhận biết asset:

```python
from airflow.sdk import DAG, Asset
from airflow.providers.standard.operators.python import PythonOperator

# Define the asset
customer_data_asset = Asset(name="customer_data", uri="s3://my-bucket/customer-data.csv")

def process_customer_data():
	"""Process customer data..."""
	# Implementation here

# Create the DAG and task
with DAG(dag_id="process_customer_data", schedule="@daily"):
	PythonOperator(
		task_id="process_data", 
		outlets=[customer_data_asset], 
		python_callable=process_customer_data
	)
```

Ví dụ sau cho thấy cách tiếp cận tập trung vào asset với decorator `@asset`:

```python
from airflow.sdk import asset

@asset(uri="s3://my-bucket/customer-data.csv", schedule="@daily")
def customer_data():
	"""Process customer data..."""
	# Implementation here
```

Decorator `@asset` tự động tạo một asset với tên hàm, một DAG có cùng identifier, và một task tạo ra asset đó. Điều này giảm độ phức tạp mã và tạo điều kiện cho việc tạo DAG tự động, nơi mỗi asset trở thành một đơn vị workflow độc lập.

#### Lập lịch theo sự kiện bên ngoài với Asset Watchers

Một tiến bộ quan trọng trong Amazon MWAA với Airflow 3 là giới thiệu Asset Watchers, giúp Airflow phản ứng với các sự kiện diễn ra bên ngoài hệ thống Airflow. Trong khi các phiên bản trước hỗ trợ phụ thuộc chéo giữa các DAG nội bộ, Asset Watchers mở rộng khả năng này đến các hệ thống dữ liệu ngoài và hàng đợi tin nhắn thông qua lớp `AssetWatcher`.

Amazon MWAA với Airflow 3 bao gồm hỗ trợ cho Amazon Simple Queue Service (Amazon SQS) qua Asset Watchers. Điều này cho phép workflow của bạn được kích hoạt bởi các tin nhắn bên ngoài và hỗ trợ lập lịch theo sự kiện. Asset Watchers giám sát hệ thống bên ngoài bất đồng bộ và kích hoạt workflow khi sự kiện cụ thể xảy ra, giúp workflow phản ứng với các sự kiện nghiệp vụ, cập nhật dữ liệu hoặc thông báo hệ thống mà không cần polling liên tục bằng sensor.

#### Giao diện người dùng hiện đại dựa trên React

Amazon MWAA với Airflow 3 tích hợp giao diện người dùng hoàn toàn được thiết kế lại, trực quan và xây dựng bằng React và FastAPI, giúp đơn giản hóa việc điều phối workflow cho người dùng ở mọi trình độ. Giao diện mới cung cấp điều hướng và hình dung workflow trực quan hơn, với chế độ lưới nâng cao giúp quan sát trạng thái và lịch sử task tốt hơn. Người dùng sẽ đánh giá cao việc bổ sung chế độ nền tối (dark mode) giảm mỏi mắt khi làm việc lâu, và hiệu năng tổng thể nhanh hơn, đặc biệt khi làm việc với DAG lớn.

Giao diện mới duy trì các luồng công việc quen thuộc trong khi cung cấp trải nghiệm quản lý DAG hiện đại và hiệu quả hơn, làm cho công việc hàng ngày của developer và operator trở nên năng suất hơn. Giao diện cũ đã được loại bỏ hoàn toàn, mang lại trải nghiệm sạch sẽ và đồng nhất hơn trên toàn hệ thống. Nền tảng cho giao diện mới được xây dựng trên REST API và một tập các API nội bộ cho các thao tác UI, cả hai hiện được dựa trên FastAPI, tạo ra kiến trúc nhất quán và an toàn hơn cho cả truy cập chương trình và hoạt động giao diện người dùng.

#### Tối ưu hoá scheduler

Scheduler trong Amazon MWAA với Airflow 3 mang đến các cải tiến hiệu năng cho việc thực thi task và quản lý workflow. Engine lập lịch được thiết kế lại xử lý task hiệu quả hơn, giảm thời gian giữa việc submit task và thực thi. Tối ưu này có lợi cho các pipeline dữ liệu cần xử lý nhanh và hoàn thành workflow đúng hạn.

Scheduler giờ phân bổ tài nguyên tính toán hiệu quả hơn, đảm bảo hiệu năng ổn định khi workload tăng. Khi chạy nhiều DAG đồng thời, hệ thống phân bổ tài nguyên mới giúp tránh tắc nghẽn và duy trì tốc độ thực thi nhất quán. Tiến bộ này đặc biệt hữu ích cho các tổ chức chạy các workflow phức tạp với yêu cầu tài nguyên khác nhau. Scheduler mới cũng quản lý hoạt động đồng thời chính xác hơn, cho phép chạy nhiều instance DAG đồng thời mà vẫn giữ ổn định hệ thống và độ dự đoán hiệu năng.

#### Nâng cấp backfill do scheduler quản lý

Scheduler-managed backfill (quá trình chạy DAG cho các ngày lịch sử) chuyển các thao tác từ CLI sang scheduler, cung cấp điều khiển và quan sát tập trung qua UI của Airflow. Amazon MWAA với Airflow 3 cung cấp các nâng cấp quan trọng cho khả năng backfill của scheduler, giúp các đội dữ liệu xử lý dữ liệu lịch sử hiệu quả hơn. Quá trình backfill được tối ưu để giảm tải lên database trong quá trình thực thi và đảm bảo backfill hoàn thành nhanh hơn, giảm tác động đến workflow gần thời gian thực.

Amazon MWAA với Airflow 3 cũng cải thiện quản lý các hoạt động backfill, với scheduler cung cấp cách cô lập tốt hơn giữa các job backfill và hỗ trợ xử lý dữ liệu lịch sử hiệu quả hơn. Operator bây giờ có các công cụ giám sát tốt hơn để theo dõi tiến độ và trạng thái của job backfill, giúp quản lý những tác vụ xử lý dữ liệu này hiệu quả hơn.

### Cải tiến hướng tới developer

Airflow 3 trên Amazon MWAA mang đến nhiều nâng cấp nhằm cải thiện trải nghiệm developer, từ định nghĩa task đơn giản hơn đến khả năng quản lý workflow tốt hơn.

#### Task SDK

Task SDK cung cấp cách trực quan hơn để định nghĩa task và DAG:

```python
# Example using the Task SDK
from airflow.sdk import dag, task
from datetime import datetime

@dag(
	start_date=datetime(2023, 1, 1),
	schedule="@daily",
	catchup=False
)
def modern_etl_workflow():
    
	@task
	def extract():
		# Extract data from source
		return {"data": [1, 2, 3, 4, 5]}
    
	@task
	def transform(input_data):
		# Transform the data
		return [x * 10 for x in input_data]
    
	@task
	def load(transformed_data):
		# Load data to destination
		print(f"Loading data: {transformed_data}")
    
	# Define the workflow
	extracted_data = extract()
	transformed_data = transform(extracted_data["data"])
	load(transformed_data)

# Instantiate the DAG
etl_dag = modern_etl_workflow()
```

Cách tiếp cận này cho phép luồng dữ liệu giữa các task trực quan hơn, hỗ trợ IDE tốt hơn với type hinting được cải thiện, và dễ dàng unit test logic của task. Kết quả là mã sạch hơn, dễ bảo trì hơn và phản ánh rõ luồng dữ liệu thực tế của pipeline. Các team áp dụng mẫu này thường thấy DAG trở nên dễ đọc và đơn giản hơn để bảo trì khi workflow phức tạp tăng lên.

#### Versioning DAG

Amazon MWAA với Airflow 3 bao gồm khả năng versioning cơ bản cho DAG, được bật mặc định. Mỗi khi DAG được chỉnh sửa và deploy, Airflow sẽ serialize và lưu định nghĩa DAG để giữ lịch sử. Việc theo dõi phiên bản tự động này giảm nhu cầu ghi chép thủ công và đảm bảo mọi thay đổi được ghi lại.

Qua UI của Airflow, team có thể truy cập và xem lịch sử các phiên bản của DAG. Hiển thị này cho thấy số phiên bản (v1, v2, v3, ...) và giúp team hiểu cách workflow tiến hoá theo thời gian.

Hệ thống versioning DAG trong Amazon MWAA giúp cải thiện tính ổn định của workflow và hỗ trợ cộng tác hiệu quả hơn cho các team dữ liệu quản lý pipeline phức tạp và thay đổi liên tục.

#### Hỗ trợ Python 3.12

Amazon MWAA bổ sung hỗ trợ cho Python 3.12, mang đến các cải tiến ngôn ngữ mới nhất cho phát triển workflow. Việc nâng cấp này cho phép truy cập các cải thiện hiệu năng và thư viện mới nhất, giữ cho pipeline dữ liệu hiện đại và hiệu quả.

### Các tính năng chưa được hỗ trợ trên Amazon MWAA

Dù chúng tôi ra mắt nhiều tính năng Airflow 3 trên Amazon MWAA trong bản phát hành này, vẫn có một số tính năng chưa được hỗ trợ tại thời điểm này:

* Thay thế Flask AppBuilder (AIP-79) – Khả năng thay thế đầy đủ

* Edge Executor và task isolations (AIP-69) – Khả năng thực thi từ xa đầy đủ

* Hỗ trợ đa ngôn ngữ (AIP-72) – Hỗ trợ ngôn ngữ khác ngoài Python

Chúng tôi dự định hỗ trợ những tính năng này trong các phiên bản tiếp theo của Airflow trên Amazon MWAA.

### Kết luận

Airflow 3 trên Amazon MWAA đem lại khả năng tự động hoá workflow nâng cao. Những cải tiến kiến trúc, mô hình bảo mật được nâng cao và các tính năng thân thiện với developer cung cấp nền tảng vững chắc để xây dựng pipeline dữ liệu đáng tin cậy và dễ bảo trì hơn. Việc giới thiệu Asset Watchers thay đổi cách workflow phản ứng với các sự kiện bên ngoài, giúp lập lịch thực sự theo sự kiện. Khả năng này, kết hợp với thiết kế workflow tập trung vào asset, khiến Airflow 3 trở thành dịch vụ điều phối mạnh mẽ và linh hoạt hơn.

Các tối ưu của scheduler cải thiện hiệu năng cho thực thi task và quản lý workflow, và các nâng cấp backfill giúp xử lý dữ liệu lịch sử hiệu quả hơn. Hệ thống versioning DAG nâng cao tính ổn định và cộng tác, và hỗ trợ Python 3.12 giữ pipeline của bạn hiện đại và hiệu quả.

Các tổ chức giờ đây có thể tận dụng những tính năng và cải tiến này trên Airflow 3 trên Amazon MWAA để nâng cao khả năng điều phối workflow của họ. Để bắt đầu, truy cập trang sản phẩm Amazon MWAA.

