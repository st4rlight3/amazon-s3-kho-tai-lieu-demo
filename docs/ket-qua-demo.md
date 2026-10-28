# Kết quả demo Amazon S3 thực tế

Ngày thực hiện: **28/10/2026**, múi giờ Việt Nam (UTC+07:00).

Bucket dùng cho sản phẩm: **cloudnotes-starlight**. Region: **Asia Pacific (Sydney), ap-southeast-2**. General purpose bucket, global namespace, dữ liệu giả lập. Demo chạy trên AWS S3 thật qua Console.

**Kết luận:** cả ba chức năng đã chạy và được kiểm chứng trên S3. Đã lưu tám ảnh demo thật.

## Kết quả quan sát

| Hạng mục | Kết quả |
| --- | --- |
| Bucket riêng tư, Block all public access | Đạt: On, không mở public |
| Object Ownership | Đạt: Bucket owner enforced, ACLs disabled |
| Mã hóa | Đạt: SSE-S3, không tạo khóa KMS |
| Versioning | Đạt: Enabled |
| Upload V1 | Đạt: 305 byte, S3 Standard, Upload succeeded |
| Download V1 | Đạt: file tải xuống có lịch Thu Sau, 14:00, khớp file mẫu |
| Upload V2 cùng key | Đạt: phiên bản mới 312 byte, V1 trở thành noncurrent |
| Đọc V1 bằng version ID | Đạt: nội dung lấy lại từ S3 khớp nguyên vẹn 305 ký tự của bản gốc |
| Ghi bản khôi phục cùng key | Đạt: tạo V3 305 byte, cả V1 và V2 vẫn còn |
| Đọc bản hiện tại sau khôi phục | Đạt: GET bản hiện tại khớp hoàn toàn nội dung V1 |
| URL thường không có chữ ký | Đạt: S3 trả AccessDenied |
| Presigned URL còn hạn | Đạt: liên kết GET 300 giây đọc được nội dung hiện tại |
| Cùng presigned URL sau khi hết hạn | Đạt: AccessDenied, Request has expired |

## Lịch sử phiên bản đã kiểm tra

Cùng bucket và cùng key `ke-hoach-nhom.txt`.

| Cách gọi trong bài | Version ID do S3 tạo | Giờ tạo tại Việt Nam | Dung lượng | Vai trò |
| --- | --- | --- | --- | --- |
| V1 | `eNJSiw2vvWIeQ_F6rdmioIqBoW4lYmZl` | 23:28:08 | 305 byte | Bản đúng ban đầu, noncurrent |
| V2 | `x19B8Dn_k_cwppAXl6t0eRTrJ6ueqC1f` | 23:33:39 | 312 byte | Bản cố ý sửa sai, noncurrent |
| V3 | `cbwdxB6krHDDW25UXJFauUlNAsdiq.Jy` | 23:45:03 | 305 byte | Bản hiện tại, chứa nội dung V1 |

S3 không đặt version ID thành V1/V2/V3; đó là tên gọi để thuyết trình. Bản khôi phục là một lần ghi mới. Không xóa bất kỳ phiên bản nào trong phần kiểm thử.

Lượt tải riêng phiên bản cũ qua trình duyệt điều khiển có lúc chậm và không hoàn tất qua nút Download. Để kiểm chứng dữ liệu, đã đọc chính phiên bản V1 bằng URL ký có `versionId`, lưu nguyên nội dung đã đọc rồi upload lại cùng key. Nội dung lấy từ S3 khớp bản gốc; lượt GET bản hiện tại sau khi ghi V3 cũng khớp. Hướng dẫn thực hành dùng Download phiên bản cũ; nên tập thao tác này trên trình duyệt sẽ dùng trong buổi học.

## Phép thử quyền và thời hạn

- Bucket giữ private và Block Public Access bật suốt phần demo.
- GET không có chữ ký vào object trả `AccessDenied`.
- Presigned URL kiểm thử ký lúc **23:47:40**, thời hạn **300 giây**, nhắm bản hiện tại và không chỉ định version ID.
- Trước hạn: đọc được dữ liệu, nội dung khớp V1 sau khi đã phục hồi thành V3.
- Sau hạn: gửi GET mới bằng **chính liên kết đã kiểm tra trước đó**, S3 trả `AccessDenied` và `Request has expired`. Phản hồi ghi giờ hết hạn `16:52:40Z` và giờ máy chủ `16:54:24Z` (tương ứng 23:52:40 và 23:54:24 tại Việt Nam).
- Liên kết dùng dữ liệu mẫu và không được đưa vào repository, ảnh hoặc slide. Ảnh chỉ ghi lại phần nội dung trang, không có thanh địa chỉ.

Kịch bản thuyết trình có thể dùng link một phút khi nhóm đã luyện thao tác. Lần kiểm thử tự động chọn năm phút để có thời gian kiểm tra trước và sau hạn.

## Bằng chứng ảnh

Xem [danh mục ảnh](../assets/demo/README.md). Các ảnh 04 và 06 ghi lại cùng một trạng thái: GET có chữ ký đọc bản hiện tại đã khôi phục. Dùng ảnh 04 để nói về nội dung phục hồi, ảnh 06 để đối chiếu quyền truy cập; không phải hai phép thử độc lập.

Ảnh được chụp trực tiếp từ trang AWS và phản hồi S3. Ba sơ đồ SVG là hình giải thích khái niệm, không phải ảnh Console.

## Trạng thái tài nguyên sau kiểm thử

Bucket `cloudnotes-starlight` giữ lại để nhóm luyện và trình diễn, có một key với ba phiên bản. Chưa chạy dọn dữ liệu hoặc xóa bucket. Versioning vẫn tính dung lượng các phiên bản; làm theo phần dọn tài nguyên của README sau khi chấm.

Bucket tên dài tạo ban đầu đã được thay thế trong phạm vi demo bằng `cloudnotes-starlight`; bucket ban đầu vẫn rỗng và không được dùng trong bài. Không xóa tài nguyên nào có sẵn của người dùng.