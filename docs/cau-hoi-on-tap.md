# Câu hỏi ôn tập cho demo Amazon S3

Hãy tự trả lời bằng lời của mình rồi mới xem đáp án gợi ý. Mục tiêu là giải thích được ba chức năng của “Kho tài liệu nhóm”, thao tác đang gửi yêu cầu gì và vì sao nhận kết quả đó.

## 1. S3, bucket, object và key là gì?

**S3** là dịch vụ lưu trữ object do AWS quản lý. **Bucket** chứa object. **Object** gồm dữ liệu và metadata; **key** xác định object trong bucket, ví dụ `ke-hoach-nhom.txt`. Trong bucket bật Versioning, Version ID phân biệt các phiên bản có cùng key. [AWS: bắt đầu với S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/GetStartedWithS3.html)

**Tự kiểm tra:** chỉ vào bucket và key thật trong màn hình demo; không đọc thuộc định nghĩa mà không nhận ra chúng.

## 2. Không viết web thì “sản phẩm” của nhóm nằm ở đâu?

Sản phẩm là kho tài liệu có dữ liệu mẫu, cấu hình bảo mật, lịch sử phiên bản và cách chia sẻ có hạn; nhóm chứng minh nó giải quyết một bài toán cụ thể. Console là giao diện có sẵn để quản trị và gọi API S3. Dùng console giúp tập trung học S3 trong phạm vi ba chức năng này. Muốn có giao diện riêng sau này có thể xây thêm ứng dụng gọi cùng các API. [AWS: console và API S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingBucket.html)

**Tự kiểm tra:** nói được bài toán trước khi kể tên nút trên giao diện.

## 3. Upload hai file cùng tên có tạo hai object khác tên không?

Nếu upload vào cùng vị trí để có **cùng key**, Versioning Enabled sẽ tạo phiên bản mới; phiên bản mới là current, bản trước thành noncurrent. Nếu vô tình upload vào prefix `v2/` hoặc đổi thành `ke-hoach-nhom (1).txt`, đó là key khác, không minh họa việc ghi cùng key. [AWS: upload object](https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html)

**Tự kiểm tra:** giải thích vì sao thư mục `samples/v1` và `samples/v2` trên máy chỉ dùng để giữ hai file cùng tên, còn khi upload phải chọn từng file.

## 4. Nhóm đã khôi phục bản cũ như thế nào? Có xóa bản bị sửa nhầm không?

Nhóm chọn Version ID của bản đầu, tải về, kiểm tra nội dung, rồi upload lại đúng key. Kết quả là một phiên bản mới có nội dung cũ; cả bản đầu và bản sửa nhầm vẫn còn. Đây là một quy trình khôi phục bằng thao tác đọc rồi ghi mới. Không cần xóa bất kỳ version nào. [AWS: khôi phục phiên bản trước](https://docs.aws.amazon.com/AmazonS3/latest/userguide/RestoringPreviousVersions.html)

**Tự kiểm tra:** nếu chạy sạch một lần, giải thích nội dung của ba phiên bản theo thứ tự: bản đầu → bản sửa → bản phục hồi.

## 5. Versioning có thay thế hoàn toàn backup không? Có tốn thêm tiền không?

Versioning giúp xử lý ghi đè hoặc xóa nhầm, nhưng người có quyền xóa version vẫn có thể xóa vĩnh viễn; nó không tự tạo bản sao độc lập ở tài khoản hay Region khác. Mỗi version là một bản đầy đủ, không chỉ phần chênh lệch, nên nhiều phiên bản làm tăng dung lượng tính phí. Nhóm cần giữ đúng quyền và dọn sau bài học. [AWS: Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)

**Tự kiểm tra:** bật Versioning không đồng nghĩa miễn phí hoặc bất khả xóa.

## 6. Vì sao Object URL thông thường bị 403 nhưng nút Download vẫn tải được?

Bucket demo là private. GET ẩn danh bằng Object URL thông thường không có quyền nên dự kiến nhận 403 AccessDenied. Người dùng console đã đăng nhập có quyền đọc nên Download có thể thành công. URL chỉ cho biết vị trí; việc biết vị trí không tự cấp quyền truy cập. Nếu Download trong console cũng lỗi thì phải kiểm tra quyền của phiên đăng nhập. [AWS: xử lý 403](https://docs.aws.amazon.com/AmazonS3/latest/userguide/troubleshoot-403-errors.html)

**Tự kiểm tra:** dùng cửa sổ ẩn danh và URL thường cho phép thử private; không dựa vào nút Open của console.

## 7. Presigned URL hoạt động ra sao, và ai có thể dùng nó?

Đó là yêu cầu đã ký để truy cập một object trong khoảng thời gian cho phép. Người tạo cần quyền phù hợp; người nhận giữ URL có thể tải mà không cần đăng nhập AWS. URL tải trong demo không cấp quyền liệt kê cả bucket hoặc upload tài liệu. Bucket vẫn private, Block Public Access vẫn bật. Phải giữ kín liên kết như một quyền truy cập tạm thời. [AWS: chia sẻ object bằng presigned URL](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html)

**Tự kiểm tra:** vì sao không commit URL thật lên GitHub dù hạn chỉ một phút?

## 8. Tại sao link một phút có thể chết sớm hoặc file vẫn xem được sau một phút?

Link có thể hết hiệu lực sớm nếu credentials tạm thời dùng để ký hết hạn hoặc bị thu hồi. Console cho chọn từ một phút đến 12 giờ, nhưng không bảo đảm phiên đăng nhập tồn tại tới cuối hạn đã chọn. Hết hạn chặn yêu cầu mới; không xóa file đã tải, và một lượt tải bắt đầu trước hạn có thể tiếp tục. Cần thử bằng yêu cầu mới sau hạn, tránh nhầm với cache. [AWS: thời hạn presigned URL](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html)

**Tự kiểm tra:** giải thích được vì sao không chỉ nhấn Back để kết luận link còn hiệu lực.

## 9. SSE-S3 và Block Public Access giải quyết hai việc gì khác nhau?

SSE-S3 mã hóa dữ liệu khi lưu; S3 quản lý khóa và giải mã khi xử lý yêu cầu đọc hợp lệ. Block Public Access chặn các cách cấp quyền công khai. ACL disabled/Bucket owner enforced giúp quản lý quyền qua policy. Do đó, file được mã hóa vẫn có thể tải được khi có quyền hợp lệ, như qua presigned URL. [AWS: SSE-S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/serv-side-encryption.html), [AWS: Object Ownership](https://docs.aws.amazon.com/AmazonS3/latest/userguide/about-object-ownership.html)

**Tự kiểm tra:** không nói “bật mã hóa nên không cần quản lý quyền”.

## 10. Chỉ bấm Delete ở danh sách object đã dọn hết và hết phí chưa?

Chưa chắc. Trong bucket bật Versioning, xóa thông thường tạo **delete marker**, còn các version dữ liệu vẫn tồn tại. Delete marker làm object trông như bị xóa ở lượt đọc thông thường; nó không chứa nội dung file. Muốn dọn hoàn toàn bucket demo, cần xóa mọi version và delete marker bằng quy trình Empty rồi mới Delete bucket, sau khi lưu đủ bằng chứng. Đây là xóa vĩnh viễn. [AWS: delete marker](https://docs.aws.amazon.com/AmazonS3/latest/userguide/DeleteMarker.html), [AWS: empty bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/empty-bucket.html)

Chi phí đã phát sinh trước đó vẫn được tính; kiểm tra Billing sau khi dữ liệu cập nhật. Bài demo không có tác vụ tự động xóa tài nguyên. [AWS: S3 Pricing](https://aws.amazon.com/s3/pricing/)

**Tự kiểm tra:** mở Show versions và phân biệt version chứa dữ liệu với delete marker; không thử xóa dữ liệu thật để ôn bài.

## Bài tập nói trong một phút

Không nhìn tài liệu, giải thích liền mạch:

> “Nhóm em dùng một bucket private để lưu kế hoạch. Em upload và tải lại tài liệu để kiểm tra. Khi ghi bản sai cùng key, S3 giữ version cũ. Em lấy nội dung cũ rồi upload lại để tạo bản hiện tại đã phục hồi. Cuối cùng, em dùng URL đã ký để cho người khác tải trong thời gian ngắn, trong khi bucket vẫn chặn public. Các version vẫn tính dung lượng nên nhóm sẽ dọn tài nguyên sau khi chấm.”

Nếu còn phần nào không chỉ ra được trên console, luyện lại đúng thao tác tương ứng trong [hướng dẫn demo](demo-aws-console.md). Các đáp án là nội dung ôn tập; chưa chứng minh bài demo đã chạy thành công trên AWS.

Nguồn AWS được đối chiếu ngày 28/10/2026.
