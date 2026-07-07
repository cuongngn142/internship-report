---
title: 'Bản đề xuất'
date: 2026-07-07
weight: 2
chapter: false
pre: ' <b> 2. </b> '
---

---

# Trung tâm Điều hành An toàn Thông tin (SOC) trên AWS

## Nền tảng Serverless và Event-driven cho Phát hiện và Ứng phó Mối đe dọa Tự động

### 1. Tóm tắt dự án

Hệ thống Trung tâm Điều hành An toàn Thông tin (Security Operations Center - SOC) trên nền tảng AWS là một giải pháp bảo mật được thiết kế theo mô hình **Serverless** và **Event-driven**, cho phép tự động phát hiện, phân tích và phản ứng với các mối đe dọa an toàn thông tin theo thời gian thực. Kiến trúc của hệ thống được xây dựng dựa trên năm chức năng cốt lõi của **NIST Cybersecurity Framework**, bao gồm: **Identify, Protect, Detect, Respond và Recover**.

Giải pháp bảo vệ các tài nguyên triển khai trong Amazon VPC thông qua việc kết hợp nhiều dịch vụ bảo mật của AWS như AWS WAF, AWS Shield Standard, Amazon GuardDuty, IAM Access Analyzer, AWS Security Hub, Amazon EventBridge, AWS Lambda và AWS Step Functions.

Nhằm tối ưu chi phí vận hành, hệ thống áp dụng định hướng **FinOps**, ưu tiên sử dụng AWS Free Tier khi có thể, lưu trữ nhật ký bảo mật trên Amazon S3 thay vì CloudWatch Logs và sử dụng Amazon Athena để truy vấn dữ liệu trực tiếp mà không cần xây dựng quy trình ETL.

Dự án minh họa cách xây dựng một hệ thống SOC hiện đại trên nền tảng đám mây, có khả năng tự động phản hồi các sự cố bảo mật đồng thời giảm chi phí quản lý hạ tầng và vận hành.

### 2. Bài toán

#### Vấn đề

Trong nhiều hệ thống hiện nay, việc giám sát an toàn thông tin vẫn phụ thuộc nhiều vào quá trình phân tích thủ công và xử lý sự cố sau khi mối đe dọa đã xảy ra. Một số khó khăn thường gặp gồm:

- Thiếu khả năng giám sát bảo mật tập trung.
- Thời gian phát hiện mối đe dọa còn chậm.
- Quá trình phản ứng sự cố còn thủ công.
- Chi phí vận hành hệ thống giám sát bảo mật cao.
- Khó tổng hợp và phân tích các cảnh báo từ nhiều dịch vụ bảo mật khác nhau.

#### Giải pháp

Hệ thống SOC được đề xuất tích hợp các dịch vụ bảo mật của AWS thành một quy trình giám sát và phản ứng tự động.

Lưu lượng truy cập từ Internet được bảo vệ bởi Amazon CloudFront, AWS WAF và AWS Shield Standard trước khi đi vào Amazon VPC. AWS CloudTrail và Amazon VPC Flow Logs thu thập các sự kiện bảo mật và lưu trữ tập trung trên Amazon S3 với dữ liệu được mã hóa bằng AWS KMS.

Amazon GuardDuty phân tích CloudTrail Management Events và VPC Flow Logs để phát hiện các hành vi bất thường, trong khi IAM Access Analyzer phát hiện các tài nguyên hoặc quyền truy cập bị công khai ngoài mong muốn. AWS Security Hub tổng hợp toàn bộ Findings và chuyển tiếp đến Amazon EventBridge.

Dựa trên mức độ nghiêm trọng của từng sự kiện, AWS Lambda hoặc AWS Step Functions sẽ tự động thực hiện các hành động phản ứng như:

- Chặn địa chỉ IP độc hại bằng AWS WAF IP Sets.
- Cô lập EC2 bằng cách cập nhật Security Groups.
- Thu hồi IAM Access Keys bị lộ.
- Tạo báo cáo sự cố và lưu trên Amazon S3.
- Gửi cảnh báo đến SOC Analyst thông qua Amazon SNS.

SOC Analyst có thể sử dụng Amazon Athena để truy vấn trực tiếp dữ liệu log phục vụ điều tra sự cố.

#### Lợi ích và hiệu quả

- Tự động phát hiện mối đe dọa bảo mật.
- Phản ứng với sự cố gần như theo thời gian thực.
- Giảm thời gian phát hiện (MTTD) và thời gian phản hồi (MTTR).
- Giám sát bảo mật tập trung.
- Giảm chi phí vận hành nhờ kiến trúc Serverless.
- Lưu trữ log tiết kiệm chi phí bằng Amazon S3.

### 3. Kiến trúc giải pháp

Hệ thống được thiết kế theo mô hình bảo vệ nhiều lớp (Defense-in-Depth) nhằm tăng cường khả năng bảo vệ, phát hiện và phản ứng với các mối đe dọa.

#### Các tầng của kiến trúc

**1. Lớp bảo vệ biên (Edge Protection)**

Amazon CloudFront, AWS WAF và AWS Shield Standard bảo vệ hệ thống trước các cuộc tấn công DDoS, SQL Injection, Cross-site Scripting (XSS) và Brute Force.

**2. Lớp cô lập mạng (Network Isolation)**

Amazon VPC bao gồm:

- **Public Subnet**
  - Application Load Balancer
  - NAT Instance (t4g.nano)

- **Private Subnet**
  - Amazon EC2
  - Security Groups

Lưu lượng truy cập chỉ được phép đến EC2 thông qua Application Load Balancer.

**3. Thu thập dữ liệu (Data Collection)**

AWS CloudTrail Management Events và Amazon VPC Flow Logs được lưu trữ tập trung trên Amazon S3 với dữ liệu được mã hóa bằng AWS KMS.

**4. Lưu trữ dữ liệu (Storage)**

Amazon S3 lưu trữ log hệ thống và báo cáo sự cố với Lifecycle Policy tự động xóa dữ liệu sau 90 ngày. Amazon Athena cho phép truy vấn dữ liệu bằng SQL phục vụ điều tra.

**5. Phát hiện mối đe dọa (Threat Detection)**

Amazon GuardDuty, IAM Access Analyzer và AWS Security Hub được sử dụng để phát hiện, phân tích và tổng hợp các cảnh báo bảo mật.

**6. Phản ứng tự động (Automated Response)**

Amazon EventBridge kích hoạt AWS Lambda hoặc AWS Step Functions để:

- Chặn địa chỉ IP độc hại.
- Cô lập EC2.
- Thu hồi IAM Access Keys.
- Gửi cảnh báo đến SOC Analyst.

**7. Bảng điều khiển giám sát (Monitoring Dashboard)**

Amazon CloudWatch Dashboard hiển thị:

- Số lượng Findings theo mức độ nghiêm trọng.
- Số lần Lambda được kích hoạt.
- Danh sách IP đã bị chặn.
- Thống kê thông báo SNS.

![SOC Architecture](/images/2-Proposal/aws_soc_architecture.png)

### Các dịch vụ AWS sử dụng

| Dịch vụ AWS                 | Vai trò                                |
| --------------------------- | -------------------------------------- |
| Amazon CloudFront           | Bảo vệ và phân phối lưu lượng tại Edge |
| AWS WAF                     | Tường lửa ứng dụng Web                 |
| AWS Shield Standard         | Chống tấn công DDoS                    |
| Amazon VPC                  | Cô lập mạng                            |
| Application Load Balancer   | Phân phối lưu lượng                    |
| Amazon EC2                  | Máy chủ ứng dụng                       |
| AWS CloudTrail              | Ghi nhận sự kiện quản trị              |
| Amazon VPC Flow Logs        | Ghi nhật ký lưu lượng mạng             |
| Amazon S3                   | Lưu trữ tập trung dữ liệu log          |
| AWS KMS                     | Mã hóa dữ liệu                         |
| Amazon GuardDuty            | Phát hiện mối đe dọa                   |
| IAM Access Analyzer         | Phân tích quyền truy cập IAM           |
| AWS Security Hub            | Tổng hợp Findings                      |
| Amazon EventBridge          | Định tuyến sự kiện                     |
| AWS Lambda                  | Phản ứng tự động                       |
| AWS Step Functions          | Điều phối quy trình phản ứng           |
| Amazon SNS                  | Gửi cảnh báo                           |
| Amazon Athena               | Điều tra dữ liệu bảo mật               |
| Amazon CloudWatch Dashboard | Giám sát hệ thống                      |

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

- **Giai đoạn 1:** Nghiên cứu các dịch vụ bảo mật của AWS và thiết kế kiến trúc SOC.
- **Giai đoạn 2:** Triển khai hạ tầng AWS bằng Terraform.
- **Giai đoạn 3:** Cấu hình CloudTrail, VPC Flow Logs, GuardDuty, IAM Access Analyzer và AWS Security Hub.
- **Giai đoạn 4:** Xây dựng quy trình phản ứng tự động bằng EventBridge, Lambda, Step Functions và SNS.

#### Yêu cầu kỹ thuật

- AWS Security Services
- AWS Networking
- Terraform
- AWS Lambda (Python)
- IAM
- Amazon EventBridge
- AWS Step Functions
- AWS CloudTrail
- Amazon S3
- Amazon Athena
- AWS KMS
- Amazon GuardDuty
- AWS Security Hub
- Amazon CloudWatch

### 5. Tiến độ thực hiện

- **Tháng 1**
  - Nghiên cứu các dịch vụ bảo mật AWS.
  - Tìm hiểu NIST Cybersecurity Framework.
  - Thiết kế kiến trúc hệ thống.

- **Tháng 2**
  - Triển khai hạ tầng.
  - Cấu hình hệ thống ghi log.
  - Kích hoạt các dịch vụ bảo mật.

- **Tháng 3**
  - Xây dựng quy trình phản ứng tự động.
  - Kiểm thử khả năng phát hiện và phản ứng.
  - Hoàn thiện triển khai và tài liệu.

### 6. Dự toán chi phí

| Dịch vụ                     | Chi phí ước tính                     |
| --------------------------- | ------------------------------------ |
| Amazon S3                   | Thấp                                 |
| Amazon Athena               | Tính phí theo lượng dữ liệu truy vấn |
| Amazon GuardDuty            | Bản dùng thử / Khối lượng thấp       |
| AWS CloudTrail              | Miễn phí Management Events           |
| AWS Lambda                  | Free Tier                            |
| Amazon EventBridge          | Free Tier                            |
| Amazon SNS                  | Free Tier                            |
| AWS Security Hub            | Bản dùng thử / Mức sử dụng thấp      |
| AWS WAF                     | Cấu hình tối thiểu                   |
| Amazon CloudWatch Dashboard | Thấp                                 |
| NAT Instance (t4g.nano)     | Thấp                                 |

**Chi phí vận hành ước tính:** dưới **60 USD/tháng**.

### 7. Đánh giá rủi ro

#### Ma trận rủi ro

| Rủi ro                                  | Mức độ ảnh hưởng | Khả năng xảy ra |
| --------------------------------------- | ---------------- | --------------- |
| Phát hiện sai cảnh báo (False Positive) | Trung bình       | Trung bình      |
| Cấu hình sai chính sách IAM             | Cao              | Thấp            |
| Chi phí AWS vượt dự kiến                | Trung bình       | Thấp            |
| Lambda thực thi thất bại                | Trung bình       | Thấp            |
| Giới hạn tài nguyên dịch vụ             | Thấp             | Thấp            |

#### Biện pháp giảm thiểu

- Cấu hình GuardDuty Suppression Rules.
- Áp dụng nguyên tắc Least Privilege cho IAM.
- Theo dõi chi phí bằng AWS Budgets.
- Kiểm thử đầy đủ quy trình phản ứng trước khi triển khai.

#### Kế hoạch dự phòng

- Điều tra sự cố thủ công bằng Amazon Athena.
- Khôi phục Security Groups khi cần.
- Kích hoạt lại IAM Access Keys nếu cần thiết.
- Khôi phục hạ tầng bằng Terraform.

### 8. Kết quả mong đợi

#### Cải tiến kỹ thuật

- Tự động phát hiện mối đe dọa trên môi trường AWS.
- Giám sát bảo mật theo thời gian thực.
- Quản lý log tập trung.
- Tự động phản ứng với sự cố.
- Vận hành hệ thống bảo mật theo mô hình Serverless với chi phí tối ưu.

#### Giá trị lâu dài

Hệ thống SOC là mô hình tham khảo phục vụ học tập, nghiên cứu và triển khai các giải pháp an toàn thông tin trên nền tảng AWS. Dự án minh họa cách kết hợp các dịch vụ Serverless và Event-driven để xây dựng một Trung tâm Điều hành An toàn Thông tin tự động theo NIST Cybersecurity Framework, đồng thời có thể được tái sử dụng làm nền tảng cho các dự án nghiên cứu và phát triển trong tương lai.
