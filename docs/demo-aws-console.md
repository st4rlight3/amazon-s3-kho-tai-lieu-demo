# Demo Amazon S3: Kho tài liệu nhóm

## Mục tiêu và trạng thái

Nhóm có một bản kế hoạch cần lưu, sửa nhầm và gửi cho thầy. Sản phẩm demo là **một kho tài liệu riêng tư trên Amazon S3**, thao tác bằng AWS Management Console. Không cần viết HTML, Python, Streamlit hay tạo access key.

Demo có đúng ba chức năng:

1. **Lưu và lấy tài liệu:** upload một file, xem thông tin và download lại.
2. **Khôi phục nội dung cũ:** upload bản sửa cùng tên, xem Versioning rồi đưa nội dung cũ thành bản hiện tại.
3. **Chia sẻ có thời hạn:** tạo presigned URL để người không đăng nhập AWS đọc được một tài liệu.

**Trạng thái:** đã thực hiện demo trên AWS ngày 28/10/2026. Xem [kết quả thực tế](ket-qua-demo.md) và ảnh để biết từng phép thử đã xác minh. Các ô tự kiểm ở dưới dành cho lần luyện tập tiếp theo của nhóm.

## 1. Chuẩn bị trước buổi học

### 1.1. Những thứ cần có

- Một tài khoản AWS hoạt động; đăng nhập bằng danh tính IAM/role hoặc phiên đăng nhập do nhà trường cấp có quyền S3 phù hợp. Không dùng root cho bài demo hằng ngày.
- Quyền tạo/cấu hình bucket, liệt kê bucket và phiên bản, upload/download object và tạo liên kết chia sẻ. Tài khoản phòng lab có thể bị giới hạn quyền hoặc thời gian phiên.
- Trình duyệt có cửa sổ ẩn danh, mạng ổn định và hai file mẫu nhỏ, không chứa dữ liệu cá nhân.
- Mở sẵn `samples/v1/ke-hoach-nhom.txt` và `samples/v2/ke-hoach-nhom.txt` để nhận ra nội dung khác nhau. Hai file có **cùng tên** nhưng nằm ở hai thư mục máy tính khác nhau.

Không gửi mật khẩu, mã MFA, access key hoặc URL đã ký lên GitHub. Việc tạo presigned URL dùng quyền của phiên đăng nhập hiện tại; không cần tạo IAM access key cho bài này.

### 1.2. Tạo một bucket riêng cho bài demo

Mở [Amazon S3 Console](https://console.aws.amazon.com/s3/), vào **General purpose buckets → Create bucket**. Dùng một bucket mới chỉ chứa dữ liệu mẫu để tránh nhầm với tài nguyên đang sử dụng.

| Mục | Giá trị chọn | Lý do |
| --- | --- | --- |
| Region | Asia Pacific (Sydney), `ap-southeast-2`, như bucket demo đã tạo | Chọn một vùng và giữ nguyên trong bài |
| Bucket type | General purpose | Phù hợp kho tài liệu thông thường |
| Bucket name | `cloudnotes-starlight`, tên đã chọn cho bài demo | Nếu dùng shared global namespace, tên phải chưa được tài khoản khác dùng trong cùng partition |
| Object Ownership | ACLs disabled / Bucket owner enforced | Quản lý quyền qua policy |
| Block Public Access | **Block all public access: bật**, giữ cả bốn mục bật | Không công khai bucket |
| Bucket Versioning | Enable | Giữ các lần ghi cùng key |
| Default encryption | SSE-S3, Amazon S3 managed keys | Mã hóa dữ liệu khi lưu |
| Object Lock và các tính năng bổ sung | Không bật trong bài này | Giữ phạm vi dễ hiểu |

Tên `cloudnotes-starlight` ngắn và có ý nghĩa với kho tài liệu. Nếu tên đã được dùng khi bạn tái hiện bài, chọn một tên riêng có ý nghĩa và phân biệt được cho nhóm mình; không bắt buộc thêm ngày hoặc chuỗi số ngẫu nhiên. Dùng chữ thường và dấu gạch nối theo quy tắc tên bucket. Nếu console cho chọn namespace, dùng **shared global namespace** để đi theo bài; không dựa vào tên bucket để bảo mật. Sau khi tạo, ghi lại Region và bucket name trong ghi chú cá nhân. [AWS: bucket và namespace](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingBucket.html)

**Kết quả cần thấy:** bucket xuất hiện trong danh sách. Trong **Permissions**, kiểm tra Block Public Access vẫn bật và Object Ownership là Bucket owner enforced. Đây là cấu hình mặc định được AWS khuyến nghị cho bucket mới. [AWS: Object Ownership và Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-ownership-new-bucket.html)

Trong **Properties**, kiểm tra Versioning là Enabled và Default encryption là SSE-S3. SSE-S3 mã hóa object trên phía dịch vụ, còn quyền đọc được quản lý riêng; “được mã hóa” không đồng nghĩa với “không ai tải được”. [AWS: mã hóa phía máy chủ](https://docs.aws.amazon.com/AmazonS3/latest/userguide/serv-side-encryption.html)

**Làm bước này trước giờ thuyết trình:** lần đầu bật Versioning, AWS khuyến nghị chờ **15 phút trước khi ghi hoặc xóa object** để thay đổi truyền đầy đủ. Thời gian chuẩn bị này không tính vào phần trình diễn 7–8 phút. [AWS: bật Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/manage-versioning-examples.html)

## 2. Thực hành ba chức năng

### Chức năng 1 — Upload và download tài liệu

1. Mở bucket → **Objects → Upload → Add files**.
2. Chọn riêng file `samples/v1/ke-hoach-nhom.txt`; không kéo cả thư mục `v1` lên.
3. Kiểm tra tên đích là `ke-hoach-nhom.txt`, storage class là **S3 Standard**, giữ quyền riêng tư và SSE-S3 → **Upload**.
4. Khi báo thành công, chọn **Close** để trở về danh sách object.
5. Mở object, chỉ vào **Key**, dung lượng và thời gian cập nhật. Key cần đúng là `ke-hoach-nhom.txt`, không có `v1/` phía trước.
6. Chọn **Download**, mở file đã tải bằng trình soạn thảo văn bản và đối chiếu nội dung bản 1.

**Kết quả:** file tải về có đúng nội dung ban đầu. Một file được upload trở thành object; key là tên định danh của object trong bucket. Console gọi API S3 thay cho việc ta viết mã. [AWS: upload object](https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html), [AWS: tải object](https://docs.aws.amazon.com/AmazonS3/latest/userguide/download-objects.html)

**Câu nói khi trình bày:** “Bucket là nơi chứa. Trong bucket này, `ke-hoach-nhom.txt` là key. Dữ liệu và thông tin mô tả tạo thành object. Em dùng console để yêu cầu S3 lưu và lấy tài liệu.”

### Chức năng 2 — Sửa nhầm và khôi phục bằng Versioning

1. Trở về **Objects → Upload**, chọn file `samples/v2/ke-hoach-nhom.txt` và upload vào **cùng vị trí gốc bucket**.
2. Download bản hiện tại và mở ra để chứng minh nội dung đã thành bản 2.
3. Mở object → **Versions**, hoặc bật **Show versions** trong danh sách. Xác định hai Version ID khác nhau của cùng key, dựa thêm vào thời điểm upload.
4. Chọn **đúng phiên bản đầu tiên** → **Download** hoặc **Actions → Download**, tùy vị trí đang mở. Lưu vào một thư mục riêng trên máy và mở kiểm tra rằng đó là nội dung bản 1.
5. Nếu trình duyệt đổi tên thành `ke-hoach-nhom (1).txt`, đổi tên cục bộ về chính xác `ke-hoach-nhom.txt` trong thư mục riêng đó.
6. Trở về **Objects → Upload**, chọn file bản cũ vừa tải và upload vào gốc bucket, cùng key `ke-hoach-nhom.txt`.
7. Download bản hiện tại một lần nữa. Kiểm tra nội dung bản 1 đã trở lại; mở **Versions** để thấy **ba phiên bản** nếu đây là lần chạy đầu tiên.

**Kết quả:** bản 3 có nội dung giống bản 1 và là bản hiện tại; bản 1 và bản 2 vẫn được giữ. Khôi phục ở đây là một lần ghi mới, không phải quay lùi đồng hồ hay xóa lịch sử. Mỗi version lưu toàn bộ object, nên các bản cũ vẫn chiếm dung lượng. [AWS: S3 Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)

**Vì sao dùng cách này?** Tải bản cũ rồi upload lại là cách dễ theo dõi trên console và không cần xóa phiên bản nào. AWS cũng hỗ trợ sao chép một version cũ trở lại cùng key bằng CLI/SDK; thao tác copy in-place đó không có trên console. Bài demo này không dùng cách xóa bản mới để lộ bản cũ. [AWS: khôi phục phiên bản](https://docs.aws.amazon.com/AmazonS3/latest/userguide/RestoringPreviousVersions.html)

**Câu nói khi trình bày:** “Lần sửa nhầm không làm mất bản gốc vì Versioning đã bật trước khi upload. Em tải đúng bản cũ và ghi lại cùng key. S3 tạo version mới có nội dung đã phục hồi.”

### Chức năng 3 — Chia sẻ tài liệu bằng presigned URL

1. Trong thông tin object, sao chép **Object URL thông thường**. Mở URL đó trong cửa sổ ẩn danh, không đăng nhập AWS.
2. Với cấu hình private của bài này, truy cập GET ẩn danh dự kiến bị từ chối **403 AccessDenied**. Đây là phép thử quyền, không phải bằng chứng upload lỗi. Không dùng nút **Open** của console cho phép thử này vì nó có thể tạo yêu cầu có xác thực. [AWS: lỗi 403](https://docs.aws.amazon.com/AmazonS3/latest/userguide/troubleshoot-403-errors.html)
3. Quay lại **Objects**, chọn object → **Object actions/Actions → Share with a presigned URL**.
4. Chọn **1 phút** → **Create presigned URL** → sao chép liên kết.
5. Mở liên kết trong cửa sổ ẩn danh; tài liệu phải hiển thị hoặc được tải về tùy trình duyệt. Người nhận không cần tài khoản AWS. [AWS: tạo liên kết trên console](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html)
6. Ghi lại thời điểm tạo trong ghi chú riêng. Sau hơn 1 phút, tạo **một yêu cầu tải mới** bằng cách dán lại URL vào tab ẩn danh mới; dự kiến bị từ chối. Một file đã tải hoặc nội dung đã nằm trong bộ nhớ đệm vẫn có thể xem được.

Console cho chọn hạn từ **1 phút đến 12 giờ**. URL có thể hết hiệu lực sớm hơn nếu thông tin xác thực tạm thời của người tạo hết hạn hoặc bị thu hồi. S3 kiểm tra hạn lúc bắt đầu yêu cầu; một lượt tải đã bắt đầu trước hạn có thể tiếp tục. [AWS: hạn presigned URL](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html)

**Kết quả:** cùng object vẫn private, nhưng URL đã ký cho phép tải trong thời hạn hợp lệ. **Ai có URL có thể sử dụng nó trong phạm vi quyền đã ký**; coi toàn bộ liên kết là bí mật tạm thời. Không đưa URL vào README, commit, issue, slide hay ảnh chụp màn hình; chỉ lưu kết quả kiểm tra đã che liên kết. Link hết hạn không thu hồi được bản người nhận đã tải.

**Câu nói khi trình bày:** “Em không bật public bucket. Presigned URL cho người cầm liên kết quyền tải tạm thời, dựa trên quyền của người ký. Sau khi hết hạn, yêu cầu mới bằng liên kết này bị từ chối.”

## 3. Kịch bản trình diễn cuối bài — khoảng 8 phút

Phần này nối tiếp 26 slide lý thuyết/phạm vi trong bài thuyết trình 30 slide, 30–40 phút: slide 27 hướng dẫn upload/download, slide 28 Versioning, slide 29 chia sẻ có thời hạn, slide 30 kết luận. Phần tạo bucket và chờ Versioning phải làm xong từ trước. Đăng nhập console sẵn, chuẩn bị cửa sổ ẩn danh và các file mẫu. Khi demo, chỉ giải thích điều đang thao tác.

Dàn ý dành **7 phút 30 giây cho ba chức năng trên slides 27–29**; lịch khoảng 8 phút dưới đây làm tròn và gồm lời dẫn/chuyển sang slide kết luận. Khi tập cả bài 35 phút 30 giây, bám nhịp của từng slide trong dàn ý và tránh tính hai lần phần kết luận.

| Thời gian | Thao tác | Điều phải giải thích |
| --- | --- | --- |
| 00:00–00:20 | Slide 27: giới thiệu bài toán, chỉ vào bucket | Nhóm cần lưu kế hoạch, phục hồi khi sửa nhầm và chia sẻ tạm thời |
| 00:20–02:00 | Upload bản 1, chỉ thông tin và download mở nội dung | Bucket, object và key là gì; dữ liệu thực sự nằm ở S3 |
| 02:00–03:00 | Slide 28: upload bản 2 cùng key; download và mở nội dung | Cùng key tạo version mới vì đã bật Versioning |
| 03:00–04:20 | Tải bản 1 từ Versions và upload lại cùng key | Bản hiện tại khôi phục nội dung, lịch sử vẫn còn |
| 04:20–05:00 | Mở Versions; tải bản hiện tại kiểm chứng | Ba Version ID; bản mới nhất có nội dung bản đầu |
| 05:00–05:40 | Slide 29: thử Object URL ẩn danh, tạo link 1 phút | URL thường bị từ chối; ghi lại giờ tạo URL đã ký |
| 05:40–06:00 | Tải bằng URL đã ký ở cửa sổ ẩn danh | Người nhận không cần tài khoản AWS; quyền được cấp qua link |
| 06:00–07:10 | Chỉ vào BPA/SSE-S3; giải thích người cầm link và hạn phiên | Bucket vẫn private; mã hóa và phân quyền giải quyết hai việc khác nhau |
| 07:10–07:45 | Gửi yêu cầu mới bằng link 1 phút đã hết hạn | Yêu cầu mới bị từ chối; file đã tải vẫn tồn tại trên máy |
| 07:45–08:00 | Chuyển slide 30 và kết luận demo | Ba chức năng đã chứng minh; sẽ dọn tài nguyên sau khi chấm |

Để phép thử hết hạn nhất quán, ghi lại lúc tạo link và chỉ thử yêu cầu mới sau hơn một phút. Tạo link sau khi phục hồi xong, giữ nguyên object trong phần chia sẻ. Nếu thao tác nhanh hơn lịch, giải thích quyền truy cập và các điểm an toàn trước khi thử lại. Không dùng việc ghi phiên bản mới như một cách thu hồi link.

Nếu thực hiện lại nhiều lần, tổng số versions có thể lớn hơn ba. Muốn có buổi demo sạch, dùng một bucket demo mới đã chuẩn bị trước; không xóa vội dữ liệu đang dùng ngay giữa buổi.

## 4. Phiếu tự kiểm tra và bằng chứng

Các ô dưới đây để trống cho tới khi chạy thật. Trong báo cáo ghi ngày, Region, kết quả và tên ảnh đã che thông tin nhạy cảm.

- [ ] Cấu hình: General purpose; BPA cả bốn mục bật; ACL disabled; Versioning Enabled; SSE-S3.
- [ ] Upload/download: tải lại đúng nội dung bản 1, object dùng S3 Standard.
- [ ] Versioning: bản 2 khác bản 1; upload lại bản cũ tạo version mới; bản hiện tại khớp bản 1.
- [ ] Object URL thường: GET ẩn danh bị từ chối 403.
- [ ] Presigned URL: tải ẩn danh trước hạn thành công; yêu cầu mới sau hạn bị từ chối.
- [ ] Ảnh và báo cáo không chứa liên kết đã ký, thông tin đăng nhập hoặc dữ liệu cá nhân.

Ảnh nên có: danh sách object sau upload; danh sách Version ID; nội dung bản 2 và bản được phục hồi; lỗi URL thường; kết quả tải bằng link hợp lệ và lỗi sau hạn. Che thanh địa chỉ chứa presigned URL trước khi đưa ảnh vào GitHub hoặc Canva.

## 5. Xử lý tình huống thường gặp

| Hiện tượng | Kiểm tra và cách xử lý |
| --- | --- |
| Không tạo được bucket | Tên có thể đã được dùng; đổi chuỗi cuối. Kiểm tra quyền tài khoản hoặc hạn chế phòng lab |
| Không thấy nhiều versions | Kiểm tra Versioning đã bật trước upload; bật Show versions/Versions; bảo đảm cùng key, không upload thành `v2/ke-hoach-nhom.txt` |
| Bản khôi phục thành file mới | Tên tải về có thể có `(1)` hoặc khác chữ hoa/thường; sửa tên cục bộ và upload lại đúng key |
| 404 ngay sau bật Versioning lần đầu | Làm theo thời gian chờ 15 phút của AWS rồi thử lại |
| Download trong console bị AccessDenied | Danh tính đang đăng nhập có thể thiếu quyền đọc. Nhờ người quản lý tài khoản cấp quyền cần thiết; không tắt Block Public Access |
| URL đã ký lỗi ngay | Sao chép đầy đủ URL, tạo lại bằng phiên còn hạn và kiểm tra quyền đọc. Đừng đưa URL vào công cụ công khai để phân tích |
| Link “hết hạn” mà vẫn thấy nội dung | Có thể đang xem file đã tải hoặc cache; tạo yêu cầu mới ở tab ẩn danh mới sau thời hạn |

## 6. Chi phí và dọn tài nguyên sau khi chấm

Dữ liệu mẫu nhỏ giúp hạn chế chi phí, nhưng **không cam kết hóa đơn bằng 0**. Chi phí phụ thuộc dung lượng/thời gian lưu, số yêu cầu và dữ liệu truyền ra; xem Region và ưu đãi thực tế của tài khoản trên [AWS S3 Pricing](https://aws.amazon.com/s3/pricing/). Ngân sách cảnh báo không phải cơ chế tự ngắt chi tiêu.

Chỉ thực hiện dọn dẹp khi nhóm đã lưu đủ bằng chứng và không cần demo lại:

1. Xác nhận **đúng tên bucket demo**, không chọn bucket tài liệu thật. Sao lưu cục bộ những gì muốn giữ.
2. Tại danh sách bucket, chọn bucket demo → **Empty**. Đọc danh sách/phạm vi xóa và xác nhận theo giao diện. Hành động này xóa vĩnh viễn nội dung, gồm các version và delete marker; không thể phục hồi bằng Versioning sau đó.
3. Chờ tác vụ báo thành công, kiểm tra **Show versions** không còn version hoặc delete marker. Nếu từng upload file lớn và bị ngắt, kiểm tra và hủy cả incomplete multipart uploads nếu có.
4. Trở về danh sách bucket → **Delete**, nhập đúng tên bucket theo yêu cầu giao diện và xác nhận.
5. Kiểm tra trang Billing sau đó; số liệu chi phí có thể cập nhật trễ và khoản phát sinh trước khi dọn vẫn được tính.

Xóa object thông thường trong bucket bật Versioning thường chỉ thêm delete marker và giữ bản dữ liệu cũ, nên không phải cách xóa sạch. Mọi version và delete marker phải được dọn trước khi xóa bucket. **Dự án này không tự động xóa tài nguyên**, không cài Lifecycle xóa dữ liệu; việc dọn do người dùng thực hiện sau khi kiểm tra. [AWS: empty bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/empty-bucket.html), [AWS: delete marker](https://docs.aws.amazon.com/AmazonS3/latest/userguide/DeleteMarker.html)

Tài liệu đối chiếu nguồn AWS ngày 28/10/2026. Nhãn nút trong console có thể thay đổi theo ngôn ngữ hoặc đợt cập nhật; đối chiếu tên chức năng nếu giao diện khác nhẹ.
