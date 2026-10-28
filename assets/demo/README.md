# Ảnh demo dành cho Canva

Đã chụp đủ tám ảnh từ demo S3 thật ngày 28/10/2026, dùng bucket `cloudnotes-starlight`. Vùng chụp không có thông tin tài khoản hoặc chữ ký URL. Các ảnh cấu hình dùng khung 1600 × 900; ảnh nội dung/lỗi cắt gọn vùng phản hồi để dễ đọc khi chèn Canva.

| Tên ảnh | Dùng cho slide | Nội dung cần thấy |
| --- | --- | --- |
| `01-bucket-rieng-tu.jpg` | 17, 26 | Bucket demo và Block Public Access |
| `02-upload-thanh-cong.jpg` | 27 | Object ke-hoach-nhom.txt đã upload |
| `03-cac-phien-ban.jpg` | 19, 28 | Nhiều version ID của cùng một key |
| `04-khoi-phuc-v1.jpg` | 28 | Nội dung hiện tại có lịch đúng của V1 |
| `05-truy-cap-bi-chan.jpg` | 17, 29 | Truy cập không có quyền bị từ chối |
| `06-link-tam-thoi.jpg` | 29 | Nội dung truy cập được bằng URL còn hạn |
| `07-link-het-han.jpg` | 29 | URL hết hạn bị từ chối |
| `08-versioning-enabled.jpg` | 19, 26 | Bucket Versioning Enabled và Region Sydney |

Ảnh 04 và 06 ghi lại cùng một lần GET thành công của bản hiện tại đã khôi phục, dùng cho hai phần giải thích. Xem [báo cáo thực tế](../../docs/ket-qua-demo.md) để biết kết quả kiểm tra.

Nếu cần một slide nhiều trạng thái, dùng ba ảnh 05, 06, 07 đặt cạnh nhau và ghi: Không có quyền / Được chia sẻ / Hết hạn. Không đặt presigned URL thật lên slide.
