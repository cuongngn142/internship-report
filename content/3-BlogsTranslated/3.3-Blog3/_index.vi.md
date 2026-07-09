---
title: 'Blog 3'
date: 2024-07-09
weight: 3
chapter: false
pre: ' <b> 3.3. </b> '
---

# Cách Amazon Bedrock phòng chống các cuộc tấn công phishing do AI tạo ra

Trong nhiều năm, các hệ thống bảo mật email chủ yếu dựa trên các quy tắc phát hiện truyền thống như lỗi chính tả, lời chào chung chung hoặc tên miền người gửi không hợp lệ để nhận diện các email phishing. Tuy nhiên, với sự phát triển của Generative AI, những dấu hiệu này đang dần biến mất.

Ngày nay, kẻ tấn công có thể sử dụng các mô hình AI kết hợp cùng nguồn thông tin công khai (OSINT) để tạo ra những email có ngữ pháp hoàn hảo, nội dung phù hợp với từng người nhận và mang tính cá nhân hóa rất cao. Điều này khiến các giải pháp lọc email truyền thống khó có thể phát hiện chính xác.

Trong bài viết này, AWS giới thiệu cách **Amazon Bedrock** kết hợp các **Foundation Models**, **Amazon Bedrock Guardrails** và cơ chế phân tích hành vi để phát hiện các email phishing do AI tạo ra trước khi chúng đến hộp thư người dùng.

---

## Sự thay đổi của các cuộc tấn công phishing

Các hệ thống chống phishing truyền thống thường phát hiện email dựa trên những dấu hiệu như:

- Lỗi chính tả và ngữ pháp.
- Lời chào chung chung.
- Logo hoặc thương hiệu giả mạo.
- Tên miền người gửi không khớp.
- Định dạng email bất thường.

Trong nhiều năm, những phương pháp này mang lại hiệu quả rất cao.

Tuy nhiên, với sự hỗ trợ của Generative AI, các cuộc tấn công phishing hiện đại đã thay đổi hoàn toàn.

Kẻ tấn công có thể:

- Thu thập dữ liệu từ các nguồn OSINT.
- Phân tích lượng lớn thông tin công khai về doanh nghiệp và người dùng.
- Sinh ra hàng nghìn email khác nhau với nội dung hoàn toàn tự nhiên.
- Cá nhân hóa từng email theo vai trò, phòng ban hoặc lịch sử giao tiếp.
- Điều chỉnh nội dung theo thời gian thực dựa trên phản hồi của nạn nhân.

Kết quả là nhiều email phishing hiện nay có chất lượng tương đương với email hợp lệ và không còn kích hoạt các bộ lọc truyền thống.

---

## Amazon Bedrock hỗ trợ phát hiện phishing như thế nào

Amazon Bedrock là dịch vụ Generative AI được quản lý hoàn toàn của AWS, cho phép sử dụng nhiều Foundation Models từ AWS và các đối tác AI để xây dựng các ứng dụng AI an toàn, riêng tư và có trách nhiệm.

Thay vì chỉ kiểm tra ngữ pháp hay từ khóa, Amazon Bedrock bổ sung thêm một lớp **phân tích hành vi (Behavior Analysis Layer)** nhằm đánh giá:

- Ngữ cảnh của email.
- Hành vi giao tiếp của người gửi.
- Các dấu hiệu thao túng tâm lý.
- Những điểm bất thường trong nội dung.

Nhờ đó, hệ thống có thể phát hiện những cuộc tấn công phishing tinh vi mà các giải pháp dựa trên quy tắc (Rule-based Detection) khó nhận ra.

---

## Hai thành phần chính của giải pháp

### Foundation Models

Các Foundation Models chịu trách nhiệm phân tích nội dung email bằng khả năng hiểu ngôn ngữ tự nhiên.

Mô hình có thể:

- Hiểu mối quan hệ ngữ cảnh trong email.
- Phát hiện các hành vi thao túng tinh vi.
- Xác định các điểm bất thường trong cách giao tiếp.
- Nhận diện các mẫu giả mạo mới chưa từng xuất hiện.

Thay vì tìm kiếm lỗi chính tả, mô hình đánh giá ý nghĩa và mục đích của toàn bộ nội dung email.

---

### Amazon Bedrock Guardrails

Amazon Bedrock Guardrails cung cấp các cơ chế bảo vệ nhằm đảm bảo việc phân tích AI luôn tuân thủ chính sách bảo mật của tổ chức.

Các khả năng chính gồm:

- Bộ lọc nội dung (Content Filters).
- Bộ lọc từ ngữ.
- Danh sách chủ đề bị từ chối.
- Phát hiện thông tin nhạy cảm.
- Contextual Grounding nhằm giảm hiện tượng Model Hallucination.

Nhờ vậy, kết quả phân tích có độ chính xác cao hơn và giảm số lượng cảnh báo giả (False Positive).

---

## Quy trình phân tích email gồm 5 bước

Amazon Bedrock được tích hợp vào hệ thống email dưới dạng một lớp phân tích chạy song song với hạ tầng hiện có.

Toàn bộ quá trình chỉ diễn ra trong vài mili giây trước khi email được chuyển tới người dùng.

### Bước 1. Input Guardrails và tiền xử lý

Email đầu vào được kiểm tra bởi Amazon Bedrock Guardrails.

Các nội dung nhạy cảm hoặc bất thường sẽ được đánh dấu để xem xét trước khi tiếp tục quá trình phân tích.

---

### Bước 2. Xây dựng Prompt có ngữ cảnh

Hệ thống tạo một Prompt phân tích bằng cách kết hợp:

- Nội dung email.
- Lịch sử giao tiếp của người gửi.
- Ngữ cảnh tổ chức.
- Các ví dụ phishing đã biết.

Các dữ liệu này được truy xuất thông qua Amazon Bedrock Knowledge Bases.

---

### Bước 3. Phân tích bằng Foundation Models

Foundation Models thực hiện phân tích email dựa trên Prompt đã xây dựng.

Trong quá trình này, Guardrails đảm bảo mô hình chỉ đưa ra kết quả trong phạm vi chính sách bảo mật đã định nghĩa.

---

### Bước 4. Chấm điểm rủi ro đa yếu tố

Sau khi phân tích, hệ thống đánh giá mức độ nguy hiểm của email dựa trên ba nhóm tiêu chí:

- Nội dung bất thường.
- Hành vi sai lệch.
- Chi tiết ngữ cảnh.

Các yếu tố này được tổng hợp thành điểm rủi ro để phục vụ quyết định xử lý.

---

### Bước 5. Phân loại và định tuyến

Dựa trên điểm rủi ro, email sẽ được xử lý tự động:

- Email an toàn được chuyển tới người dùng.
- Email đáng ngờ được chuyển cho đội ngũ bảo mật.
- Email nguy hiểm bị chặn trước khi đến hộp thư.

---

## Vòng lặp phản hồi liên tục

Một trong những điểm mạnh của giải pháp là khả năng cải thiện độ chính xác theo thời gian thông qua Continuous Feedback Loop.

Quy trình gồm năm giai đoạn:

### Analyze

Foundation Models phân tích email bằng Prompt động dựa trên dữ liệu phishing và ngữ cảnh người gửi.

### Score

Hệ thống gán điểm rủi ro từ 0 đến 100 và cách ly các email đáng ngờ.

### Review

Đội ngũ bảo mật xác minh các email đã bị đánh dấu để xác định:

- Phishing thực sự.
- Cảnh báo giả (False Positive).

### Learn

Các kết quả xác minh được bổ sung vào:

- Thư viện ví dụ.
- Hồ sơ hành vi người gửi.
- Bộ dữ liệu về các mẫu phishing mới.

### Enhance

Các ví dụ mới được sử dụng trong Dynamic Prompt Engineering và Few-shot Learning nhằm cải thiện chất lượng phân tích cho các email tiếp theo.

Qua thời gian, hệ thống ngày càng hiểu rõ hành vi giao tiếp bình thường của tổ chức và giảm đáng kể số lượng cảnh báo sai.

---

## Lợi ích của giải pháp

Việc kết hợp Amazon Bedrock với hạ tầng bảo mật email hiện có mang lại nhiều lợi ích:

- Phát hiện các email phishing do AI tạo ra.
- Hiểu ngữ cảnh thay vì chỉ dựa trên từ khóa.
- Phân tích hành vi giao tiếp của người gửi.
- Giảm tỷ lệ False Positive.
- Không cần thay đổi hệ thống email hiện tại.
- Liên tục học hỏi từ các cuộc tấn công mới.
- Tự động phân loại và định tuyến email theo mức độ rủi ro.

---

## Kết luận

Sự phát triển của Generative AI đã làm thay đổi hoàn toàn cách thức thực hiện các cuộc tấn công phishing. Những email được tạo ra ngày càng tự nhiên, chính xác và khó phân biệt với email hợp lệ.

Amazon Bedrock giải quyết thách thức này bằng cách kết hợp Foundation Models, Amazon Bedrock Guardrails và cơ chế phân tích hành vi để phát hiện các dấu hiệu thao túng tinh vi mà các hệ thống dựa trên quy tắc truyền thống không thể nhận ra.

Nhờ vòng lặp phản hồi liên tục, hệ thống ngày càng cải thiện độ chính xác, giảm cảnh báo giả và hỗ trợ đội ngũ bảo mật tập trung xử lý các mối đe dọa thực sự, trong khi hạ tầng email hiện tại vẫn hoạt động bình thường.

---

## Bài viết gốc

https://aws.amazon.com/vi/blogs/machine-learning/how-amazon-bedrock-catches-ai-generated-phishing/
