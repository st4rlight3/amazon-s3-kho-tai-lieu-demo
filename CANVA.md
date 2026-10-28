# Bàn giao nội dung cho Canva Pro

Dùng [canva-noi-dung.txt](canva-noi-dung.txt) để đưa đúng phần chữ ngắn lên 30 slide. [Dàn ý đầy đủ](docs/dan-y-30-slide.md) có lời thuyết trình, thời lượng, gợi ý hình và nguồn của từng trang; phần lời nói đặt trong ghi chú thuyết trình, không dồn lên mặt slide.

Thời lượng mục tiêu là **35 phút 30 giây**, đã gồm **7 phút 30 giây demo trực tiếp**. Các trang 27–29 dẫn vào thao tác trên AWS Console; trình chiếu không thay thế phần demo thật.

Repository dự kiến để gắn vào slide 30 sau khi xác nhận push thành công: [st4rlight3/amazon-s3-kho-tai-lieu-demo](https://github.com/st4rlight3/amazon-s3-kho-tai-lieu-demo). Có thể tạo QR cho địa chỉ repository này sau khi kiểm tra truy cập được; không tạo QR cho presigned URL.

## 1. Nội dung nhập cho Canva

Sao chép phần yêu cầu dưới đây, rồi dán toàn bộ nội dung trong `canva-noi-dung.txt` ngay sau yêu cầu. Nếu công cụ tạo chưa đủ 30 trang, giữ nguyên danh sách nội dung và bổ sung các trang còn thiếu theo đúng số thứ tự, không yêu cầu công cụ tự nghĩ thêm ý.

```text
Tạo bộ thuyết trình TIẾNG VIỆT, đúng 30 slide, tỷ lệ 16:9, chủ đề Amazon S3. Đối tượng là sinh viên và giảng viên. Nội dung để trình bày trong 30–40 phút, với phần demo AWS Console ở cuối.

Nguồn nội dung duy nhất là danh sách 30 slide được dán sau yêu cầu này. Giữ đúng thứ tự, tiêu đề và các ý; không tự thêm số liệu, ví dụ sản phẩm, chức năng hoặc lời hứa của AWS. Không gộp hoặc tách slide. Các chỗ [điền tên] và [điền lớp] để nhóm tự cập nhật.

Thiết kế dễ đọc khi chiếu trong lớp: nền trắng ngà hoặc xanh navy, chữ tương phản cao, màu cam làm điểm nhấn. Gợi ý bảng màu: navy #14213D, trắng #FAFBFD, cam #F59E0B. Dùng một font sans serif có đủ dấu tiếng Việt. Tiêu đề khoảng 32–44 pt, nội dung 24–28 pt; chỉ dùng cỡ nhỏ hơn cho nguồn ở chân trang. Tiêu đề dài được xuống hai dòng, không thu nhỏ chữ quá mức.

Mỗi trang tập trung vào một thông điệp và một hình chính. Ưu tiên sơ đồ đơn giản, bảng ngắn, timeline hoặc thẻ thông tin; tránh đoạn văn dài và hình trang trí lấn chữ. Căn lề, số trang và vị trí nguồn thống nhất. Dùng hiệu ứng xuất hiện nhẹ, không cần âm thanh hay chuyển cảnh phức tạp.

Phân biệt durability là độ bền dữ liệu với availability là độ sẵn sàng. Với S3 Standard, giữ đúng số 99.999999999% và 99.99%, tương ứng; ghi là “được thiết kế cho”, không chuyển thành bảo đảm tuyệt đối. Không áp hai số này cho mọi storage class.

Demo có đúng ba chức năng: upload/download, khôi phục nội dung bằng Versioning, chia sẻ qua presigned URL. Phạm vi là một general purpose bucket riêng tư, S3 Standard, Block Public Access bật, ACL disabled/Bucket owner enforced và SSE-S3. Không thêm ứng dụng web, mã HTML/Python, website hosting, IAM access key hoặc một bucket công khai.

Khi minh họa khôi phục, dùng dòng v1 → v2 → v3, với nội dung v1 được tải về rồi upload lại thành v3 cùng key. Đừng vẽ thao tác xóa v2. v1/v2/v3 là cách gọi trong bài, không phải định dạng Version ID thật của AWS.

Ảnh demo sẽ do nhóm tải lên từ repo và gán đúng trang theo bảng ảnh kèm theo. Chỉ dùng ảnh thực có; không tạo ảnh giả giao diện AWS để làm bằng chứng. Không hiển thị presigned URL thật, chữ ký URL, thông tin đăng nhập hay tài khoản AWS. Nếu chưa có ảnh, để ô giữ chỗ ghi rõ “Chèn ảnh demo thật sau khi kiểm tra”.

Đặt lời thuyết trình dài trong ghi chú, không dùng để tăng chữ trên mặt slide. Duy trì các trích dẫn AWS lấy từ dàn ý đầy đủ ở chân trang tương ứng; không tự phát minh nguồn.

DANH SÁCH NỘI DUNG 30 SLIDE:
[Dán toàn bộ canva-noi-dung.txt vào đây]
```

Nếu Canva không tiếp nhận hết nội dung một lượt, nhập theo ba nhóm **01–10, 11–20, 21–30** trong cùng một thiết kế. Dùng lại kiểu chữ, bảng màu và lưới bố cục của nhóm đầu; giữ tổng cộng 30 trang.

## 2. Ảnh thật cần tải lên và vị trí chèn

Tải các ảnh JPG dưới đây từ `assets/demo/` khi chúng thực sự đã được chụp và kiểm tra. Danh mục này mô tả ảnh cần có; xem [báo cáo demo](docs/ket-qua-demo.md) để biết trạng thái chạy thật. Trước khi chia sẻ hoặc tải ảnh lên Canva, che toàn bộ URL đã ký và thông tin tài khoản.

| Tệp trong `assets/demo/` | Slide chính | Cách dùng |
| --- | --- | --- |
| `01-bucket-rieng-tu.jpg` | 17, 26 | Cắt vùng bucket demo và Block Public Access; thêm nhãn “Private” |
| `02-upload-thanh-cong.jpg` | 27 | Làm nổi object `ke-hoach-nhom.txt` đã upload |
| `03-cac-phien-ban.jpg` | 19, 28 | Làm nổi nhiều Version ID của cùng key; nhãn v1/v2/v3 chỉ là tên giải thích |
| `04-khoi-phuc-v1.jpg` | 28 | Cho thấy nội dung bản hiện tại đã có lịch đúng của V1 |
| `05-truy-cap-bi-chan.jpg` | 17, 29 | Trạng thái “Không có quyền” khi dùng URL thường |
| `06-link-tam-thoi.jpg` | 29 | Trạng thái “Được chia sẻ” khi dùng URL còn hạn |
| `07-link-het-han.jpg` | 29 | Trạng thái “Hết hạn” với một yêu cầu mới |

Slide 29 có thể dùng ba ảnh 05–07 theo hàng ngang, mỗi ảnh một trạng thái và một nhãn ngắn. Cắt gọn để chữ lỗi hoặc nội dung tài liệu đọc được; không cần chụp toàn bộ trình duyệt. Slide 08 có thể tái sử dụng ảnh 01 nếu phù hợp, nhưng sơ đồ bucket trong dàn ý đã đủ giải thích khái niệm.

Danh mục gốc: [assets/demo/README.md](assets/demo/README.md). Các đường dẫn trong repo không tự đưa ảnh vào thiết kế; nhóm cần chọn đúng tệp ảnh để tải lên.

## 3. Giữ lời nói, nguồn và demo thống nhất

- Sao chép **Lời thuyết trình** từ dàn ý vào ghi chú của đúng slide. Không dùng phần ghi chú này làm nội dung mặt trang.
- Chọn nguồn AWS từ mục **Nguồn** của từng slide; đặt tên nguồn ngắn kèm liên kết ở chân trang. Nguồn tổng hợp nằm ở [docs/nguon-tham-khao.md](docs/nguon-tham-khao.md).
- Giữ mốc **14/03/2006** là ngày công bố S3; không lấy giá hoặc giới hạn năm 2006 làm thông số hiện tại.
- Với hai chỉ số S3 Standard, lời giải thích đầy đủ là mục tiêu thiết kế **trong một năm**: độ bền dữ liệu `99.999999999%`, độ sẵn sàng `99.99%`. Không đổi lẫn hai nhãn.
- Demo dùng đúng key `ke-hoach-nhom.txt` tại gốc bucket. Hai thư mục mẫu trên máy không trở thành hai prefix trên S3.
- Presigned URL là quyền tạm thời cho người có liên kết; không phải link chỉ dùng một lần. Không đưa URL thật vào chữ, hình, ghi chú hay mã QR.
- Đối chiếu thời gian thao tác với [hướng dẫn demo](docs/demo-aws-console.md); tạo bucket và chờ Versioning trước giờ trình bày, không tính vào thời lượng demo.

## 4. Kiểm tra trước buổi thuyết trình

- [ ] Đúng 30 trang và thứ tự; tên nhóm/lớp đã thay.
- [ ] Không lỗi dấu tiếng Việt, chữ tràn khung hoặc tỷ lệ phần trăm bị đổi.
- [ ] Mọi chữ chính đọc được trên màn chiếu; đồ họa chỉ hỗ trợ một ý mỗi trang.
- [ ] Slide 14 phân biệt đúng hai chỉ số; slide 19 thể hiện bản phục hồi thành version mới.
- [ ] Ảnh thật đã che thông tin; không có URL đã ký hoặc ảnh giả làm bằng chứng.
- [ ] Ghi chú đủ lời nói, nguồn bấm được và khớp trang.
- [ ] Slides 27–29 kết nối đúng ba thao tác live; cửa sổ AWS Console và file mẫu đã mở sẵn.
- [ ] Nhóm đã tập và căn thời gian toàn bài; mỗi thành viên giải thích được các bước demo.

File TXT chỉ chứa tiêu đề và các ý trên slide, được trích nguyên văn từ dàn ý. Khi sửa nội dung dàn ý, cập nhật lại TXT trước khi nhập lại Canva để tránh hai bản khác nhau.
