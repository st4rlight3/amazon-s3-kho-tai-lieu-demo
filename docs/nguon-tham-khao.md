# Nguồn tham khảo chính thức về Amazon S3

Ngày đối chiếu: **28/10/2026**. Tất cả nguồn dưới đây thuộc AWS hoặc Amazon. Đây là ghi chú kiểm chứng kiến thức và giới hạn phát biểu, để dùng cho bài thuyết trình và demo trên AWS Console.

Phạm vi demo: **general purpose bucket**, object thông thường, lớp **S3 Standard**. Không cần giới thiệu hết các sản phẩm mới thuộc họ S3.

## 1. Định nghĩa và mô hình cơ bản

[What is Amazon S3? — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)

- Amazon S3 là **Amazon Simple Storage Service**, dịch vụ lưu trữ đối tượng trên đám mây.
- **Bucket** chứa object; **object** gồm dữ liệu và metadata; **key** định danh object trong bucket.
- Khi tạo bucket, chọn tên và AWS Region. Ví dụ `tai-lieu/bao-cao.txt` là một key.
- Ứng dụng điển hình: lưu ảnh/tài liệu, backup, archive, data lake.
- Cần phân biệt bucket với object và key; version ID phân biệt các phiên bản khi bật Versioning.

Lưu ý tên bucket: mặc định general purpose bucket dùng shared global namespace và tên phải duy nhất trong một AWS partition. Tài liệu hiện cũng có **account regional namespace**. Vì vậy không nên nói “mọi tên bucket S3 luôn duy nhất toàn thế giới”.

## 2. Bối cảnh ra đời và ngày công bố

[Amazon Web Services Launches — Amazon Press Center, 14/03/2006](https://press.aboutamazon.com/2006/3/amazon-web-services-launches)

- S3 được công bố và cung cấp ngày **14/03/2006**.
- Mục tiêu ban đầu: cho lập trình viên dùng hạ tầng lưu trữ có khả năng mở rộng qua một giao diện web service đơn giản.
- Có thể mô tả ý nghĩa là giảm nhu cầu tự mua và quản lý toàn bộ hạ tầng lưu trữ trước khi xây ứng dụng.

[Our Origins — AWS](https://aws.amazon.com/about-aws/our-origins/)

- AWS liên hệ sự ra đời của dịch vụ với trải nghiệm Amazon tự vận hành hạ tầng: tốn kém, phức tạp và làm đội phát triển mất thời gian cho việc quản trị.
- Đây là lời giải thích của AWS về lịch sử của chính họ; không cần thêm suy đoán về thị trường năm 2006.

Không dùng giá, giới hạn kích thước object hoặc tính năng năm 2006 làm thông số hiện tại.

## 3. “Thư mục” trong bucket thông thường

[Naming Amazon S3 objects — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-keys.html)

- General purpose bucket có mô hình key phẳng. Console hiển thị “folder” bằng prefix và dấu phân cách `/` trong key.
- `tai-lieu/bao-cao.txt` là tên key đầy đủ, không phải một hệ thống thư mục con trên ổ đĩa.
- Phát biểu này áp dụng cho general purpose bucket của demo; không suy rộng sang directory bucket.

## 4. Tính nhất quán

[Amazon S3 Strong Consistency — AWS](https://aws.amazon.com/s3/consistency/)

- S3 có **strong read-after-write consistency** và tính nhất quán mạnh cho LIST.
- Sau khi ghi mới hoặc ghi đè thành công, lần đọc sau nhận dữ liệu mới nhất; danh sách phản ánh thay đổi đã thành công. Điều này cũng áp dụng cho xóa object.
- Tính năng này tự có, không thu thêm phí riêng.

Không dùng mô tả cũ “ghi đè/xóa phải chờ eventual consistency”. Điều này không có nghĩa mọi cấu hình bucket hay bản sao ở Region khác đều cập nhật tức thì.

## 5. Durability khác availability

[Data protection in Amazon S3 — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/DataDurability.html)

- **S3 Standard** được thiết kế cho độ bền dữ liệu **99.999999999%** và độ sẵn sàng **99.99%** trong một năm.
- Durability nói về khả năng giữ dữ liệu; availability nói về khả năng truy cập khi cần.
- Standard và một số lớp nhiều AZ được thiết kế chịu được mất toàn bộ một Availability Zone.
- Các tính năng Versioning, Object Lock, Replication giải quyết thêm những nhu cầu bảo vệ dữ liệu khác nhau.

Nên nói “được thiết kế cho”, không nói “cam kết không bao giờ mất dữ liệu”. 11 số 9 không đồng nghĩa availability, không bảo vệ trước mọi thao tác xóa có quyền và không thay thế chiến lược backup.

## 6. Bảo mật mặc định

[Default encryption FAQ — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/default-encryption-faq.html)

- Từ 05/01/2023, mọi object tải lên mới được mã hóa phía máy chủ. SSE-S3 là mức mã hóa nền tảng, không có phụ phí mã hóa SSE-S3.
- Bucket có thể được cấu hình phương thức khác, chẳng hạn SSE-KMS. Không cần dùng KMS cho demo này.
- Thay đổi năm 2023 không tự mã hóa lại các object cũ từng lưu không mã hóa.
- Mã hóa dữ liệu khi lưu và quyền truy cập là hai cơ chế riêng; mã hóa không biến URL công khai thành riêng tư.

[Configuring block public access settings for your S3 buckets — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/configuring-block-public-access-bucket.html)

- Bucket/object mới không cho public access theo mặc định.
- Block Public Access có nhiều cấp. AWS áp dụng kết hợp hạn chế nhất giữa cấp bucket và cấp tài khoản/tổ chức đang có hiệu lực.
- Demo có thể giữ cả bốn tùy chọn Block Public Access và dùng presigned URL để chia sẻ tạm thời.

[Controlling ownership of objects and disabling ACLs — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/about-object-ownership.html)

- Bucket mới mặc định **Bucket owner enforced**, ACL bị vô hiệu hóa.
- AWS khuyến nghị sử dụng IAM policy hoặc resource policy cho kiểm soát truy cập trong các trường hợp thông thường.

## 7. Presigned URL và chia sẻ tạm thời

[Download and upload objects with presigned URLs — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html)

- Presigned URL cấp quyền thao tác có thời hạn lên object, không cần sửa bucket policy.
- Người có URL có thể sử dụng URL trong thời hạn còn hiệu lực; đây không phải link chỉ dùng một lần.
- Người tạo phải có quyền tương ứng, ví dụ `s3:GetObject` để đọc.
- Console cho đặt từ **1 phút đến 12 giờ**. Credentials tạm thời có thể khiến URL hết hiệu lực sớm hơn thời gian đã chọn.
- Hết hạn được kiểm tra khi có request mới; download đã bắt đầu trước lúc hết hạn có thể tiếp tục.

Không commit URL còn hiệu lực lên GitHub. Khi kiểm tra hết hạn, mở request mới hoặc dùng cửa sổ riêng tư để tránh nhầm với nội dung trình duyệt đã tải sẵn.

[Sharing objects with presigned URLs — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html)

- Tạo link trực tiếp trong S3 Console: chọn object → **Object actions** → **Share with a presigned URL** → chọn thời hạn → tạo URL.
- Tên nút có thể thay đổi theo giao diện Console; cần chạy thử trong tài khoản dùng thuyết trình.

## 8. Versioning và khôi phục

[Retaining multiple versions of objects with S3 Versioning — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)

- Versioning mặc định tắt; cần bật trước phần demo.
- Ghi đè cùng key tạo phiên bản mới, giữ phiên bản cũ.
- Mỗi phiên bản là toàn bộ object và có tính phí lưu trữ, không chỉ là phần thay đổi.
- Bucket đã bật có thể suspend nhưng không trở lại trạng thái unversioned.

[Managing delete markers — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ManagingDelMarkers.html)

- Xóa object mà không chỉ định version ID trong bucket đang bật Versioning tạo **delete marker**, các phiên bản dữ liệu vẫn còn.
- Khôi phục trường hợp này bằng cách hiển thị versions rồi xóa đúng **delete marker** hiện tại.
- Cần phân biệt xóa marker với xóa vĩnh viễn một phiên bản dữ liệu.
- Chỉ dùng object mẫu khi luyện tập thao tác xóa; dọn bucket phải tính cả phiên bản cũ và delete marker.

## 9. Các storage class cần biết

[Understanding and managing Amazon S3 storage classes — AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html)

| Lớp | Cách dùng dễ nhớ |
| --- | --- |
| S3 Standard | Dữ liệu truy cập thường xuyên; dùng cho demo. |
| S3 Intelligent-Tiering | Tần suất truy cập khó dự đoán, tự chuyển access tier. |
| S3 Standard-IA | Ít truy cập, vẫn cần truy xuất mili giây. |
| S3 One Zone-IA | Ít truy cập, có thể tái tạo, lưu trong một AZ. |
| S3 Glacier Instant Retrieval | Archive vẫn cần truy xuất mili giây. |
| S3 Glacier Flexible Retrieval | Archive, chấp nhận chờ phút đến giờ. |
| S3 Glacier Deep Archive | Archive lâu dài, chấp nhận chờ nhiều giờ. |
| S3 Express One Zone | Nhu cầu độ trễ thấp trong một AZ. |

One Zone-IA và Express One Zone không có khả năng chịu mất cả AZ như các lớp nhiều AZ. IA/Glacier có thể có phí retrieval, thời gian lưu tối thiểu và kích thước tính phí tối thiểu. Không nên chuyển lớp để minh họa một demo kéo dài vài phút.

## 10. Chi phí và Free Tier

[Amazon S3 Pricing — AWS](https://aws.amazon.com/s3/pricing/)

- Nhóm chi phí: dung lượng lưu, requests, retrieval, truyền dữ liệu, cùng tính năng quản lý/replication/xử lý nếu sử dụng.
- Xem bucket bằng Console cũng tạo requests tính phí theo biểu giá.
- Giá phụ thuộc Region, storage class và cách dùng. Các phiên bản dữ liệu cũ cũng chiếm dung lượng.
- Các lớp lưu trữ ít truy cập/archive có thể tính phí tối thiểu dù xóa sớm.

Không hứa demo “chắc chắn miễn phí” và không chốt giá USD/GB khi chưa chọn Region. Mẫu nhỏ, Standard, ít request và dọn sạch sau buổi học giúp giữ chi phí thấp; kiểm tra Billing thực tế trong tài khoản.

[Explore AWS services with AWS Free Tier — AWS Billing User Guide](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier.html)

- Chương trình hiện tại cho khách hàng mới có credits khi đăng ký và khả năng nhận thêm credits qua hoạt động đủ điều kiện.
- Free account plan kéo dài tối đa sáu tháng hoặc đến khi dùng hết credits, tùy điều kiện nào xảy ra trước.
- Phải kiểm tra plan, ngày tạo tài khoản, credits và dịch vụ đủ điều kiện thực tế.

[AWS Free Tier announcement — AWS, 16/07/2025](https://aws.amazon.com/about-aws/whats-new/2025/07/aws-free-tier-credits-month-free-plan/)

- Thông báo giới thiệu chương trình mới: 100 USD credits ban đầu, có thể nhận thêm tối đa 100 USD.
- Không đồng nghĩa mọi tài khoản đều có sẵn 200 USD hay mọi dịch vụ đều miễn phí vô hạn.

[Control Your AWS Costs — AWS tutorial](https://docs.aws.amazon.com/hands-on/latest/control-your-costs-free-tier-budgets/control-your-costs-free-tier-budgets.html)

- Tài khoản tạo trước 15/07/2025 thuộc Legacy AWS Free Tier. Tài liệu cũ về “5 GB S3 miễn phí trong 12 tháng” không nên áp dụng mặc định cho tài khoản mới.

## Cách dùng nguồn trong Canva

Gắn link nguồn cạnh dữ kiện số hoặc ghi số nguồn ngắn ở chân slide, rồi có slide tài liệu tham khảo cuối. Đây là bản tóm tắt bằng tiếng Việt; các liên kết dẫn đến tài liệu gốc. Chụp màn hình demo sau khi chạy thật và che thông tin tài khoản cùng URL còn hiệu lực.
