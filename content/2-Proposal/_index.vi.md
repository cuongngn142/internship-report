---
title: 'Bản đề xuất'
date: 2024-01-01
weight: 2
chapter: false
pre: ' <b> 2. </b> '
---

# Security Operations Center (SOC) on AWS

## Nền tảng Serverless và Event-driven cho Phát hiện, Phản ứng và Giám sát An toàn thông tin tự động

### 1. Tóm tắt điều hành

Trong bối cảnh các doanh nghiệp ngày càng sử dụng điện toán đám mây để triển khai hạ tầng và ứng dụng, việc đảm bảo an toàn thông tin trở thành một yêu cầu quan trọng. Mặc dù AWS cung cấp nhiều dịch vụ bảo mật, quá trình giám sát và xử lý sự cố vẫn thường được thực hiện riêng lẻ hoặc thủ công, dẫn đến thời gian phát hiện và phản ứng kéo dài.

Dự án **Security Operations Center (SOC) on AWS** được đề xuất nhằm xây dựng một nền tảng giám sát và phản ứng sự cố theo mô hình **Serverless** kết hợp **Event-driven**, giúp tự động hóa quy trình thu thập nhật ký, phát hiện mối đe dọa, phản ứng và giám sát hệ thống.

Giải pháp sử dụng các dịch vụ AWS gồm Amazon CloudTrail, VPC Flow Logs, Amazon GuardDuty, AWS Security Hub, AWS Config, IAM Access Analyzer, Amazon EventBridge, AWS Step Functions, AWS Lambda, Amazon SNS, Amazon CloudWatch, Amazon S3, AWS KMS và Amazon Athena. Khi phát hiện một Security Finding, hệ thống sẽ tự động kích hoạt quy trình phản ứng, thực hiện các hành động như cô lập EC2, vô hiệu hóa Access Key của IAM User và gửi cảnh báo tới quản trị viên.

Kiến trúc được xây dựng theo mô hình **Defense in Depth** và bám sát năm chức năng của **NIST Cybersecurity Framework** gồm **Identify, Protect, Detect, Respond** và **Recover**. Dự án hướng tới xây dựng một mô hình SOC có khả năng tự động hóa, dễ triển khai, phù hợp cho mục đích học tập, nghiên cứu và làm nền tảng để phát triển các hệ thống bảo mật trên AWS trong tương lai.

---

### 2. Ý tưởng & Mục tiêu (Tuyên bố vấn đề)

#### 2.1 Bối cảnh & Bài toán

- **Mục đích hệ thống:**
  Security Operations Center (SOC) on AWS được phát triển nhằm xây dựng một nền tảng giám sát, phát hiện và phản ứng sự cố an toàn thông tin trên môi trường AWS theo mô hình **Serverless** kết hợp **Event-driven**. Hệ thống tự động hóa quy trình thu thập nhật ký, phát hiện mối đe dọa, điều phối phản ứng và gửi cảnh báo, giúp giảm thời gian xử lý sự cố và nâng cao hiệu quả quản lý bảo mật.

- **Đối tượng khách hàng:**
  Hệ thống hướng đến hai nhóm đối tượng chính: các **doanh nghiệp nhỏ và vừa (SME)** đang sử dụng AWS nhưng chưa có đội ngũ SOC chuyên trách, chỉ cần từ **1–2 nhân sự** để triển khai, theo dõi nhật ký và xử lý cảnh báo; cùng với **sinh viên, học viên và nhóm nghiên cứu** cần một mô hình SOC thực tế để học tập, nghiên cứu và phát triển các dự án về Cloud Security.

- **Vấn đề giải quyết:**
  Các dịch vụ bảo mật của AWS như Amazon GuardDuty, AWS Config và IAM Access Analyzer có khả năng phát hiện mối đe dọa, đánh giá tuân thủ cấu hình hoặc phát hiện các tài nguyên được chia sẻ ngoài ý muốn. AWS Security Hub tổng hợp, chuẩn hóa và ưu tiên các Security Findings từ các dịch vụ này. Tuy nhiên, các dịch vụ trên chủ yếu dừng ở việc phát hiện và tạo cảnh báo. Người quản trị vẫn phải kiểm tra và xử lý thủ công, trong khi dữ liệu nhật ký phân tán ở nhiều dịch vụ khác nhau gây khó khăn cho việc giám sát tập trung. Dự án giải quyết vấn đề này bằng cách xây dựng một nền tảng SOC tự động thu thập nhật ký, phát hiện mối đe dọa, kích hoạt quy trình phản ứng và giám sát hệ thống theo thời gian thực.

#### 2.2 Mục tiêu cụ thể

- **Output mong muốn:**
  Dự án hướng tới xây dựng một nền tảng Security Operations Center hoàn chỉnh với các thành phần chính như sau:
  - Xây dựng kiến trúc SOC theo mô hình Serverless kết hợp Event-driven.
  - Triển khai lớp bảo vệ biên bằng Amazon CloudFront, AWS WAF và AWS Shield Standard.
  - Thiết lập hạ tầng mạng VPC với Public Subnet, Private Subnet, Application Load Balancer, Security Group và VPC Flow Logs.
  - Thu thập tập trung toàn bộ nhật ký từ CloudTrail, VPC Flow Logs, GuardDuty, AWS Config và ALB Access Logs về Amazon S3.
  - Xây dựng hệ thống phát hiện mối đe dọa sử dụng GuardDuty, Security Hub, IAM Access Analyzer và AWS Config.
  - Xây dựng quy trình phản ứng tự động sử dụng EventBridge, Step Functions và Lambda Functions.
  - Thiết lập CloudWatch Dashboard phục vụ giám sát tập trung.
  - Hoàn thiện tài liệu hướng dẫn triển khai trên AWS Console và CloudFormation.

- **Tiêu chí đánh giá thành công:**
  Hệ thống được xem là hoàn thành khi đáp ứng các tiêu chí sau:
  - Tự động phát hiện các Security Findings từ Amazon GuardDuty.
  - Tự động kích hoạt quy trình phản ứng khi phát hiện sự cố.
  - Có khả năng cô lập EC2 bằng Isolation Security Group.
  - Có khả năng vô hiệu hóa Access Key và Console Login của IAM User bị nghi ngờ xâm nhập.
  - Gửi cảnh báo tới quản trị viên thông qua Amazon SNS.
  - Lưu trữ toàn bộ thông tin sự cố trên Amazon S3 phục vụ điều tra số.
  - Giám sát toàn bộ hệ thống thông qua CloudWatch Dashboard và CloudWatch Alarms.
  - Mã hóa toàn bộ dữ liệu nhật ký bằng AWS KMS.
  - Thực hiện đầy đủ quy trình xử lý sự cố Detect → Respond → Recover, trong khuôn khổ tổng thể 5 chức năng của NIST Cybersecurity Framework (Identify, Protect, Detect, Respond, Recover) mà hệ thống hướng tới.

#### 2.3 Phù hợp với chương trình

Dự án **Security Operations Center (SOC) on AWS** được xây dựng phù hợp với định hướng của chương trình **First Cloud AI Journey (FCAJ)** khi tập trung khai thác các dịch vụ Cloud và Security của AWS để giải quyết một bài toán thực tế trong lĩnh vực an toàn thông tin.

Giải pháp vận dụng các dịch vụ đã được học trong chương trình như Amazon EC2, Amazon VPC, IAM, Amazon S3, Amazon CloudTrail, Amazon CloudWatch, Amazon SNS và AWS Lambda, đồng thời mở rộng sang các dịch vụ bảo mật chuyên sâu như Amazon GuardDuty, AWS Security Hub, AWS Config, IAM Access Analyzer, Amazon EventBridge, AWS Step Functions, AWS WAF và Amazon CloudFront.

Khác với các bài thực hành riêng lẻ chỉ tập trung vào từng dịch vụ, dự án tích hợp các thành phần này thành một nền tảng Security Operations Center hoàn chỉnh, có khả năng tự động giám sát, phát hiện và phản ứng với các sự cố bảo mật trên môi trường AWS.

Kiến trúc của hệ thống tuân thủ các nguyên tắc trong **AWS Well-Architected Framework**, đặc biệt là hai trụ cột **Security** và **Operational Excellence**, thông qua việc áp dụng mô hình Defense in Depth, nguyên tắc Least Privilege, mã hóa dữ liệu bằng AWS KMS, ghi nhận nhật ký tập trung và tự động hóa quy trình phản ứng.

Đồng thời, toàn bộ hệ thống được thiết kế bám sát năm chức năng của **NIST Cybersecurity Framework**:

| Chức năng NIST | Dịch vụ AWS                                               |
| -------------- | --------------------------------------------------------- |
| Identify       | IAM Access Analyzer, AWS Config                           |
| Protect        | CloudFront, AWS WAF, AWS Shield Standard, Security Groups |
| Detect         | CloudTrail, VPC Flow Logs, GuardDuty, Security Hub        |
| Respond        | EventBridge, Step Functions, Lambda, SNS                  |
| Recover        | Amazon S3, Amazon Athena                                  |

Cần lưu ý rằng ở phạm vi dự án này, chức năng **Recover** chủ yếu được thể hiện qua việc lưu trữ tập trung dữ liệu sự cố trên Amazon S3 và hỗ trợ truy vấn/điều tra bằng Amazon Athena, phục vụ công tác điều tra số và rút kinh nghiệm vận hành. Đây chưa phải là một cơ chế khôi phục hệ thống hoàn chỉnh (ví dụ tự động khôi phục cấu hình, backup/restore tài nguyên hay chuyển đổi dự phòng) — đây là hướng mở rộng có thể bổ sung trong các giai đoạn phát triển tiếp theo. Amazon CloudWatch Dashboard, dù xuất hiện trong luồng xử lý sau sự cố, thiên về vai trò **Monitoring/Observability** — hỗ trợ quan sát trạng thái hệ thống sau sự cố — hơn là một thành phần của chức năng Recover.

Thông qua dự án này, người thực hiện không chỉ củng cố kiến thức về các dịch vụ AWS mà còn có cơ hội tiếp cận quy trình vận hành của một Security Operations Center hiện đại, từ đó nâng cao kỹ năng thiết kế kiến trúc Cloud Security và tự động hóa phản ứng sự cố trên nền tảng AWS.

---

### 3. Kiến trúc giải pháp

#### 3.1 Sơ đồ kiến trúc hệ thống

![Image](/images/4-EventParticipated/AWS_SOC_Architecture_final.drawio.png)

Hệ thống **Security Operations Center (SOC) on AWS** được thiết kế theo mô hình **Serverless** kết hợp **Event-driven**, trong đó mọi sự kiện bảo mật đều được xử lý theo cơ chế bất đồng bộ (Asynchronous Event Processing). Khi một sự kiện hoặc hành vi bất thường xảy ra trên môi trường AWS, hệ thống sẽ tự động thu thập dữ liệu, phân tích mức độ ảnh hưởng, thực hiện các hành động phản ứng phù hợp và gửi cảnh báo tới quản trị viên mà không cần can thiệp thủ công.

Kiến trúc được chia thành bảy lớp chức năng chính, mỗi lớp đảm nhận một vai trò riêng nhưng được kết nối chặt chẽ nhằm tạo thành một quy trình xử lý sự cố hoàn chỉnh.

##### Layer 1 – Edge Protection

Đây là lớp đầu tiên tiếp nhận toàn bộ lưu lượng truy cập từ Internet.

Người dùng truy cập ứng dụng thông qua **Amazon CloudFront**, giúp tăng tốc độ phân phối nội dung, giảm độ trễ truy cập và hạn chế việc truy cập trực tiếp đến máy chủ gốc (Origin).

Tại lớp này, **AWS WAF** được sử dụng để kiểm tra các yêu cầu HTTP/HTTPS, ngăn chặn các hình thức tấn công phổ biến như:

- SQL Injection (SQLi)
- Cross-site Scripting (XSS)
- Bot Traffic
- Rate-based Attack
- IP Reputation List

Song song với đó, **AWS Shield Standard** cung cấp khả năng bảo vệ tự động trước các cuộc tấn công DDoS ở tầng mạng và tầng vận chuyển.

---

##### Layer 2 – Network Infrastructure

Sau khi vượt qua lớp bảo vệ biên, lưu lượng sẽ được chuyển vào hạ tầng mạng Amazon VPC.

Kiến trúc mạng được xây dựng theo mô hình phân tách Public và Private Subnet.

Các thành phần bao gồm:

- Amazon VPC
- Internet Gateway
- NAT Gateway
- Public Route Table
- Private Route Table
- Application Load Balancer
- Security Groups

Application Load Balancer tiếp nhận lưu lượng từ CloudFront và phân phối tới các EC2 Instance nằm trong Private Subnet.

Việc triển khai EC2 trong Private Subnet giúp hạn chế khả năng truy cập trực tiếp từ Internet, giảm đáng kể bề mặt tấn công.

---

##### Layer 3 – Data Collection

Lớp này chịu trách nhiệm thu thập toàn bộ nhật ký và sự kiện diễn ra trên hệ thống.

Nguồn dữ liệu bao gồm:

- Amazon CloudTrail
- VPC Flow Logs
- ALB Access Logs
- AWS Config
- GuardDuty Findings
- CloudWatch Logs

CloudTrail ghi nhận toàn bộ API calls trong tài khoản AWS.

VPC Flow Logs ghi nhận các kết nối mạng giữa các thành phần trong VPC.

AWS Config theo dõi sự thay đổi cấu hình tài nguyên.

GuardDuty sinh các Security Findings khi phát hiện hành vi bất thường.

Nhờ việc tập trung toàn bộ dữ liệu tại một nơi, hệ thống có thể dễ dàng phục vụ công tác điều tra số (Digital Forensics) cũng như truy vết nguyên nhân sau sự cố.

---

##### Layer 4 – Storage & Analytics

Toàn bộ dữ liệu được lưu trữ tập trung trên **Amazon S3**.

Để đảm bảo an toàn dữ liệu, bucket được cấu hình:

- Block Public Access
- Versioning
- Server-side Encryption
- AWS KMS Encryption
- Lifecycle Policy

Amazon Athena được sử dụng để truy vấn trực tiếp các tập tin log trên S3 mà không cần triển khai cơ sở dữ liệu.

Điều này giúp giảm chi phí lưu trữ đồng thời hỗ trợ việc phân tích log một cách nhanh chóng.

---

##### Layer 5 – Threat Detection

Đây là lớp chịu trách nhiệm phát hiện các mối đe dọa bảo mật và tổng hợp kết quả phát hiện.

Các dịch vụ trực tiếp phát hiện mối đe dọa và đánh giá tuân thủ bao gồm:

- Amazon GuardDuty
- AWS Config
- IAM Access Analyzer

Bên cạnh đó, **AWS Security Hub** không trực tiếp phát hiện mối đe dọa mà đóng vai trò tổng hợp (aggregator): thu thập Security Findings từ GuardDuty, Config, IAM Access Analyzer và các dịch vụ bảo mật khác, chuẩn hóa theo định dạng **AWS Security Finding Format (ASFF)**, đồng thời gán mức độ ưu tiên (Severity) để hỗ trợ quản trị viên xử lý.

GuardDuty sử dụng Machine Learning cùng Threat Intelligence để phân tích CloudTrail, VPC Flow Logs và DNS Logs, qua đó phát hiện các dấu hiệu như:

- Credential Compromise
- Cryptocurrency Mining
- Port Scanning / Reconnaissance
- Suspicious API calls

Ngoài ra, nếu được cấu hình bật (enabled), GuardDuty còn hỗ trợ phát hiện Malware Activity thông qua tính năng bổ sung **GuardDuty Malware Protection** cho EC2/EBS hoặc S3; đây không phải tính năng mặc định đi kèm GuardDuty.

AWS Config liên tục đánh giá mức độ tuân thủ của tài nguyên AWS theo các quy tắc bảo mật.

IAM Access Analyzer phân tích resource policy và trust policy để phát hiện các tài nguyên bị chia sẻ ra ngoài ý muốn (ví dụ IAM Role, Amazon S3 Bucket, AWS KMS Key...).

---

##### Layer 6 – Automated Response

Đây là thành phần trung tâm của toàn bộ hệ thống SOC.

Khi Amazon GuardDuty, AWS Config hoặc IAM Access Analyzer tạo Security Findings, AWS Security Hub sẽ tổng hợp và chuẩn hóa các Findings này. Amazon EventBridge sau đó nhận sự kiện từ Security Hub và kích hoạt AWS Step Functions.

Step Functions điều phối toàn bộ quy trình phản ứng bằng cách gọi các Lambda Functions tương ứng.

Tùy theo loại Security Finding, Lambda sẽ thực hiện các hành động như:

- Cô lập EC2 bằng Isolation Security Group.
- Vô hiệu hóa (deactivate) Access Key của IAM User bị nghi ngờ lộ thông tin xác thực.
- Chặn quyền đăng nhập Console của IAM User bằng cách xóa Login Profile (DeleteLoginProfile) hoặc áp dụng IAM Policy deny.
- Gửi thông báo qua Amazon SNS.
- Ghi nhận lịch sử xử lý lên Amazon S3.
- Ghi log vận hành vào CloudWatch Logs.

Nhờ sử dụng kiến trúc Event-driven, toàn bộ quá trình phản ứng diễn ra tự động ngay sau khi phát hiện sự cố, góp phần giảm đáng kể thời gian xử lý.

---

##### Layer 7 – Monitoring & Visualization

Lớp cuối cùng cung cấp khả năng giám sát và quan sát toàn bộ hệ thống.

Amazon CloudWatch Dashboard hiển thị các thông tin như:

- Số lượng Security Findings
- Lambda Invocation
- Lambda Error Rate
- Step Functions Execution
- EC2 Health
- ALB Request Count
- CloudFront Requests
- WAF Blocked Requests
- GuardDuty Findings
- SNS Notifications

CloudWatch Alarms sẽ tự động gửi cảnh báo khi các chỉ số vượt quá ngưỡng cấu hình.

Dashboard giúp người quản trị theo dõi trạng thái bảo mật của toàn bộ hệ thống theo thời gian thực.

#### 3.2 Kiến trúc tổng thể

Kiến trúc của hệ thống được xây dựng theo mô hình phòng thủ nhiều lớp (Defense in Depth), trong đó mỗi lớp đảm nhiệm một vai trò riêng nhằm giảm thiểu rủi ro và nâng cao khả năng phát hiện cũng như phản ứng với các mối đe dọa.

Luồng hoạt động của hệ thống được mô tả như sau:

1. Người dùng gửi yêu cầu từ Internet đến Amazon CloudFront.
2. AWS WAF và AWS Shield Standard kiểm tra lưu lượng truy cập.
3. Lưu lượng hợp lệ được chuyển tới Application Load Balancer.
4. ALB phân phối yêu cầu đến EC2 trong Private Subnet.
5. CloudTrail, VPC Flow Logs và AWS Config ghi nhận toàn bộ hoạt động của hệ thống.
6. Amazon GuardDuty liên tục phân tích dữ liệu từ CloudTrail, VPC Flow Logs và DNS Logs để phát hiện các dấu hiệu bất thường. AWS Config theo dõi thay đổi cấu hình tài nguyên, trong khi IAM Access Analyzer phát hiện các tài nguyên bị chia sẻ ra ngoài ý muốn.
7. AWS Security Hub tổng hợp các Security Findings.
8. Amazon EventBridge nhận sự kiện bảo mật.
9. AWS Step Functions điều phối quy trình phản ứng.
10. AWS Lambda thực hiện các hành động khắc phục tự động.
11. Amazon SNS gửi cảnh báo tới quản trị viên.
12. Toàn bộ nhật ký và kết quả xử lý được lưu trữ trên Amazon S3.
13. Amazon Athena hỗ trợ truy vấn và điều tra dữ liệu.
14. Amazon CloudWatch Dashboard hiển thị trạng thái hoạt động của hệ thống theo thời gian thực.

#### 3.3 Các dịch vụ AWS sử dụng

| Dịch vụ                   | Vai trò                                         |
| ------------------------- | ----------------------------------------------- |
| Amazon VPC                | Xây dựng hạ tầng mạng riêng                     |
| Public & Private Subnet   | Phân tách vùng truy cập                         |
| Internet Gateway          | Kết nối Internet                                |
| NAT Gateway               | Cho phép Private Subnet truy cập Internet       |
| Application Load Balancer | Cân bằng tải                                    |
| Amazon EC2                | Chạy ứng dụng                                   |
| Amazon CloudFront         | CDN và bảo vệ biên                              |
| AWS WAF                   | Lọc các cuộc tấn công Web                       |
| AWS Shield Standard       | Chống DDoS                                      |
| Amazon CloudTrail         | Ghi nhận API calls                              |
| VPC Flow Logs             | Ghi nhận lưu lượng mạng                         |
| Amazon S3                 | Lưu trữ log tập trung                           |
| AWS KMS                   | Mã hóa dữ liệu                                  |
| Amazon Athena             | Phân tích log                                   |
| Amazon GuardDuty          | Phát hiện mối đe dọa                            |
| AWS Security Hub          | Tổng hợp Security Findings                      |
| AWS Config                | Kiểm tra tuân thủ cấu hình                      |
| IAM Access Analyzer       | Phát hiện tài nguyên bị chia sẻ ra ngoài ý muốn |
| Amazon EventBridge        | Điều phối sự kiện                               |
| AWS Step Functions        | Orchestration quy trình phản ứng                |
| AWS Lambda                | Thực hiện phản ứng tự động                      |
| Amazon SNS                | Gửi cảnh báo                                    |
| Amazon CloudWatch         | Dashboard và Monitoring                         |
|                           |

---

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

Dự án được triển khai theo các giai đoạn kỹ thuật chính sau:

### Xây dựng hạ tầng mạng và lớp bảo vệ biên

- Tạo Amazon VPC.
- Tạo Public Subnet và Private Subnet.
- Cấu hình Internet Gateway và NAT Gateway.
- Thiết lập Public Route Table và Private Route Table.
- Tạo Security Groups theo nguyên tắc **Least Privilege**.
- Triển khai Application Load Balancer.
- Cấu hình Amazon CloudFront.
- Triển khai AWS WAF và AWS Shield Standard để bảo vệ lớp biên.

### Thiết lập hệ thống thu thập và lưu trữ nhật ký

- Bật Amazon CloudTrail để ghi nhận API calls.
- Cấu hình VPC Flow Logs.
- Bật AWS Config để theo dõi thay đổi cấu hình tài nguyên.
- Bật ALB Access Logs.
- Tạo Amazon S3 Bucket lưu trữ tập trung.
- Cấu hình Block Public Access.
- Bật Versioning.
- Mã hóa dữ liệu bằng AWS KMS.
- Thiết lập Lifecycle Policy cho dữ liệu nhật ký.

### Thiết lập hệ thống phát hiện mối đe dọa

- Bật Amazon GuardDuty.
- Bật AWS Security Hub.
- Cấu hình AWS Config Rules.
- Tạo IAM Access Analyzer.
- Kiểm tra việc tổng hợp Security Findings trên AWS Security Hub.
- Sử dụng Sample Findings của GuardDuty và Security Hub phục vụ kiểm thử.

### Thiết lập quy trình phản ứng tự động

- Tạo Amazon EventBridge Rule nhận Security Findings từ AWS Security Hub.
- Xây dựng AWS Step Functions để điều phối quy trình phản ứng.
- Phát triển các AWS Lambda Functions xử lý từng loại Security Finding.
- Cấp IAM Role và IAM Policy cần thiết cho Lambda.
- Cấu hình Lambda cô lập EC2 bằng Isolation Security Group.
- Cấu hình Lambda vô hiệu hóa IAM Access Key.
- Cấu hình Lambda chặn quyền đăng nhập Console của IAM User bằng cách xóa Login Profile hoặc áp dụng IAM Policy deny.
- Gửi cảnh báo thông qua Amazon SNS.
- Ghi nhận lịch sử xử lý lên Amazon S3.
- Theo dõi log thực thi trên Amazon CloudWatch Logs.

### Thiết lập hệ thống giám sát và trực quan hóa

- Xây dựng Amazon CloudWatch Dashboard.
- Hiển thị GuardDuty Findings.
- Hiển thị Security Hub Findings.
- Theo dõi Lambda Invocations và Errors.
- Theo dõi Step Functions Executions.
- Theo dõi EC2 Health.
- Theo dõi CloudFront Requests.
- Theo dõi ALB Request Count.
- Theo dõi WAF Blocked Requests.
- Cấu hình CloudWatch Alarms.
- Kiểm tra Email Notification thông qua Amazon SNS.

### Kiểm thử hệ thống

- Mô phỏng Port Scan trên EC2.
- Mô phỏng Credential Compromise.
- Mô phỏng Security Group mở SSH ra Internet.
- Mô phỏng S3 Bucket Public.
- Kiểm tra GuardDuty tạo Security Findings.
- Kiểm tra Security Hub tổng hợp Security Findings.
- Kiểm tra EventBridge kích hoạt AWS Step Functions.
- Kiểm tra AWS Lambda thực hiện phản ứng tự động.
- Kiểm tra Email Notification.
- Kiểm tra CloudWatch Dashboard và CloudWatch Alarms.

### Hoàn thiện và tối ưu hệ thống

- Kiểm tra toàn bộ quy trình **Detect → Respond → Recover**.
- Tối ưu IAM Policies theo nguyên tắc **Least Privilege**.
- Đánh giá chi phí bằng AWS Pricing Calculator.
- Hoàn thiện tài liệu triển khai.
- Chuẩn bị các hướng mở rộng như Multi-AZ, Multi-Account và Infrastructure as Code.

#### Yêu cầu chuẩn bị (Prerequisites)

- **Tài nguyên & Công cụ:** AWS Account có quyền sử dụng Amazon EC2, Amazon VPC, IAM, Amazon CloudTrail, Amazon GuardDuty, AWS Security Hub, AWS Config, IAM Access Analyzer, Amazon EventBridge, AWS Step Functions, AWS Lambda, Amazon SNS, Amazon CloudWatch, Amazon S3, AWS KMS, Amazon Athena, AWS WAF và Amazon CloudFront.
- Trình duyệt web để truy cập AWS Management Console.
- Máy tính có kết nối Internet ổn định.
- Email dùng để nhận thông báo từ Amazon SNS.
- **Kiến thức cơ bản:**
- Amazon VPC, Subnet, Route Table, Internet Gateway và NAT Gateway.
- Security Groups và nguyên tắc **Least Privilege**.
- Amazon EC2 và IAM Role.
- Amazon CloudTrail và VPC Flow Logs.
- AWS Config và IAM Access Analyzer.
- Amazon GuardDuty và AWS Security Hub.
- Amazon EventBridge.
- AWS Step Functions.
- AWS Lambda.
- Amazon SNS.
- Amazon CloudWatch Dashboard và CloudWatch Alarms.
- Amazon S3, AWS KMS và Amazon Athena.
- Kiến thức cơ bản về Cloud Security, Incident Response và **NIST Cybersecurity Framework**.

---

### 5. Lộ trình & Mốc triển khai

- **Tuần 1: Thiết lập hệ thống giám sát và phát hiện mối đe dọa**
- Tạo AWS Account và cấu hình bảo mật cơ bản (bật MFA cho Root User, tạo IAM User có quyền quản trị).
- Bật Amazon CloudTrail để ghi nhận toàn bộ API Calls.
- Cấu hình VPC Flow Logs thu thập lưu lượng mạng.
- Bật AWS Config để theo dõi thay đổi cấu hình tài nguyên.
- Tạo AWS Budgets và cảnh báo chi phí.
- Kích hoạt Amazon GuardDuty.
- Bật AWS Security Hub và tích hợp GuardDuty Findings.
- Tạo IAM Access Analyzer để phát hiện tài nguyên được chia sẻ ngoài ý muốn.
- Cấu hình CloudWatch Alarms giám sát các sự kiện quan trọng.
- Sinh GuardDuty Sample Findings và kiểm tra việc tổng hợp Security Findings trên AWS Security Hub.
- **Tuần 2: Xây dựng quy trình phản ứng sự cố tự động**
- Tạo Amazon SNS Topic và Email Subscription để gửi cảnh báo.
- Phát triển AWS Lambda Functions xử lý Security Findings.
- Xây dựng Lambda tự động cô lập EC2 bằng Isolation Security Group.
- Xây dựng Lambda tự động vô hiệu hóa IAM Access Key bị nghi ngờ xâm nhập.
- Tạo Amazon EventBridge Rule nhận Security Findings từ AWS Security Hub.
- Thiết kế workflow phản ứng bằng AWS Step Functions.
- Tích hợp EventBridge, Step Functions và Lambda thành quy trình phản ứng tự động.
- Kiểm thử quy trình GuardDuty → Security Hub → EventBridge → Step Functions → Lambda → SNS.
- Ghi log thực thi trên Amazon CloudWatch Logs.
- **Tuần 3: Hoàn thiện quy trình phản ứng và lưu trữ dữ liệu**
- Hoàn thiện các Lambda Functions xử lý từng loại Security Findings.
- Cấu hình IAM Role và IAM Policy theo nguyên tắc Least Privilege.
- Triển khai chức năng chặn quyền đăng nhập Console của IAM User khi phát hiện Credential Compromise.
- Lưu lịch sử xử lý sự cố và kết quả phản ứng lên Amazon S3.
- Mã hóa dữ liệu lưu trữ bằng AWS KMS.
- Kiểm thử các kịch bản:
  - Port Scan trên EC2.
  - Credential Compromise.
  - Security Group mở SSH ra Internet.
  - S3 Bucket Public.
- Đánh giá khả năng phát hiện và thời gian phản ứng của hệ thống.
  - **Tuần 4: Giám sát, kiểm thử và hoàn thiện hệ thống**
- Xây dựng Amazon CloudWatch Dashboard phục vụ giám sát tập trung.
- Hiển thị GuardDuty Findings, Security Hub Findings và AWS Config Compliance.
- Theo dõi Lambda Invocations, Lambda Errors và Step Functions Executions.
- Theo dõi EC2 Health, CloudFront Requests, ALB Request Count và WAF Blocked Requests.
- Cấu hình CloudWatch Alarms và kiểm tra Email Notification thông qua Amazon SNS.
- Kiểm thử toàn bộ quy trình Detect → Respond → Recover.
- Đánh giá chi phí triển khai bằng AWS Pricing Calculator.
- Hoàn thiện tài liệu triển khai và tài liệu hướng dẫn sử dụng.
- Đánh giá kết quả đạt được và đề xuất các hướng mở rộng như Multi-AZ, Multi-Account, Infrastructure as Code (Terraform/CloudFormation), Amazon Macie, Amazon Detective và tích hợp SIEM.

---

### 6. Ước tính ngân sách

Bảng tính chi phí chi tiết của hệ thống dựa trên công cụ ước tính [AWS Pricing Calculator.](https://calculator.aws/#/estimate?id=e3157d6bc8f89ac9ba160192d26e64ca7d3c0cde)

#### 6.1. Môi trường Workshop / Hướng dẫn

Môi trường Workshop được xây dựng để phục vụ mục đích học tập, nghiên cứu và trình diễn khả năng phát hiện, phân tích và phản ứng sự cố của hệ thống SOC.

Cấu hình sử dụng một số dịch vụ AWS tương tự môi trường thực tế như ALB, NAT Gateway, WAF, GuardDuty, AWS Config và Security Hub, nhưng với quy mô tài nguyên và lưu lượng thấp.

| STT                             | Dịch vụ AWS               | Cấu hình & Tham số tính toán                         |     Chi phí/tháng |
| ------------------------------- | ------------------------- | ---------------------------------------------------- | ----------------: |
| 1                               | Amazon EC2                | 01 instance t3.micro Linux, On-Demand, 730 giờ/tháng |             $9.64 |
| 2                               | Application Load Balancer | 01 ALB, lưu lượng thấp                               |            $18.63 |
| 3                               | NAT Gateway               | 01 NAT Gateway hoạt động liên tục                    |            $43.66 |
| 4                               | Amazon S3                 | 20 GB Standard Storage, PUT/GET requests             |             $0.79 |
| 5                               | Amazon CloudFront         | 10 GB Data Transfer Out, 500.000 HTTPS requests      |             $1.35 |
| 6                               | Amazon API Gateway        | HTTP/REST API requests quy mô nhỏ                    |             $1.25 |
| 7                               | Amazon CloudWatch         | 5 GB Logs, 20 Metrics, 1 Dashboard, 10 Alarms        |            $15.80 |
| 8                               | Amazon EBS                | 30 GB gp3 SSD, Snapshot                              |             $8.87 |
| 9                               | AWS KMS                   | 01 Customer Managed Key, 10.000 requests             |             $1.03 |
| 10                              | Amazon CloudTrail         | Management Events, 01 Trail                          |             $0.00 |
| 11                              | Amazon GuardDuty          | CloudTrail Events, VPC Flow Logs, DNS Logs           |            $11.96 |
| 12                              | AWS Config                | 5000 Configuration Items, 10 Rules                   |            $15.01 |
| 13                              | AWS Security Hub          | Security Checks và Findings                          |             $0.00 |
| 14                              | Amazon Athena             | Query log trên S3                                    |             $0.00 |
| 15                              | AWS Lambda                | 50.000 requests/tháng                                |             $0.00 |
| 16                              | Amazon EventBridge        | 100.000 events/tháng                                 |             $0.00 |
| 17                              | Amazon SNS                | Email notification                                   |             $0.00 |
| 18                              | AWS WAF                   | 01 Web ACL, 10 Rules                                 |            $15.60 |
| 19                              | AWS Step Functions        | Standard Workflow, 20.000 state transitions/tháng    |             $0.40 |
| **Ước tính chi phí hàng tháng** |                           |                                                      | **$144.00/tháng** |

_Lưu ý:_ Chi phí trên giả định toàn bộ hệ thống chạy liên tục. Trong môi trường học tập có thể giảm đáng kể bằng cách:

- Dừng EC2 khi không sử dụng.
- Xóa NAT Gateway sau khi hoàn thành demo vì đây là thành phần có chi phí cố định cao.
- Giảm thời gian lưu trữ CloudWatch Logs và S3 Logs.
- Giảm số lượng AWS Config Rules.
- Sử dụng AWS Free Tier, AWS Credits hoặc chương trình hỗ trợ học tập.

#### 6.2. Môi trường Thực tế

Khi triển khai trong môi trường Production, hệ thống SOC cần mở rộng tài nguyên nhằm đáp ứng yêu cầu về hiệu năng, tính sẵn sàng cao, khả năng lưu trữ log dài hạn và giám sát liên tục.

Dựa trên chi phí môi trường Workshop/Demo hiện tại (~245.83 USD/tháng), môi trường Production cần bổ sung thêm tài nguyên như nhiều EC2 instance hơn, triển khai Multi-AZ, tăng dung lượng lưu trữ log, tăng số lượng Security Findings và mở rộng khả năng phân tích dữ liệu.

Chi phí Production dưới đây chỉ mang tính ước lượng tham khảo:

| STT                             | Thành phần                | Cấu hình & Tham số tính toán                    | Chi phí/Tháng |
| ------------------------------- | ------------------------- | ----------------------------------------------- | ------------: |
| 1                               | Amazon EC2                | 02-04 EC2 instance (t3.medium hoặc tương đương) | ~ $120 - $250 |
| 2                               | Amazon EBS                | 100-200 GB gp3 SSD                              |   ~ $10 - $20 |
| 3                               | Application Load Balancer | 01 Production ALB, lưu lượng cao hơn            |   ~ $25 - $50 |
| 4                               | NAT Gateway               | Multi-AZ NAT Gateway                            |  ~ $70 - $100 |
| 5                               | Amazon S3                 | 200 GB - 1 TB log storage                       |   ~ $10 - $30 |
| 6                               | AWS KMS                   | Customer Managed Keys và encryption requests    |     ~ $2 - $5 |
| 7                               | Amazon CloudTrail         | Audit logging liên tục                          |    ~ $5 - $20 |
| 8                               | VPC Flow Logs             | Lưu lượng mạng Production                       |   ~ $10 - $50 |
| 9                               | Amazon GuardDuty          | Threat Detection liên tục                       |  ~ $20 - $100 |
| 10                              | AWS Config                | Nhiều Configuration Items và Rules              |  ~ $20 - $100 |
| 11                              | IAM Access Analyzer       | Account Analyzer                                |         $0.00 |
| 12                              | AWS Security Hub          | Security Checks và Findings                     |   ~ $10 - $50 |
| 13                              | Amazon Athena             | Truy vấn log thường xuyên                       |  ~ $20 - $100 |
| 14                              | AWS Lambda                | Automated Response Functions                    |    ~ $5 - $20 |
| 15                              | Amazon EventBridge        | Event Processing                                |    ~ $5 - $20 |
| 16                              | AWS Step Functions        | Incident Response Workflow                      |    ~ $5 - $30 |
| 17                              | Amazon SNS                | Notification Service                            |    ~ $1 - $10 |
| 18                              | Amazon CloudWatch         | Logs, Metrics, Dashboard, Alarm                 |  ~ $30 - $100 |
| 19                              | AWS WAF                   | Web ACL, Managed Rules, Request Processing      |  ~ $20 - $100 |
| 20                              | AWS Shield Standard       | DDoS Protection cơ bản                          |         $0.00 |
| 21                              | Amazon CloudFront         | CDN và lưu lượng Internet                       |   ~ $10 - $50 |
| **Ước tính chi phí hàng tháng** |                           | **~ $200 - $800+/tháng**                        |

_Lưu ý:_ Chi phí Production không thể xác định chính xác chỉ dựa trên số lượng dịch vụ. Giá thực tế phụ thuộc vào:

- Số lượng ứng dụng và tài nguyên cần bảo vệ.
- Lưu lượng truy cập Internet.
- Số lượng log phát sinh mỗi ngày.
- Thời gian lưu trữ log phục vụ điều tra sự cố.
- Số lượng Security Findings từ GuardDuty và Security Hub.
- Tần suất thực thi Lambda, Step Functions và EventBridge.
- Yêu cầu High Availability (Multi-AZ) và Disaster Recovery.

---

### 7. Đánh giá rủi ro

#### Ma trận rủi ro

Trong quá trình triển khai hệ thống Security Operations Center (SOC) trên AWS, một số rủi ro có thể ảnh hưởng đến khả năng giám sát, phát hiện và phản ứng sự cố. Các rủi ro được đánh giá dựa trên hai yếu tố chính gồm khả năng xảy ra và mức độ ảnh hưởng đến hệ thống.

| Rủi ro xác định                                                                               | Khả năng xảy ra | Mức độ ảnh hưởng | Chiến lược giảm thiểu & Phòng ngừa                                                                                                                                    |
| --------------------------------------------------------------------------------------------- | --------------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IAM Role hoặc IAM Policy cấp quyền quá rộng cho Lambda và các dịch vụ tự động                 | Trung bình      | Cao              | Áp dụng nguyên tắc Least Privilege. Chỉ cấp các quyền cần thiết cho từng Lambda Function, sử dụng IAM Access Analyzer để kiểm tra quyền truy cập ngoài ý muốn.        |
| EC2 bị truy cập trái phép hoặc bị khai thác lỗ hổng bảo mật                                   | Trung bình      | Cao              | Đặt EC2 trong Private Subnet, không mở SSH trực tiếp từ Internet, sử dụng Security Group giới hạn truy cập, cập nhật bản vá thường xuyên và giám sát bằng GuardDuty.  |
| Security Finding không được phát hiện do cấu hình sai GuardDuty, Security Hub hoặc CloudTrail | Thấp            | Cao              | Kiểm tra trạng thái Enabled của các dịch vụ bảo mật, sử dụng GuardDuty Sample Findings và Security Hub Sample Findings để kiểm thử định kỳ.                           |
| Lambda phản ứng sai gây ảnh hưởng đến tài nguyên hợp lệ                                       | Trung bình      | Cao              | Kiểm thử workflow trước khi triển khai chính thức, sử dụng Step Functions để kiểm soát luồng xử lý, ghi log đầy đủ trên CloudWatch và xây dựng cơ chế rollback.       |
| EventBridge không kích hoạt quy trình phản ứng khi có Security Finding                        | Thấp            | Cao              | Kiểm tra Event Pattern, IAM Permission giữa các dịch vụ, theo dõi trạng thái thực thi của Step Functions và tạo CloudWatch Alarm cho lỗi EventBridge/Lambda.          |
| Mất hoặc thay đổi dữ liệu log phục vụ điều tra sự cố                                          | Thấp            | Cao              | Lưu trữ log tập trung trên Amazon S3, bật Versioning, Server-side Encryption bằng AWS KMS, Block Public Access và áp dụng Lifecycle Policy.                           |
| Chi phí AWS phát sinh vượt dự kiến                                                            | Trung bình      | Trung bình       | Thiết lập AWS Budget và Cost Alert, theo dõi Cost Explorer, giới hạn tài nguyên thử nghiệm, xóa các dịch vụ có chi phí cố định cao như NAT Gateway khi không sử dụng. |
| NAT Gateway, ALB hoặc CloudWatch Logs tạo chi phí lớn trong môi trường demo                   | Cao             | Trung bình       | Chỉ duy trì tài nguyên khi cần trình diễn, giảm dung lượng log, sử dụng Lifecycle Policy cho S3 và kiểm tra AWS Pricing Calculator trước khi triển khai.              |
| Security Hub hoặc GuardDuty tạo quá nhiều Finding gây khó khăn trong xử lý                    | Trung bình      | Trung bình       | Cấu hình mức độ ưu tiên Finding, lọc theo Severity, sử dụng EventBridge Rule để chỉ xử lý các sự kiện quan trọng.                                                     |
| Sai cấu hình AWS Config Rules dẫn đến đánh giá Compliance không chính xác                     | Trung bình      | Trung bình       | Kiểm tra lại Config Rules trước khi áp dụng, sử dụng các AWS Managed Rules phù hợp và theo dõi trạng thái Compliance.                                                 |
| Tài khoản AWS bị mất quyền kiểm soát hoặc lộ thông tin xác thực                               | Thấp            | Rất cao          | Bật MFA cho Root Account, không sử dụng Root User thường xuyên, sử dụng IAM User/Role riêng biệt và theo dõi hoạt động thông qua CloudTrail.                          |
| Hệ thống phản ứng tự động không hoạt động trong lúc xảy ra sự cố                              | Thấp            | Cao              | Xây dựng phương án xử lý thủ công, duy trì quyền quản trị AWS Console, kiểm tra định kỳ toàn bộ luồng Detect → Respond.                                               |

#### Kế hoạch dự phòng (Contingency Plan)

- **Trường hợp phát hiện Security Finding nhưng hệ thống phản ứng tự động thất bại:** Khi GuardDuty hoặc Security Hub phát hiện sự cố nhưng EventBridge, Step Functions hoặc Lambda không thực hiện được hành động phản ứng, quản trị viên sẽ kiểm tra:

- AWS CloudWatch Logs của Lambda Function.
- Trạng thái thực thi của AWS Step Functions.
- EventBridge Rule và Permission giữa các dịch vụ.

Trong trường hợp cần thiết, quản trị viên có thể thực hiện phản ứng thủ công như:

- Cô lập EC2 bằng cách thay đổi Security Group.
- Vô hiệu hóa IAM Access Key bị nghi ngờ.
- Điều chỉnh IAM Policy để giới hạn quyền truy cập.

- **Trường hợp EC2 bị xâm nhập hoặc có hành vi bất thường:** Khi GuardDuty phát hiện dấu hiệu như Port Scanning, Credential Compromise hoặc hoạt động đáng ngờ:

Quy trình xử lý:

1. GuardDuty tạo Security Finding.
2. Security Hub tổng hợp và chuẩn hóa Finding.
3. EventBridge kích hoạt workflow phản ứng.
4. Lambda thực hiện cô lập EC2 bằng Isolation Security Group.
5. SNS gửi cảnh báo đến quản trị viên.
6. Log sự kiện được lưu trữ trên Amazon S3 phục vụ điều tra.

Nếu phản ứng tự động không thành công, quản trị viên thực hiện cách ly thủ công thông qua AWS Console.

- **Trường hợp dữ liệu log bị mất hoặc không thể truy vấn:** Nếu Amazon S3, CloudTrail hoặc Athena gặp lỗi:

- Kiểm tra trạng thái ghi log của CloudTrail, VPC Flow Logs và AWS Config.
- Kiểm tra quyền truy cập IAM tới S3 Bucket.
- Khôi phục dữ liệu từ S3 Versioning nếu dữ liệu bị thay đổi ngoài ý muốn.
- Sử dụng CloudWatch Logs làm nguồn dữ liệu kiểm tra tạm thời.

- **Trường hợp Lambda xử lý sai Security Finding:** Trong trường hợp Lambda thực hiện hành động nhầm đối với tài nguyên hợp lệ:

- Dừng hoặc vô hiệu hóa EventBridge Rule gây kích hoạt workflow.
- Kiểm tra CloudWatch Logs để xác định nguyên nhân.
- Khôi phục Security Group hoặc IAM Policy về trạng thái trước đó.
- Điều chỉnh lại logic xử lý trước khi bật lại tính năng tự động.

- **Trường hợp chi phí AWS vượt dự kiến:** Do môi trường Workshop sử dụng nhiều dịch vụ có chi phí cố định như Application Load Balancer, NAT Gateway, AWS Config và WAF, chi phí có thể phát sinh cao hơn khi để hệ thống chạy liên tục.

Biện pháp xử lý:

- Kiểm tra AWS Cost Explorer để xác định dịch vụ phát sinh chi phí.
- Dừng EC2 khi không sử dụng.
- Xóa NAT Gateway, ALB hoặc WAF khi kết thúc demo.
- Giảm thời gian lưu trữ CloudWatch Logs và S3 Logs.
- Thiết lập AWS Budget Alert để cảnh báo trước khi vượt ngân sách.

- **Trường hợp cần phục hồi toàn bộ hệ thống:** Đối với môi trường Production, có thể triển khai các phương án mở rộng:

- Sử dụng Infrastructure as Code bằng Terraform hoặc CloudFormation để tái tạo môi trường.
- Sao lưu cấu hình IAM, Security Group và tài nguyên quan trọng.
- Triển khai Multi-AZ nhằm tăng khả năng sẵn sàng.
- Sử dụng S3 Versioning và Backup Strategy để bảo vệ dữ liệu log.

Hệ thống được thiết kế theo hướng ưu tiên khả năng phát hiện sớm, phản ứng tự động và có phương án xử lý thủ công khi các thành phần tự động gặp lỗi, đảm bảo quy trình vận hành SOC vẫn duy trì được khả năng giám sát và xử lý sự cố.

---

### 8. Các Luồng Xử Lý Hệ Thống & Đặc Điểm Kỹ Thuật

Hệ thống Security Operations Center (SOC) on AWS được xây dựng theo kiến trúc **Serverless kết hợp Event-driven**, trong đó các sự kiện bảo mật được thu thập, phân tích, xử lý và phản ứng tự động thông qua chuỗi dịch vụ AWS.

Các luồng xử lý chính bao gồm: luồng truy cập ứng dụng, luồng thu thập dữ liệu bảo mật, luồng phát hiện mối đe dọa, luồng phản ứng tự động, luồng cảnh báo quản trị và luồng lưu trữ phục vụ điều tra.

#### 8.1 Các Luồng Xử Lý Cốt Lõi (Core Processing Flows)

- **Luồng người dùng truy cập ứng dụng:**
  Người dùng truy cập hệ thống thông qua **Amazon CloudFront**.

Toàn bộ lưu lượng HTTP/HTTPS trước tiên được kiểm tra bởi **AWS WAF** nhằm phát hiện và ngăn chặn các hành vi tấn công phổ biến như SQL Injection, Cross-site Scripting (XSS), Bot Traffic hoặc các request có dấu hiệu bất thường.

Bên cạnh đó, **AWS Shield Standard** cung cấp khả năng bảo vệ tự động trước các cuộc tấn công DDoS ở tầng mạng và tầng vận chuyển.

Sau khi vượt qua lớp bảo vệ biên, lưu lượng hợp lệ được chuyển đến **Application Load Balancer**, sau đó phân phối tới các EC2 Instance trong Private Subnet.

Việc đặt EC2 trong Private Subnet giúp hạn chế khả năng truy cập trực tiếp từ Internet và giảm bề mặt tấn công.

- **Luồng quản trị an toàn:**
  Quản trị viên không truy cập trực tiếp vào tài nguyên thông qua các cổng public không cần thiết.

Việc quản trị được thực hiện thông qua các cơ chế bảo mật của AWS như:

- IAM Role với quyền hạn tối thiểu (Least Privilege).
- MFA cho tài khoản quản trị.
- Security Group giới hạn quyền truy cập.
- AWS Systems Manager Session Manager (nếu cần quản trị EC2).

Cách tiếp cận này giúp giảm nguy cơ brute-force, lộ thông tin xác thực và hạn chế việc sử dụng các thông tin đăng nhập dài hạn.

- **Luồng thu thập dữ liệu bảo mật:**
  Hệ thống thu thập dữ liệu từ nhiều nguồn khác nhau trong môi trường AWS:

- **Amazon CloudTrail**: ghi nhận toàn bộ API Calls và hoạt động quản trị tài nguyên.
- **VPC Flow Logs**: ghi nhận lưu lượng mạng giữa các thành phần trong VPC.
- **AWS Config**: theo dõi thay đổi cấu hình tài nguyên và đánh giá Compliance.
- **ALB Access Logs**: ghi nhận các request truy cập ứng dụng.
- **CloudWatch Logs**: lưu trữ log vận hành của các dịch vụ.

Toàn bộ dữ liệu log được lưu trữ tập trung trên **Amazon S3**, được mã hóa bằng **AWS KMS** nhằm đảm bảo tính bảo mật và phục vụ điều tra sau sự cố.

- **Luồng phát hiện mối đe dọa:**
  **Amazon GuardDuty** liên tục phân tích dữ liệu từ CloudTrail, VPC Flow Logs và DNS Logs để phát hiện các hành vi bất thường.

Các loại phát hiện bao gồm:

- Port Scanning.
- Credential Compromise.
- Suspicious API Calls.
- Unusual Network Activity.
- Malware Activity (khi bật tính năng mở rộng phù hợp).

Bên cạnh đó:

- **AWS Config** phát hiện các cấu hình không tuân thủ chính sách bảo mật.
- **IAM Access Analyzer** phát hiện các tài nguyên bị chia sẻ ngoài ý muốn.

Sau khi phát hiện, các Security Findings được gửi đến **AWS Security Hub** để tổng hợp, chuẩn hóa và đánh giá mức độ nghiêm trọng.

- **Luồng tự động phản ứng sự cố:**
  Khi AWS Security Hub tạo Security Finding, quy trình phản ứng tự động được kích hoạt theo luồng:

**Security Hub → EventBridge → Step Functions → Lambda → SNS**

Cụ thể:

1. **Amazon EventBridge** nhận Security Finding từ Security Hub.
2. EventBridge Rule kiểm tra loại sự kiện và mức độ nghiêm trọng.
3. **AWS Step Functions** điều phối workflow xử lý.
4. **AWS Lambda** thực hiện hành động phản ứng tương ứng.

Các hành động phản ứng có thể bao gồm:

- Cô lập EC2 bằng Isolation Security Group.
- Vô hiệu hóa IAM Access Key bị nghi ngờ bị lộ.
- Áp dụng IAM Policy Deny để hạn chế quyền truy cập.
- Ghi nhận lịch sử xử lý sự cố.
- Gửi cảnh báo đến quản trị viên.

Kết quả thực thi được ghi nhận trên **Amazon CloudWatch Logs** để phục vụ kiểm tra và phân tích.

- **Luồng cảnh báo quản trị:**
  Sau khi quá trình phản ứng hoàn tất, **Amazon SNS** gửi thông báo đến quản trị viên.

Nội dung cảnh báo bao gồm:

- Loại Security Finding.
- Mức độ nghiêm trọng.
- Thời gian phát hiện.
- Tài nguyên bị ảnh hưởng.
- Hành động phản ứng đã thực hiện.

Điều này giúp quản trị viên nhanh chóng nắm bắt tình trạng hệ thống và thực hiện xử lý bổ sung nếu cần.

- **Luồng lưu trữ và điều tra sự cố:**
  Toàn bộ dữ liệu liên quan đến sự cố được lưu trữ trên Amazon S3.

Quản trị viên có thể sử dụng **Amazon Athena** để truy vấn trực tiếp dữ liệu log trên S3 phục vụ:

- Điều tra nguồn gốc sự cố.
- Phân tích hành vi tấn công.
- Truy vết hoạt động của tài khoản hoặc tài nguyên AWS.

Cơ chế này giúp hệ thống hỗ trợ hoạt động Digital Forensics sau sự cố.

#### 8.2 Đặc Điểm Kiến Trúc (Architectural Strengths)

- **Bảo mật theo chiều sâu (Defense in Depth):**
  Hệ thống không phụ thuộc vào một cơ chế bảo vệ duy nhất mà kết hợp nhiều lớp bảo mật:

- CloudFront.
- AWS WAF.
- AWS Shield Standard.
- VPC Security Group.
- IAM.
- CloudTrail.
- GuardDuty.
- Security Hub.
- Lambda Response.

Mỗi lớp đảm nhận một vai trò riêng, giúp giảm khả năng bị khai thác khi một lớp bảo vệ gặp sự cố.

- **Thu thập và giám sát tập trung:**
  Thay vì quản lý log phân tán trên nhiều dịch vụ, hệ thống tập trung dữ liệu bảo mật trên Amazon S3.

Điều này giúp:

- Dễ dàng tìm kiếm dữ liệu.
- Hỗ trợ điều tra sự cố.
- Lưu trữ log dài hạn.
- Giảm độ phức tạp khi vận hành.
- **Tự động hóa phản ứng sự cố:**
  Sự kết hợp giữa Security Hub, EventBridge, Step Functions và Lambda tạo thành một mô hình SOAR thu nhỏ.

Hệ thống không chỉ phát hiện vấn đề mà còn có khả năng tự động thực hiện hành động phản ứng, giúp giảm thời gian xử lý sự cố.

- **Áp dụng nguyên tắc Least Privilege:**
  Các dịch vụ trong hệ thống được cấp quyền thông qua IAM Role với phạm vi quyền hạn tối thiểu.

IAM Access Analyzer hỗ trợ kiểm tra các quyền truy cập không mong muốn, giúp giảm nguy cơ lộ dữ liệu hoặc sử dụng sai quyền.

- **Khả năng mở rộng cao:**
  Kiến trúc Event-driven giúp hệ thống dễ dàng mở rộng thêm:

- Thêm nguồn dữ liệu bảo mật mới.
- Thêm workflow phản ứng mới.
- Tích hợp SIEM.
- Tích hợp AI phân tích Security Finding.

- **Dễ dàng kiểm thử:**
  AWS cung cấp các tính năng như GuardDuty Sample Findings và Security Hub Sample Findings giúp mô phỏng sự cố bảo mật.

Nhờ đó có thể kiểm tra toàn bộ quy trình:
**Detect → Respond → Recover**
mà không cần chờ xảy ra tấn công thực tế.

---

### 9. Kết quả kỳ vọng

- **Cải tiến kỹ thuật:**
  Xây dựng thành công mô hình Security Operations Center (SOC) trên nền tảng AWS theo kiến trúc Serverless kết hợp Event-driven, có khả năng tự động thu thập nhật ký, phát hiện mối đe dọa, điều phối phản ứng sự cố và gửi cảnh báo theo thời gian thực. Hệ thống hỗ trợ lưu trữ tập trung log trên Amazon S3, phân tích bằng Amazon Athena và giám sát thông qua Amazon CloudWatch Dashboard.

- **Giá trị lâu dài:**
  Xây dựng được một kiến trúc Cloud Security hiện đại, áp dụng các nguyên tắc Defense in Depth, Least Privilege và Automated Incident Response. Hệ thống có khả năng mở rộng lên Multi-Account, Multi-Region, tích hợp thêm các dịch vụ bảo mật của AWS hoặc nền tảng SIEM, đồng thời là mô hình tham khảo phục vụ học tập, nghiên cứu và triển khai các giải pháp SOC trong thực tế.
