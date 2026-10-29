# Bản gốc Canva và tài liệu demo

Bản trình chiếu chính là **bản gốc Canva**: [slides/Amazon-S3-ban-goc-Canva.pptx](slides/Amazon-S3-ban-goc-Canva.pptx). Tệp PowerPoint được xuất từ nguồn Canva gốc, giữ nội dung và thiết kế của bản gốc.

Xem trực tuyến: **[Bản gốc trên Canva](https://canva.link/67bxz0ua9w88aoh)**.

Repository [st4rlight3/amazon-s3-kho-tai-lieu-demo](https://github.com/st4rlight3/amazon-s3-kho-tai-lieu-demo) hiện **public**, mở được không cần đăng nhập GitHub. Bucket S3 của demo vẫn riêng tư.

## 1. Mở bản trình chiếu

- Mở liên kết Canva ở trên để xem bản gốc.
- Tải tệp PowerPoint để lưu trên máy hoặc trình chiếu.
- Tài liệu AWS, dữ liệu mẫu và ảnh demo trong repository phục vụ phần thực hành. Chúng không thay thế hoặc sửa nội dung của bản gốc Canva.
- Tập toàn bài cùng thao tác demo để căn thời gian thực tế.

## 2. Ba chức năng demo AWS Console

| Chức năng | Thao tác |
| --- | --- |
| Upload và download | Upload V1 rồi tải lại để kiểm tra nội dung |
| Khôi phục bằng Versioning | Upload V2 cùng key, lấy lại V1 từ S3 rồi upload thành V3 |
| Chia sẻ có thời hạn | URL thường bị chặn; presigned URL còn hạn đọc được; request mới sau hạn bị từ chối |

Dùng một general purpose bucket riêng tư, S3 Standard, key gốc ke-hoach-nhom.txt, Block Public Access bật, ACL disabled/Bucket owner enforced và SSE-S3. Tạo bucket và bật Versioning từ trước buổi học; khi bật Versioning lần đầu, làm theo thời gian chờ trong [hướng dẫn demo](docs/demo-aws-console.md).

Lần kiểm thử thực tế dùng **5 phút (300 giây)**. Phần live có thể chọn **1 phút** để giảm thời gian chờ. Khi giải thích ảnh hết hạn, phân biệt thời hạn ảnh kiểm thử với thời hạn đang demo. Gửi request mới sau hạn; file đã tải không tự biến mất khi URL hết hiệu lực.

Phục hồi là luồng v1 → v2 → v3: nội dung v1 được lấy từ S3 rồi upload cùng key thành v3. Không xóa v2. Các nhãn v1/v2/v3 là cách gọi trong bài, không phải Version ID thật. Presigned URL có thể dùng nhiều lần khi còn hiệu lực và có thể hết sớm nếu credentials của người ký hết hạn hoặc bị thu hồi.

## 3. Ảnh và kết quả demo

Tám ảnh trong [assets/demo](assets/demo/README.md) được chụp từ AWS S3 thật. [Báo cáo demo](docs/ket-qua-demo.md) ghi kết quả kiểm chứng. Bảng dưới mô tả nội dung ảnh, không gán số trang của bản Canva gốc.

| Tệp trong assets/demo/ | Nội dung |
| --- | --- |
| 01-bucket-rieng-tu.jpg | Block Public Access bật; bucket vẫn riêng tư |
| 02-upload-thanh-cong.jpg | Upload thành công vào bucket demo |
| 03-cac-phien-ban.jpg | Ba versions của cùng key |
| 04-khoi-phuc-v1.jpg | Nội dung đã phục hồi có lịch “Thu Sau, 14:00” |
| 05-truy-cap-bi-chan.jpg | URL thường trả AccessDenied |
| 06-link-tam-thoi.jpg | GET có chữ ký còn hạn đọc được nội dung |
| 07-link-het-han.jpg | Request has expired; phép thử dùng 300 giây |
| 08-versioning-enabled.jpg | Versioning Enabled, Region Sydney |

Ảnh 04 và 06 là cùng một lần GET thành công của bản hiện tại đã khôi phục, không phải hai phép thử độc lập. Không đưa presigned URL, chữ ký URL, thông tin đăng nhập hoặc tài khoản AWS vào tài liệu công khai.

Ba SVG [kiến trúc](assets/so-do-kien-truc.svg), [Versioning](assets/so-do-versioning.svg) và [link tạm thời](assets/so-do-link-tam-thoi.svg) là sơ đồ khái niệm, không phải ảnh kiểm thử. Tra cứu thêm trong [nguồn AWS](docs/nguon-tham-khao.md) và [câu hỏi ôn tập](docs/cau-hoi-on-tap.md).

## 4. Bộ dàn ý 30 slide chỉ để tham khảo

[Dàn ý 30 slide](docs/dan-y-30-slide.md), [canva-noi-dung.txt](canva-noi-dung.txt), [DAN-VAO-CANVA.txt](DAN-VAO-CANVA.txt) và [bo-canva-s3.zip](bo-canva-s3.zip) thuộc bộ chuẩn bị trước đó. Các số trang và thời lượng trong bộ này không áp dụng cho bản Canva gốc. ZIP là gói tài liệu để giải nén, không phải bản trình chiếu chính.
