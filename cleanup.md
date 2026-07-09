## 🧹 Hướng Dẫn Dọn Dẹp (Clean Up)

Để tránh phát sinh chi phí không mong muốn, hãy xóa các tài nguyên theo thứ tự ngược lại với thứ tự tạo. **Lưu ý quan trọng**: Một số tài nguyên có dependencies, cần xóa đúng thứ tự để tránh lỗi.

---

### Bước 1: Xóa CloudFront Distribution

1. Mở **Amazon CloudFront console**, chọn distribution `soc-platform`

2. Click **Disable**:
   - Đợi status chuyển sang **Disabled** (có thể mất 10-15 phút)

3. Sau khi disabled, chọn distribution và click **Delete**

---

### Bước 2: Xóa WAF Web ACL

1. Mở **AWS WAF console** (region **us-east-1**)

2. Chọn **Web ACLs** → `soc-platform-web-acl`

3. Tab **Associated AWS resources**:
   - Xóa tất cả associations (nếu còn)

4. Tab **Logging and metrics**:
   - Click **Disable logging**

5. Quay lại danh sách Web ACLs, chọn `soc-platform-web-acl` và click **Delete**

---

### Bước 3: Xóa CloudWatch Resources

#### 3.1 Xóa CloudWatch Alarms

1. Mở **Amazon CloudWatch console**, chọn **Alarms** → **All alarms**

2. Chọn tất cả alarms có prefix `soc-platform-`:
   - `soc-platform-guardduty-critical`
   - `soc-platform-lambda-errors`
   - `soc-platform-waf-high-blocks`

3. Click **Actions** → **Delete**

#### 3.2 Xóa CloudWatch Dashboard

1. Chọn **Dashboards** → `soc-platform-security-dashboard`

2. Click **Delete**

---

### Bước 4: Xóa EventBridge Rules

1. Mở **Amazon EventBridge console**, chọn **Rules**

2. Chọn từng rule và xóa:
   - `soc-platform-guardduty-findings`
   - `soc-platform-securityhub-findings`
   - `soc-platform-accessanalyzer-findings`

3. Với mỗi rule:
   - Click vào rule → Tab **Targets** → **Delete** tất cả targets
   - Quay lại → **Delete** rule

---

### Bước 5: Xóa Step Functions State Machine

1. Mở **AWS Step Functions console**

2. Chọn `soc-platform-security-response`

3. Click **Delete**

4. Xác nhận xóa

---

### Bước 6: Xóa Lambda Functions

1. Mở **AWS Lambda console**

2. Chọn và xóa từng function:
   - `soc-platform-isolate-ec2`
   - `soc-platform-revoke-iam`
   - `soc-platform-send-notification`

3. Với mỗi function: Click **Actions** → **Delete**

---

### Bước 7: Xóa SNS Topics

1. Mở **Amazon SNS console**, chọn **Topics**

2. Chọn và xóa:
   - `soc-platform-critical-alerts`
   - `soc-platform-high-alerts`

3. Với mỗi topic: Click **Delete** và xác nhận

---

### Bước 8: Xóa Security Services

#### 8.1 Disable Security Hub

1. Mở **AWS Security Hub console**

2. Click **Settings** → **General**

3. Click **Disable Security Hub**

4. Xác nhận disable

#### 8.2 Disable GuardDuty

1. Mở **Amazon GuardDuty console**

2. Click **Settings**

3. Scroll xuống cuối, click **Suspend GuardDuty** hoặc **Disable GuardDuty**

4. Xác nhận

#### 8.3 Xóa IAM Access Analyzer

1. Mở **IAM console**, chọn **Access Analyzer**

2. Chọn `soc-platform-iam-analyzer`

3. Click **Delete** và xác nhận

#### 8.4 Xóa AWS Config

1. Mở **AWS Config console**

2. Click **Settings**

3. Click **Edit**

4. Bỏ tick **Recording is on** → **Save**

5. Xóa Config Rules:
   - Chọn **Rules** → Chọn tất cả rules đã tạo
   - Click **Actions** → **Delete rule**

6. Xóa Configuration Recorder và Delivery Channel (qua CLI):
   ```bash
   aws configservice delete-configuration-recorder --configuration-recorder-name soc-platform-recorder
   aws configservice delete-delivery-channel --delivery-channel-name soc-platform-delivery-channel
   ```

---

### Bước 9: Xóa CloudTrail

1. Mở **AWS CloudTrail console**

2. Chọn **Trails** → `soc-platform-trail`

3. Click **Delete**

4. Xác nhận xóa

---

### Bước 10: Xóa VPC Flow Logs

1. Mở **VPC console**, chọn **Your VPCs**

2. Chọn VPC `soc-platform-vpc`

3. Tab **Flow logs** → Chọn flow log → Click **Actions** → **Delete flow logs**

---

### Bước 11: Xóa Athena & Glue Resources

#### 11.1 Xóa Athena Workgroup

1. Mở **Amazon Athena console**, chọn **Workgroups**

2. Chọn `soc-platform-workgroup`

3. Click **Delete** (tick chọn xóa cả query history nếu cần)

#### 11.2 Xóa Glue Database

1. Mở **AWS Glue console**, chọn **Databases**

2. Chọn `soc_platform_logs_db`

3. Click **Delete**

---

### Bước 12: Xóa Application Load Balancer

1. Mở **EC2 console**, chọn **Load Balancers**

2. Chọn `soc-platform-alb`

3. Click **Actions** → **Delete load balancer**

4. Xác nhận bằng cách gõ `confirm`

#### Xóa Target Group

1. Chọn **Target Groups** → `soc-platform-tg`

2. Click **Actions** → **Delete**

---

### Bước 13: Xóa NAT Gateway & Elastic IP

#### 13.1 Xóa NAT Gateway

1. Mở **VPC console**, chọn **NAT Gateways**

2. Chọn `soc-platform-nat-gw`

3. Click **Actions** → **Delete NAT gateway**

4. Xác nhận và đợi status chuyển sang **Deleted** (mất vài phút)

#### 13.2 Release Elastic IP

1. Chọn **Elastic IPs**

2. Chọn EIP có tag `soc-platform-nat-eip`

3. Click **Actions** → **Release Elastic IP addresses**

---

### Bước 14: Xóa Security Groups

1. Mở **EC2 console**, chọn **Security Groups**

2. Xóa theo thứ tự (để tránh dependency errors):
   - Đầu tiên: `soc-platform-isolation-sg`
   - Tiếp theo: `soc-platform-app-sg`
   - Cuối cùng: `soc-platform-alb-sg`

3. Với mỗi security group: Click **Actions** → **Delete security groups**

> **Lưu ý**: Không thể xóa default security group của VPC

---

### Bước 15: Xóa VPC Components

#### 15.1 Xóa Route Table Associations & Route Tables

1. Mở **VPC console**, chọn **Route Tables**

2. Với `soc-platform-private-rt`:
   - Tab **Subnet associations** → **Edit subnet associations** → Bỏ chọn subnet → **Save**
   - Quay lại → Click **Actions** → **Delete route table**

3. Với `soc-platform-public-rt`:
   - Làm tương tự như trên

> **Lưu ý**: Không thể xóa main route table

#### 15.2 Xóa Subnets

1. Chọn **Subnets**

2. Chọn `soc-platform-public-subnet` → **Actions** → **Delete subnet**

3. Chọn `soc-platform-private-subnet` → **Actions** → **Delete subnet**

#### 15.3 Detach & Delete Internet Gateway

1. Chọn **Internet Gateways**

2. Chọn `soc-platform-igw`

3. Click **Actions** → **Detach from VPC**

4. Click **Actions** → **Delete internet gateway**

#### 15.4 Xóa VPC

1. Chọn **Your VPCs**

2. Chọn `soc-platform-vpc`

3. Click **Actions** → **Delete VPC**

4. Xác nhận bằng cách gõ `delete`

---

### Bước 16: Xóa S3 Bucket

> **Lưu ý**: Bucket phải empty trước khi xóa

1. Mở **Amazon S3 console**

2. Chọn bucket `soc-platform-logs-<account-id>`

3. Click **Empty**:
   - Gõ `permanently delete` để xác nhận
   - Đợi quá trình xóa hoàn tất (có thể mất thời gian nếu có nhiều objects)

4. Sau khi empty, click **Delete**:
   - Gõ tên bucket để xác nhận

---

### Bước 17: Xóa KMS Key

1. Mở **AWS KMS console**

2. Chọn **Customer managed keys**

3. Chọn key có alias `soc-platform-key`

4. Click **Key actions** → **Schedule key deletion**

5. **Waiting period**: Chọn số ngày chờ (tối thiểu 7 ngày, mặc định 30 ngày)

6. Tick xác nhận và click **Schedule deletion**

> **Lưu ý**: KMS key sẽ không bị xóa ngay mà sẽ chờ trong khoảng thời gian đã chọn. Trong thời gian này, bạn có thể cancel nếu cần.

---

### Bước 18: Xóa IAM Roles

1. Mở **IAM console**, chọn **Roles**

2. Tìm và xóa các roles:
   - `soc-platform-lambda-execution-role`
   - `soc-platform-stepfunctions-role`
   - `soc-platform-eventbridge-role`
   - `soc-platform-config-role`
   - `soc-platform-vpc-flowlogs-role`

3. Với mỗi role: Click vào role → **Delete** → Xác nhận

---

---

> **Lưu ý**: Đợi mỗi stack xóa xong trước khi xóa stack tiếp theo để tránh dependency errors.

---

## ⚠️ Lưu Ý Quan Trọng

1. **S3 Bucket với Versioning**: Khi bucket có versioning enabled, cần xóa cả current versions và delete markers. Sử dụng **Empty bucket** sẽ tự động xử lý việc này.

2. **KMS Key**: Key không bị xóa ngay mà có waiting period. Nếu cần hủy schedule deletion:
   ```bash
   aws kms cancel-key-deletion --key-id <key-id>
   aws kms enable-key --key-id <key-id>
   ```

3. **CloudFront Distribution**: Phải disable trước khi xóa và quá trình disable mất 10-15 phút.

4. **NAT Gateway**: Tiếp tục tính phí cho đến khi status là **Deleted**, không chỉ **Deleting**.

5. **Elastic IP**: Bạn sẽ bị charge nếu EIP không được associate với running instance, nên hãy release ngay sau khi xóa NAT Gateway.

6. **Config Rules**: Một số managed rules có thể mất vài phút để xóa hoàn toàn.

7. **Security Groups với Cross-references**: Nếu gặp lỗi khi xóa, kiểm tra xem có security group nào reference đến security group khác không, và xóa rule đó trước.

---

Chúc bạn dọn dẹp thành công! Nếu gặp bất kỳ lỗi nào trong quá trình xóa, hãy cho mình biết nhé! 🧹✨