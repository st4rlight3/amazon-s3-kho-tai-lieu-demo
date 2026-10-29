# Bản trình chiếu chính để chỉnh trong Canva

Bản bàn giao chính là [slides/Amazon-S3-CloudNotes-45-slide.pptx](slides/Amazon-S3-CloudNotes-45-slide.pptx), gồm **45 slide, tỷ lệ 16:9**, kèm [dàn ý 45 slide](docs/dan-y-45-slide.md). Dùng tệp PowerPoint này để trình chiếu hoặc nhập vào Canva; không tạo lại bản chính từ prompt 30 slide cũ.

Xem trực tuyến: **[45 slide trên Canva](https://canva.link/578jhfpdcv8ehhh)**. Liên kết công khai chỉ cho phép xem và không yêu cầu đăng nhập.

Bài hướng tới **30–40 phút**, với ba chức năng demo AWS Console ở phần cuối. Đây là thời lượng mục tiêu, chưa được xác nhận bằng một buổi luyện toàn bài. Nhóm cần tập để điều chỉnh nhịp nói và thao tác.

Repository [st4rlight3/amazon-s3-kho-tai-lieu-demo](https://github.com/st4rlight3/amazon-s3-kho-tai-lieu-demo) hiện **public**, mở được không cần đăng nhập GitHub. Có thể tạo QR repository trên slide 45. Bucket S3 của demo vẫn riêng tư; không tạo QR cho presigned URL.

## 1. Nhập bản chính và kiểm tra trong Canva

1. Tải tệp PowerPoint 45 slide từ liên kết trên về máy rồi nhập tệp vào Canva để mở thành bản trình chiếu có thể chỉnh sửa.
2. Kiểm tra thiết kế có đúng **45 trang**, đúng thứ tự và tỷ lệ 16:9. Đối chiếu tiêu đề, nội dung và nguồn với [dàn ý 45 slide](docs/dan-y-45-slide.md).
3. Thay tên nhóm và lớp trên trang đầu. Kiểm tra dấu tiếng Việt, xuống dòng, khoảng cách và chữ có bị tràn sau khi Canva chuyển đổi tệp.
4. Kiểm tra ghi chú thuyết trình và liên kết nguồn. Nếu ghi chú chưa được giữ khi nhập, dùng phần **Gợi ý nói** trong dàn ý để bổ sung vào đúng trang.
5. Giữ các ảnh demo thật trong thiết kế. Chỉ tải lại ảnh từ repository khi ảnh thiếu hoặc cần thay cách cắt; không dùng AI vẽ lại giao diện AWS để làm bằng chứng.
6. Tập trình chiếu và thao tác thật theo phần demo bên dưới, rồi căn tổng thời lượng 30–40 phút.

Giữ nền navy/charcoal, chữ sáng, điểm nhấn cyan và cam tiết chế. Dùng font sans serif đủ dấu tiếng Việt; ưu tiên chữ đọc rõ trên màn chiếu. Ảnh nền trung tâm dữ liệu chỉ là hình minh họa. Ảnh Console và phản hồi S3 mới là bằng chứng cho các thao tác đã kiểm chứng.

## 2. Ba chức năng demo ở phần cuối

| Slide trong bản 45 slide | Nội dung |
| --- | --- |
| 36–37 | Bài toán kho tài liệu và cấu hình chuẩn bị |
| 38 | Demo 1: Upload V1 và download để kiểm tra |
| 39–40 | Demo 2: Upload V2 cùng key, lấy lại V1 từ S3 rồi upload thành V3 |
| 41–42 | Demo 3: URL thường bị chặn, presigned URL còn hạn đọc được, request mới sau hạn bị từ chối |
| 43 | Kết quả và dọn tài nguyên sau buổi học |
| 44–45 | Kiến thức cần nhớ, tài liệu và repository |

Tạo bucket và bật Versioning từ trước buổi học; khi bật Versioning lần đầu, làm theo thời gian chờ trong [hướng dẫn demo](docs/demo-aws-console.md). Dàn 45 slide quyết định số trang của bản chính; các số trang và nhịp thời gian trong hướng dẫn cũ chỉ dùng để tham khảo thao tác.

**Chú thích phải giữ ở phần hết hạn:** “Ảnh kiểm thử: 5 phút (300 giây); demo trực tiếp: 1 phút.” Ảnh lỗi thật ghi rõ 300 giây. Khi diễn trực tiếp, tạo URL mới với thời hạn một phút và gửi request mới sau hạn. File đã tải không tự biến mất khi URL hết hiệu lực.

## 3. Ảnh thật và vị trí trong bản 45 slide

Tám ảnh trong [assets/demo](assets/demo/README.md) đã được chụp từ AWS S3 thật. [Báo cáo demo](docs/ket-qua-demo.md) ghi kết quả kiểm chứng. Bảng dưới dùng số trang của **bản 45 slide**, thay cho số trang của bản cũ trong danh mục ảnh.

| Tệp trong assets/demo/ | Slide phù hợp | Điều cần giữ |
| --- | --- | --- |
| 01-bucket-rieng-tu.jpg | 18, 36 | Block Public Access bật; bucket vẫn riêng tư |
| 02-upload-thanh-cong.jpg | 38 | Upload thành công vào bucket demo |
| 03-cac-phien-ban.jpg | 22, 40 | Ba versions của cùng key; bản hiện tại đã phục hồi |
| 04-khoi-phuc-v1.jpg | 40 | Nội dung có lịch đúng “Thu Sau, 14:00” |
| 05-truy-cap-bi-chan.jpg | 41 | URL thường trả AccessDenied |
| 06-link-tam-thoi.jpg | 41–42 | GET có chữ ký còn hạn đọc được nội dung |
| 07-link-het-han.jpg | 42 | Request has expired; phép thử dùng 300 giây |
| 08-versioning-enabled.jpg | 37 | Versioning Enabled, Region Sydney |

Ảnh 04 và 06 là cùng một lần GET thành công của bản hiện tại đã khôi phục; không mô tả thành hai phép thử độc lập. Cắt gọn và phóng vùng nội dung/lỗi đủ đọc. Không hiển thị presigned URL, chữ ký URL, thông tin đăng nhập hoặc tài khoản AWS trên slide hay trong ghi chú.

Ba SVG [kiến trúc](assets/so-do-kien-truc.svg), [Versioning](assets/so-do-versioning.svg) và [link tạm thời](assets/so-do-link-tam-thoi.svg) là sơ đồ khái niệm tùy chọn, không phải ảnh kiểm thử.

## 4. Nội dung phải giữ chính xác

- S3 là dịch vụ lưu trữ đối tượng. Demo dùng một general purpose bucket riêng tư, S3 Standard, key gốc ke-hoach-nhom.txt, Block Public Access bật, ACL disabled/Bucket owner enforced và SSE-S3.
- Slide 14: S3 Standard được thiết kế cho độ bền dữ liệu **99.999999999%** và độ sẵn sàng **99.99%** trong một năm. Không đổi lẫn nhãn hoặc áp dụng cho mọi storage class.
- Phục hồi là luồng **v1 → v2 → v3**, với nội dung v1 được lấy từ S3 rồi upload cùng key thành v3. Không xóa v2. Các nhãn v1/v2/v3 là cách gọi trong bài, không phải Version ID thật.
- Presigned URL có thể được dùng nhiều lần khi còn hiệu lực. Bucket vẫn riêng tư; URL có thể hết sớm nếu credentials của người ký hết hạn hoặc bị thu hồi.
- Chỉ ba chức năng trên được trình bày là demo đã chạy. Object Lock, Lifecycle, multipart upload, Athena, sự kiện và replication là kiến thức mở rộng; không thêm kết quả benchmark hoặc triển khai chưa thực hiện.
- Nguồn theo [dàn ý 45 slide](docs/dan-y-45-slide.md) và [tài liệu AWS](docs/nguon-tham-khao.md). Không biến mục tiêu thiết kế thành lời hứa tuyệt đối.

## 5. Bộ cũ chỉ dùng để tham khảo

[Dàn ý 30 slide](docs/dan-y-30-slide.md), [canva-noi-dung.txt](canva-noi-dung.txt), [DAN-VAO-CANVA.txt](DAN-VAO-CANVA.txt) và [bo-canva-s3.zip](bo-canva-s3.zip) thuộc bộ chuẩn bị trước đó. Giữ chúng làm tài liệu tham khảo; không dùng số trang hoặc thời lượng của bộ cũ cho bản chính 45 slide. ZIP cũ là gói giải nén trên máy, không phải bản trình chiếu mới để nhập vào Canva.
