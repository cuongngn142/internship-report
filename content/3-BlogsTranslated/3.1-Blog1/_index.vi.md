---
title: 'Blog 1'
date: 2024-07-07
weight: 1
chapter: false
pre: ' <b> 3.1. </b> '
---

# Tùy chỉnh Federated Sign-In với Inbound Federation Lambda Trigger trong Amazon Cognito

Khi xây dựng các ứng dụng sử dụng Federated Sign-In với Amazon Cognito, nhà phát triển thường tích hợp đăng nhập thông qua Google, Microsoft Entra ID (Azure AD), Facebook hoặc các Identity Provider (IdP) khác. Tuy nhiên, sau khi IdP xác thực thành công, Amazon Cognito sẽ xử lý và lưu thông tin người dùng gần như ngay lập tức. Điều này khiến việc chuẩn hóa dữ liệu, lọc thuộc tính hoặc tự động liên kết tài khoản thường phải được thực hiện ở backend hoặc thông qua các Lambda Trigger khác chưa thực sự phù hợp.

Trong bài viết này, AWS giới thiệu **Inbound Federation Lambda Trigger** – một Lambda Trigger mới của Amazon Cognito cho phép can thiệp trực tiếp vào dữ liệu người dùng nhận từ Identity Provider trước khi Cognito tạo hoặc cập nhật hồ sơ người dùng trong User Pool. Tính năng này giúp đơn giản hóa việc tích hợp với các hệ thống nhận dạng bên ngoài, giảm lượng logic xử lý ở backend và mang lại khả năng kiểm soát linh hoạt hơn đối với luồng Federated Sign-In.

---

## Tổng quan về Inbound Federation Lambda Trigger

Inbound Federation Lambda Trigger được thực thi sau khi người dùng xác thực thành công với Identity Provider và trước khi Amazon Cognito ghi dữ liệu vào User Pool.

Tại thời điểm này, Lambda có thể truy cập nhiều thông tin như:

- User Pool ID
- App Client ID
- Identity Provider đang sử dụng
- Loại giao thức xác thực (SAML, OIDC, Login with Amazon,...)
- Toàn bộ thuộc tính người dùng do IdP trả về

Từ các thông tin trên, nhà phát triển có thể:

- Chuẩn hóa thuộc tính người dùng
- Thêm hoặc loại bỏ thuộc tính
- Lọc danh sách Group
- Gọi API của hệ thống bên ngoài
- Tự động liên kết tài khoản người dùng

Sau khi Lambda hoàn tất xử lý, Cognito mới tiếp tục tạo hoặc cập nhật User Profile và phát hành Access Token, ID Token cùng Refresh Token cho ứng dụng.

---

## Luồng hoạt động

So với Federated Sign-In truyền thống, luồng xác thực hầu như không thay đổi. Người dùng vẫn được chuyển hướng đến Identity Provider để đăng nhập và xác thực.

Điểm khác biệt là sau khi Identity Provider trả về thông tin người dùng, Amazon Cognito sẽ gọi Inbound Federation Lambda Trigger trước khi lưu dữ liệu vào User Pool.

Quá trình hoạt động gồm các bước:

1. Người dùng đăng nhập thông qua Identity Provider.
2. Cognito chuyển hướng đến IdP để xác thực.
3. IdP xác thực thành công và trả về thông tin người dùng.
4. Cognito kích hoạt Inbound Federation Lambda Trigger.
5. Lambda xử lý, chuẩn hóa hoặc bổ sung dữ liệu.
6. Cognito cập nhật User Pool.
7. Cognito phát hành Token cho ứng dụng.

Nhờ điểm mở rộng này, toàn bộ dữ liệu người dùng đều có thể được xử lý trước khi lưu vào Cognito.

---

## Các trường hợp sử dụng phổ biến

### Lọc thuộc tính Group có kích thước lớn

Trong các hệ thống B2B hoặc SaaS, Identity Provider có thể gửi hàng trăm nhóm (Group Membership) của người dùng.

Nếu toàn bộ thông tin này được lưu vào Cognito, kích thước thuộc tính có thể vượt quá giới hạn của User Pool và khiến quá trình đăng nhập thất bại.

Ví dụ, Active Directory có thể trả về hơn 200 Group nhưng ứng dụng chỉ sử dụng hai Group để phân quyền. Lambda Trigger sẽ loại bỏ các Group không cần thiết trước khi Cognito lưu hồ sơ người dùng, giúp giảm dữ liệu dư thừa và đảm bảo quá trình xác thực diễn ra thành công.

---

### Tự động liên kết tài khoản

Trong các ứng dụng B2C, người dùng có thể đăng ký bằng Email/Password nhưng sau đó đăng nhập bằng Google hoặc Facebook.

Nếu không thực hiện Account Linking, Cognito sẽ tạo nhiều User Profile khác nhau cho cùng một người dùng.

Inbound Federation Lambda Trigger cho phép kiểm tra tài khoản đã tồn tại dựa trên email hoặc các thuộc tính định danh khác, sau đó tự động liên kết Identity Provider với tài khoản hiện có.

Nhờ đó, người dùng chỉ có một hồ sơ duy nhất trong Cognito User Pool và toàn bộ dữ liệu được đồng bộ xuyên suốt.

---

### Chuẩn hóa và bổ sung dữ liệu người dùng

Một số Identity Provider sử dụng các tên thuộc tính khác nhau như:

- given_name
- first_name
- displayName

Lambda Trigger có thể chuẩn hóa toàn bộ về cùng một định dạng trước khi lưu vào User Pool.

Ngoài ra, Lambda còn có thể gọi API của hệ thống bên ngoài để lấy thêm thông tin như:

- Vai trò (Role)
- Quyền (Permission)
- Department
- Tenant
- Subscription

Những dữ liệu này sẽ được bổ sung vào hồ sơ người dùng trước khi Cognito phát hành Token.

---

## Các khuyến nghị khi triển khai

Khi sử dụng Inbound Federation Lambda Trigger, AWS khuyến nghị:

- Thiết kế Lambda thực thi nhanh để giảm thời gian đăng nhập.
- Sử dụng cơ chế cache nếu cần truy vấn dữ liệu từ hệ thống bên ngoài.
- Theo dõi hiệu năng bằng Amazon CloudWatch.
- Thiết lập cảnh báo cho các trường hợp Timeout hoặc Exception.
- Đối với Apple Sign In, cần lưu ý email ẩn danh có thể khiến việc tự động liên kết tài khoản không khả thi, vì vậy nên xây dựng quy trình liên kết thủ công khi cần.

---

## Kết luận

Inbound Federation Lambda Trigger là một tính năng mới của Amazon Cognito giúp mở rộng khả năng xử lý dữ liệu trong luồng Federated Sign-In. Thay vì phải xây dựng nhiều logic ở backend, nhà phát triển có thể trực tiếp chuẩn hóa dữ liệu, lọc thuộc tính, bổ sung thông tin từ hệ thống bên ngoài hoặc tự động liên kết tài khoản trước khi Cognito cập nhật User Pool.

Đối với các ứng dụng B2B, SaaS và B2C sử dụng Federated Authentication, đây là một tính năng hữu ích giúp đơn giản hóa quá trình tích hợp Identity Provider, tăng tính linh hoạt trong quản lý danh tính và cải thiện trải nghiệm đăng nhập của người dùng.

---

## Bài viết gốc

https://aws.amazon.com/vi/blogs/security/customize-federated-sign-in-with-new-amazon-cognito-lambda-trigger/
