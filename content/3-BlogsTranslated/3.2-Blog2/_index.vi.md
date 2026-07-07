---
title: 'Blog 2'
date: 2024-07-07
weight: 2
chapter: false
pre: ' <b> 3.2. </b> '
---

# Thêm lớp giọng nói vào các cuộc trò chuyện WhatsApp với AWS End User Messaging

Các doanh nghiệp trên toàn thế giới sử dụng WhatsApp như một trong những kênh chính để giao tiếp với khách hàng. Đây là nền tảng quen thuộc, đáng tin cậy và hiệu quả cho nhiều tình huống như xác nhận lịch hẹn, hỗ trợ khách hàng, gửi thông báo và các hoạt động kinh doanh khác. Tuy nhiên, phần lớn các cuộc trò chuyện hiện nay vẫn chỉ dựa trên tin nhắn văn bản.

Mặc dù nhắn tin văn bản rất tiện lợi, nhưng trong nhiều trường hợp việc gõ phím có thể chậm, bất tiện hoặc không thể truyền tải đầy đủ ý định của người dùng. Khi đó, tin nhắn thoại mang đến một phương thức giao tiếp tự nhiên và hiệu quả hơn.

Trong bài viết này, AWS giới thiệu cách **AWS End User Messaging** cho phép doanh nghiệp nhận và phản hồi tin nhắn thoại trên WhatsApp. Bằng cách kết hợp các dịch vụ như AWS Lambda, Amazon Transcribe, Amazon Polly và Amazon SNS, doanh nghiệp có thể xây dựng giải pháp giao tiếp voice-to-voice mà không cần triển khai các cuộc gọi thoại thời gian thực.

---

## Vì sao tin nhắn thoại quan trọng

Tin nhắn văn bản vẫn là phương thức giao tiếp phổ biến, tuy nhiên tin nhắn thoại mang lại nhiều lợi ích riêng.

Một số ưu điểm nổi bật gồm:

- Truyền tải cảm xúc, ngữ điệu và mức độ nhấn mạnh tốt hơn.
- Giao tiếp nhanh hơn vì nói thường nhanh hơn gõ trên thiết bị di động.
- Cải thiện khả năng tiếp cận cho người cao tuổi hoặc người gặp khó khăn về thị lực.
- Linh hoạt hơn khi người dùng có thể lựa chọn giữa giọng nói và văn bản tùy theo hoàn cảnh.

Thay vì thay thế tin nhắn văn bản, tin nhắn thoại đóng vai trò bổ sung, giúp nâng cao trải nghiệm giao tiếp với khách hàng.

---

## Các trường hợp sử dụng phổ biến

Tin nhắn thoại đặc biệt hữu ích trong những tình huống mà việc nói thuận tiện hơn so với gõ văn bản.

Một số trường hợp sử dụng điển hình gồm:

- Người lớn tuổi thích nghe và nói hơn là đọc và gõ.
- Nhân viên hiện trường hoặc tài xế không thuận tiện để nhập văn bản trong khi làm việc.
- Các ứng dụng y tế, nơi bệnh nhân có thể mô tả triệu chứng bằng giọng nói tự nhiên hơn.
- Nhà hàng và dịch vụ du lịch, nơi khách hàng có thể đặt bàn hoặc đặt dịch vụ nhanh chóng.
- Hỗ trợ khách hàng đối với các vấn đề phức tạp cần giải thích bằng lời nói.

Những tình huống này cho thấy tin nhắn thoại có thể nâng cao hiệu quả giao tiếp cũng như cải thiện trải nghiệm của khách hàng.

---

## AWS End User Messaging và WhatsApp

AWS End User Messaging là dịch vụ được AWS quản lý hoàn toàn, cho phép doanh nghiệp gửi và nhận tin nhắn thông qua nhiều kênh khác nhau, bao gồm:

- WhatsApp
- SMS
- MMS (chỉ tại Hoa Kỳ)
- Cuộc gọi thoại đi (Outbound Voice)
- Thông báo đẩy (Push Notifications)

Đối với WhatsApp, các tin nhắn đến sẽ tự động được chuyển vào một Amazon SNS Topic, từ đó có thể tích hợp với các dịch vụ AWS khác như:

- Amazon SNS
- Amazon SQS
- AWS Lambda
- Amazon Bedrock

Kiến trúc hướng sự kiện (Event-driven Architecture) này giúp việc xử lý cả tin nhắn văn bản và tin nhắn thoại trở nên đơn giản thông qua các dịch vụ serverless.

Đối với xử lý giọng nói, nhà phát triển có thể kết hợp các dịch vụ AI của AWS như:

- Amazon Transcribe để chuyển giọng nói thành văn bản (Speech-to-Text).
- Amazon Polly để chuyển văn bản thành giọng nói (Text-to-Speech).
- Các mô hình nhận dạng giọng nói của bên thứ ba như Whisper thông qua Amazon Bedrock Marketplace.

---

## Kiến trúc Voice-to-Voice Messaging

Nhờ kiến trúc linh hoạt của AWS End User Messaging, doanh nghiệp có thể xây dựng quy trình giao tiếp voice-to-voice hoàn chỉnh.

Quy trình hoạt động gồm các bước sau:

1. Khách hàng gửi một tin nhắn thoại qua WhatsApp.
2. AWS End User Messaging tiếp nhận tin nhắn.
3. Amazon SNS phát hành sự kiện (Inbound Event).
4. AWS Lambda tải xuống và xử lý tệp âm thanh.
5. Amazon Transcribe (hoặc Whisper) chuyển giọng nói thành văn bản.
6. Chatbot hoặc ứng dụng hội thoại xử lý nội dung yêu cầu.
7. Amazon Polly chuyển phản hồi thành giọng nói tự nhiên.
8. AWS End User Messaging gửi tin nhắn thoại phản hồi trở lại cho khách hàng qua WhatsApp.

Do giải pháp xử lý các tệp âm thanh đã được ghi sẵn nên đây là mô hình xử lý bất đồng bộ (Asynchronous Messaging), khác với cuộc gọi thoại thời gian thực.

---

## Giải pháp mẫu

AWS cung cấp một dự án mã nguồn mở sử dụng AWS CDK để minh họa kiến trúc này.

Dự án mẫu thực hiện các chức năng sau:

- Nhận tin nhắn thoại từ WhatsApp.
- Chuyển giọng nói thành văn bản.
- Xử lý nội dung bằng chatbot.
- Tạo phản hồi bằng giọng nói tự nhiên.
- Gửi phản hồi thoại trở lại WhatsApp.

Giải pháp hỗ trợ nhiều chế độ triển khai:

- Chỉ nhận tin nhắn (Inbound Only)
- Chỉ gửi tin nhắn (Outbound Only)
- Giao tiếp Voice-to-Voice hoàn chỉnh

Các tính năng hiện có bao gồm:

- Mã hóa toàn bộ dữ liệu bằng AWS KMS.
- Cho phép cấu hình Amazon SNS Topic.
- Lựa chọn giữa Amazon Transcribe và Whisper để nhận dạng giọng nói.
- Hỗ trợ chuyển văn bản thành giọng nói bằng Amazon Polly.
- Hỗ trợ xử lý đồng thời cả tin nhắn văn bản và tin nhắn thoại.

---

## Bắt đầu triển khai

Giải pháp hoàn chỉnh được cung cấp dưới dạng dự án AWS CDK mã nguồn mở.

Trước khi triển khai, cần chuẩn bị:

- Một tài khoản AWS với đầy đủ quyền cần thiết.
- Node.js phiên bản 18 trở lên.
- AWS CDK CLI đã được cài đặt.
- Một tài khoản WhatsApp Business đã đăng ký với AWS End User Messaging.

Khi đăng ký WhatsApp Business Account, cần tạo một doanh nghiệp trên Meta. Số điện thoại sử dụng phải chưa từng được liên kết với tài khoản WhatsApp cá nhân. Sau đó, kích hoạt ứng dụng WhatsApp Business bằng chính số điện thoại này.

---

## Triển khai giải pháp

Đầu tiên, sao chép (clone) dự án mẫu và cài đặt các thư viện cần thiết.

```bash
npm install
```

Tiếp theo, cấu hình **WhatsApp Phone Number ID** trong tệp `config.params.json`. Nếu chưa cấu hình, AWS CDK sẽ yêu cầu nhập thông tin này trong quá trình triển khai.

Biên dịch dự án:

```bash
npm run build
```

Triển khai hạ tầng:

```bash
cdk deploy
```

Sau khi triển khai, AWS CDK sẽ tự động tạo toàn bộ tài nguyên cần thiết, bao gồm:

- Các hàm AWS Lambda
- Các Amazon SNS Topic
- Các Amazon S3 Bucket
- Các IAM Role

Để biết thêm chi tiết về quá trình cấu hình, có thể tham khảo tài liệu trong GitHub Repository do AWS cung cấp.

Khi không còn sử dụng, có thể xóa toàn bộ tài nguyên để tránh phát sinh chi phí:

```bash
cdk destroy
```

---

## Kết luận

Tin nhắn thoại đã trở thành một phương thức giao tiếp quen thuộc trong các cuộc trò chuyện cá nhân trên WhatsApp. Việc đưa khả năng này vào các cuộc hội thoại giữa doanh nghiệp và khách hàng giúp quá trình giao tiếp trở nên tự nhiên, dễ tiếp cận và hiệu quả hơn.

Bằng cách kết hợp AWS End User Messaging với các dịch vụ như AWS Lambda, Amazon Transcribe, Amazon Polly và Amazon SNS, nhà phát triển có thể xây dựng các giải pháp giao tiếp bằng giọng nói có khả năng mở rộng mà không làm thay đổi cách khách hàng tương tác với doanh nghiệp.

Dự án mẫu AWS CDK là điểm khởi đầu phù hợp để thử nghiệm giải pháp voice-to-voice và mở rộng cho các nhu cầu thực tế của doanh nghiệp.

---

## Bài viết gốc

https://aws.amazon.com/vi/blogs/messaging-and-targeting/adding-a-voice-layer-to-whatsapp-conversations-with-aws-end-user-messaging/
