# Amazon S3: Dàn bài 45 slide

Bản biên tập theo dàn người dùng gửi, giữ trọng tâm Amazon S3 và ba demo AWS Console. Lược phần triển khai MinIO/FastAPI, benchmark chưa chạy và các tuyên bố tuyệt đối. Kiến thức mở rộng không được trình bày như chức năng đã demo.

## 1. Amazon S3

- Lưu trữ đối tượng trên AWS
- Kho tài liệu nhóm: lưu, khôi phục, chia sẻ có hạn
- Nhóm: [điền tên]   Lớp: [điền lớp]

**Gợi ý nói:** Bài trình bày đi từ kiến thức S3 đến ba thao tác trên AWS Console. Sản phẩm là kho tài liệu riêng tư trên dịch vụ thật, không cần chạy một ứng dụng web.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html

## 2. Một tệp nhóm, ba vấn đề

- Tệp nằm rải rác trên nhiều máy
- Nội dung cũ mất sau một lần sửa nhầm
- Link chia sẻ tồn tại lâu hơn nhu cầu
- Cần nơi lưu chung và quyền truy cập rõ ràng

**Gợi ý nói:** Dùng một tệp kế hoạch làm ví dụ xuyên suốt. Nhóm cần giữ được nội dung ban đầu và chia sẻ cho người khác trong một khoảng thời gian có kiểm soát.

**Nguồn:** Tình huống minh họa của nhóm

## 3. Lộ trình trình bày

- Bối cảnh và mô hình lưu trữ đối tượng
- Bảo mật và bảo vệ dữ liệu
- Quản lý dữ liệu, hiệu năng và chi phí
- Ba chức năng demo trực tiếp trên AWS Console

**Gợi ý nói:** Phần kiến thức khoảng 27–30 phút. Phần demo khoảng 8–10 phút. Các trang ngắn có thể đi nhanh hơn; khi trao đổi với thầy, tập trung vào bucket, key, version và quyền truy cập.

**Nguồn:** Cấu trúc bài trình bày của nhóm

## 4. Bối cảnh trước lưu trữ đám mây

- Tự chuẩn bị máy chủ, ổ đĩa và mạng
- Ước lượng dung lượng trước khi dùng
- Tự theo dõi hỏng hóc, sao lưu và mở rộng
- Dữ liệu tăng kéo theo công việc vận hành

**Gợi ý nói:** Đây là bối cảnh vận hành, không phải một quy luật rằng mọi hệ thống nội bộ đều kém. Lưu trữ đám mây chuyển phần lớn công việc hạ tầng sang nhà cung cấp.

**Nguồn:** https://aws.amazon.com/about-aws/our-origins/

## 5. Amazon S3 ra đời năm 2006

- Công bố ngày 14/03/2006
- Cung cấp lưu trữ qua giao diện web service
- Cho lập trình viên sử dụng hạ tầng có thể mở rộng
- Giảm nhu cầu tự xây toàn bộ hệ thống lưu trữ

**Gợi ý nói:** S3 là một trong các dịch vụ nền tảng của AWS. Nhấn vào việc lập trình viên có thể gọi dịch vụ qua mạng, thay vì tự lắp đặt hạ tầng lưu trữ cho từng dự án.

**Nguồn:** https://press.aboutamazon.com/2006/3/amazon-web-services-launches

## 6. Amazon S3 là gì?

- Amazon Simple Storage Service
- Dịch vụ lưu trữ đối tượng trên AWS
- Lưu tài liệu, ảnh, video, bản sao lưu và dữ liệu phân tích
- Truy cập bằng Console, API, CLI hoặc SDK

**Gợi ý nói:** S3 lưu và trả về object. S3 không tự chạy mã Python hay máy chủ ứng dụng. Trong bài này, Console là giao diện để thao tác với dịch vụ thật.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html

## 7. Block, file và object

- Block: làm việc với các khối trên volume
- File: tổ chức theo tệp và thư mục
- Object: dữ liệu gắn với key và metadata
- Chọn theo cách truy cập và nhu cầu của ứng dụng

**Gợi ý nói:** Không xếp hạng mọi hệ thống bằng câu block đắt nhất, object rẻ nhất. Chi phí và hiệu năng phụ thuộc dịch vụ và khối lượng công việc. EBS, EFS và S3 là ba ví dụ AWS tương ứng.

**Nguồn:** https://aws.amazon.com/compare/the-difference-between-block-file-object-storage/

## 8. Mô hình lưu trữ đối tượng

- Bucket chứa các object
- Key xác định object trong bucket
- Metadata mô tả dữ liệu
- Version ID phân biệt phiên bản khi có Versioning

**Gợi ý nói:** Hãy hình dung bucket là phạm vi chứa và quản lý. Muốn đọc đúng một object cần biết bucket và key; nếu muốn đọc một phiên bản cụ thể thì bổ sung version ID.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingObjects.html

## 9. Bucket và phạm vi cấu hình

- Chọn tên và AWS Region khi tạo bucket
- General purpose bucket phù hợp với demo
- Quyền truy cập, Versioning và Lifecycle là cấu hình quan trọng
- Một bucket có thể chứa nhiều object

**Gợi ý nói:** Demo dùng cloudnotes-starlight tại Sydney. Các loại bucket có đặc điểm khác nhau; không áp quy tắc của general purpose bucket cho mọi loại bucket.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingBucket.html

## 10. Key và prefix

- tai-lieu/ke-hoach.txt là một key đầy đủ
- Dấu / giúp Console hiển thị dạng thư mục
- Prefix gom các key có cùng phần đầu
- Demo dùng key gốc ke-hoach-nhom.txt

**Gợi ý nói:** Trong mô hình general purpose bucket đang xét, prefix không phải thư mục vật lý trên một ổ đĩa. Ghi cùng key khi Versioning bật tạo thêm phiên bản thay vì đổi tên tệp.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-keys.html

## 11. Metadata và object tags

- Metadata: Content-Type và thông tin mô tả khác
- Metadata do hệ thống hoặc người dùng cung cấp
- Tags: các cặp key–value dùng phân loại object
- Tags và metadata là hai cơ chế khác nhau

**Gợi ý nói:** Dàn gốc gộp tags vào metadata dễ làm người nghe nhầm. Ví dụ Content-Type mô tả cách đọc nội dung, còn tag project=cloudnotes có thể dùng để phân loại hoặc quản lý.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMetadata.html

## 12. Region và Availability Zone

- Region là một khu vực địa lý của AWS
- AZ gồm một hoặc nhiều trung tâm dữ liệu tách biệt
- S3 Standard lưu dữ liệu trên ít nhất ba AZ
- Demo chọn Sydney: ap-southeast-2

**Gợi ý nói:** Một Region chứa nhiều AZ. Đặc điểm nhiều AZ được nêu cho S3 Standard; One Zone-IA và Express One Zone có mô hình một AZ khác.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html

## 13. Bốn thao tác với object

- PUT: ghi object
- GET: lấy nội dung object
- LIST: liệt kê object
- DELETE: xử lý theo trạng thái Versioning

**Gợi ý nói:** Console đóng gói thao tác thành nút Upload, Download và Delete. Hiểu các thao tác API giúp giải thích được điều gì xảy ra phía sau giao diện.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingObjects.html

## 14. Độ bền và độ sẵn sàng

- Durability: khả năng giữ dữ liệu lâu dài
- Availability: khả năng truy cập khi cần
- S3 Standard được thiết kế cho 99.999999999% độ bền
- S3 Standard được thiết kế cho 99.99% độ sẵn sàng

**Gợi ý nói:** Đây là hai mục tiêu thiết kế khác nhau, không phải cam kết không bao giờ mất dữ liệu hoặc gián đoạn. Không dùng hai con số này chung cho mọi storage class. Versioning vẫn cần để xử lý ghi đè nhầm.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/DataDurability.html

## 15. Strong consistency

- Ghi mới thành công: có thể đọc thấy object
- Ghi đè thành công: đọc thấy bản mới
- LIST phản ánh thay đổi đã thành công
- Replication xuyên Region vẫn là cơ chế bất đồng bộ

**Gợi ý nói:** Tính nhất quán cho phép demo ghi đè rồi đọc ngay bản hiện tại. Nó không có nghĩa mọi hệ thống cache hay mọi bản sao ở Region khác đều cập nhật tức thì.

**Nguồn:** https://aws.amazon.com/s3/consistency/

## 16. Mô hình trách nhiệm chung

- AWS vận hành hạ tầng chạy dịch vụ
- Người dùng quản lý dữ liệu và quyền truy cập
- Người dùng chọn cấu hình, vòng đời và cách sử dụng
- Bảo mật cần cả dịch vụ và lựa chọn đúng

**Gợi ý nói:** Có mã hóa mặc định không thay thế việc cấp quyền đúng. Một policy hoặc quy tắc xóa sai vẫn có thể gây hậu quả dù hạ tầng của AWS hoạt động bình thường.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/security.html

## 17. IAM policy và bucket policy

- IAM policy gắn quyền với danh tính
- Bucket policy gắn quy tắc với tài nguyên
- Policy có thể xét hành động, tài nguyên và điều kiện
- Chỉ cấp quyền cần thiết cho công việc

**Gợi ý nói:** Một yêu cầu truy cập được đánh giá theo các chính sách áp dụng. Không nên dùng câu chỉ cần có URL là tải được, vì S3 còn kiểm tra quyền và chữ ký.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-management.html

## 18. Block Public Access

- Lớp kiểm soát nhằm hạn chế truy cập công khai
- Có cấu hình ở cấp tài khoản và bucket
- Demo bật cả bốn tùy chọn ở bucket
- Vẫn có thể chia sẻ bằng presigned URL hợp lệ

**Gợi ý nói:** Block Public Access không có nghĩa chặn mọi hình thức truy cập. Người đã có quyền và request được ký hợp lệ vẫn có thể sử dụng object riêng tư.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/configuring-block-public-access-bucket.html

## 19. Mã hóa khi lưu và khi truyền

- Object mới có mã hóa phía máy chủ mặc định
- Demo dùng SSE-S3, khóa do S3 quản lý
- HTTPS bảo vệ dữ liệu trên đường truyền
- Mã hóa và quyền truy cập là hai việc khác nhau

**Gợi ý nói:** Chỉ giới thiệu thêm SSE-KMS khi thầy hỏi nhu cầu quản lý khóa. Không cần đưa mọi lựa chọn mã hóa vào demo và không biến mã hóa thành bằng chứng rằng object đã được cấp quyền an toàn.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/default-encryption-faq.html

## 20. Presigned URL: Quyền truy cập có thời hạn

- Được ký bằng thông tin xác thực của bên có quyền
- Gắn với một hành động và một tài nguyên
- Hợp lệ trong thời hạn và quyền của bên ký
- Người có link có thể thực hiện hành động được cho phép

**Gợi ý nói:** Không cần một backend mới để thực hiện demo vì AWS Console có chức năng tạo URL. Presigned URL là bearer token, cần giữ kín. Nó không mặc định chỉ được sử dụng một lần.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html

## 21. Luồng cấp quyền và luồng dữ liệu

- Ứng dụng có thể cấp URL tạm thời cho client
- Client truyền dữ liệu trực tiếp với S3
- Backend không cần trung chuyển toàn bộ nội dung tệp
- Demo này tạo URL ngay từ AWS Console

**Gợi ý nói:** Đây là mô hình kiến trúc ứng dụng để giải thích ý nghĩa của presigned URL. Nhóm không tuyên bố đã xây FastAPI, MinIO hoặc đo hiệu năng backend. Phần thực nghiệm chỉ dùng S3 Console.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html

## 22. Versioning: Cùng key, nhiều phiên bản

- Bật Versioning trước khi thử ghi đè
- Ghi nội dung mới cùng key tạo version mới
- Có thể đọc bản cũ bằng Version ID
- Các phiên bản cũ tiếp tục dùng dung lượng

**Gợi ý nói:** Versioning giữ lịch sử thay đổi object. Demo dùng hai nội dung khác nhau của tệp kế hoạch, sau đó phục hồi bản đầu thành phiên bản hiện tại thứ ba.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html

## 23. Delete marker và xóa phiên bản

- Xóa không chỉ định version có thể tạo delete marker
- GET mặc định khi đó không trả về bản cũ
- Xóa một version ID có thể xóa vĩnh viễn phiên bản đó
- Phải phân biệt xóa logic và xóa phiên bản

**Gợi ý nói:** Nội dung này là kiến thức bổ sung, không phải một chức năng demo đã chạy. Không phát biểu rằng mọi lệnh DELETE đều chỉ thêm delete marker, vì xóa theo version ID có thể xóa dữ liệu vĩnh viễn.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/DeleteMarker.html

## 24. Object Lock: Bảo vệ một phiên bản

- Cơ chế WORM: bảo vệ phiên bản trong thời gian lưu
- Governance và Compliance có quy tắc khác nhau
- Hữu ích khi cần chính sách lưu giữ bắt buộc
- Demo không bật Object Lock

**Gợi ý nói:** Object Lock áp dụng cho phiên bản. Vẫn có thể tạo phiên bản mới của cùng key. Governance có thể được bỏ qua bằng quyền đặc biệt, còn Compliance bảo vệ chặt hơn trong thời hạn lưu giữ.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html

## 25. Chọn storage class theo nhu cầu

- Tần suất truy cập dữ liệu
- Độ trễ và thời gian chờ phục hồi
- Có cần chịu mất cả một AZ hay không?
- Tổng chi phí lưu, đọc và chuyển lớp

**Gợi ý nói:** Không chọn chỉ theo giá lưu trữ mỗi GB. Dữ liệu ít dùng nhưng cần đọc ngay khác với dữ liệu có thể chờ nhiều giờ để phục hồi.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html

## 26. Các lớp lưu trữ thường gặp

- Standard: thường xuyên truy cập
- Intelligent-Tiering: tần suất khó dự đoán
- Standard-IA và One Zone-IA: ít truy cập
- Express One Zone: độ trễ thấp, dùng directory bucket

**Gợi ý nói:** Demo dùng Standard. Express One Zone có đặc điểm một AZ và directory bucket, không phải một công tắc tăng tốc cho bucket demo hiện tại. Các lớp có mức phí đọc và thời gian lưu tối thiểu khác nhau.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html

## 27. Glacier và thời gian truy xuất

- Instant Retrieval: truy cập ngay mức mili giây
- Flexible Retrieval: tùy mức phục hồi, từ phút đến giờ
- Deep Archive: thường 12 giờ (Standard), 48 giờ (Bulk)
- Chọn theo thời gian có thể chờ và chi phí

**Gợi ý nói:** Không gộp toàn bộ Glacier thành vài phút đến 12 giờ như dàn gốc. Thời gian phụ thuộc lớp và tùy chọn retrieval. Đây là phần lý thuyết, không chuyển object demo sang archive.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/restoring-objects-retrieval-options.html

## 28. Lifecycle: Quản lý dữ liệu theo thời gian

- Transition chuyển sang lớp lưu trữ phù hợp
- Expiration xử lý object theo quy tắc
- Có thể quản lý phiên bản cũ
- Mốc thời gian phải phù hợp dữ liệu và điều kiện lớp

**Gợi ý nói:** Ví dụ ngày 30 chuyển IA, ngày 90 chuyển archive chỉ là chính sách minh họa. Với bucket bật Versioning, expiration của bản hiện tại thường tạo delete marker, không tự xóa mọi phiên bản cũ.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html

## 29. Multipart upload và tệp lớn

- Khởi tạo, tải các phần, hoàn tất
- Tải song song và thử lại phần gặp lỗi
- AWS khuyến nghị cân nhắc từ 100 MB
- S3 hiện hỗ trợ object đến 50 TB

**Gợi ý nói:** Giới hạn 5 TB trong dàn gốc đã thay đổi ngày 02/12/2025. Một PUT đơn có giới hạn 5 GB; tệp lớn hơn cần multipart. Các phần chưa hoàn tất có thể tiếp tục phát sinh chi phí cho đến khi hoàn tất hoặc hủy. Nguồn cập nhật: https://aws.amazon.com/about-aws/whats-new/2025/12/amazon-s3-maximum-object-size-50-tb/

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html

## 30. Hiệu năng và prefix

- Ít nhất 3.500 yêu cầu ghi mỗi giây cho mỗi prefix phân vùng
- Ít nhất 5.500 GET/HEAD mỗi giây cho mỗi prefix phân vùng
- Có thể tăng thông lượng bằng song song hóa
- Mở rộng diễn ra dần, còn phụ thuộc workload

**Gợi ý nói:** Đây không phải mức trần cứng hay kết quả benchmark của nhóm. Tệp demo rất nhỏ nên chỉ chứng minh chức năng, không dùng để kết luận về hiệu năng ở quy mô lớn.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/optimizing-performance.html

## 31. Sự kiện từ S3

- Object mới hoặc bị xóa có thể phát thông báo
- Đích gồm Lambda, SQS, SNS hoặc EventBridge
- Ví dụ: xử lý ảnh sau khi upload
- Thông báo có thể lặp, cần xử lý phù hợp

**Gợi ý nói:** S3 Event Notifications có cơ chế at least once. Hình luồng trên slide là mô hình khái niệm, không phải hệ thống Lambda hoặc worker mà nhóm đã triển khai.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/EventNotifications.html

## 32. Phân tích dữ liệu với Athena

- Dữ liệu nằm trong S3
- Athena thực hiện truy vấn SQL trên dữ liệu phù hợp
- Không cần tự dựng cụm cơ sở dữ liệu cho ví dụ này
- S3 Select không còn mở cho khách hàng mới

**Gợi ý nói:** Không giữ lời hứa tiết kiệm 80–90% vì thiếu bối cảnh đo. S3 là nơi lưu, Athena là dịch vụ truy vấn. Việc chọn định dạng và phân vùng dữ liệu ảnh hưởng chi phí và tốc độ. S3 Select: https://docs.aws.amazon.com/AmazonS3/latest/userguide/selecting-content-from-objects.html

**Nguồn:** https://docs.aws.amazon.com/athena/latest/ug/what-is.html

## 33. Replication giữa các bucket

- SRR: nhân bản trong cùng Region
- CRR: nhân bản sang Region khác
- Đây là quá trình bất đồng bộ
- Cần xét Versioning, quyền và chi phí

**Gợi ý nói:** Replication khác Versioning: Versioning giữ lịch sử trong bucket, replication tạo bản sao ở bucket đích. Cũng khác với strong consistency khi đọc dữ liệu trong phạm vi dịch vụ nguồn.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html

## 34. Chi phí sử dụng S3

- Dung lượng và thời gian lưu, kể cả version cũ
- Requests và phí retrieval tùy storage class
- Truyền dữ liệu và các tính năng bổ sung
- Free Tier phụ thuộc tài khoản và điều kiện hiện hành

**Gợi ý nói:** Không nói chắc demo miễn phí hoặc mọi GET đều cùng một đơn giá. Với phiên bản cũ, dung lượng vẫn tính tiền. Sau buổi học cần theo dõi Billing và dọn tài nguyên phù hợp.

**Nguồn:** https://aws.amazon.com/s3/pricing/

## 35. Ưu điểm và giới hạn

- Giảm việc vận hành hạ tầng lưu trữ
- Phù hợp ảnh, tài liệu, backup và data lake
- Phụ thuộc mạng, cấu hình quyền và mô hình chi phí
- Không thay thế ổ đĩa hay cơ sở dữ liệu cho mọi nhu cầu

**Gợi ý nói:** Chọn S3 khi ứng dụng phù hợp truy cập object. Một yêu cầu đọc ghi khối cho hệ điều hành hoặc giao dịch cơ sở dữ liệu có thể cần loại lưu trữ khác.

**Nguồn:** https://aws.amazon.com/s3/

## 36. Demo: Kho tài liệu nhóm

- Một bucket riêng tư trên Amazon S3
- Một key: ke-hoach-nhom.txt
- Ba chức năng: lưu, phục hồi, chia sẻ tạm thời
- GitHub chứa hướng dẫn, tệp mẫu và ảnh kiểm chứng

**Gợi ý nói:** Phần này chuyển sang AWS Console. Không cần chạy Docker, MinIO, FastAPI hay mã HTML. Sơ đồ chỉ mô tả các thành phần thực sự dùng trong sản phẩm.

**Nguồn:** https://github.com/st4rlight3/amazon-s3-kho-tai-lieu-demo

## 37. Cấu hình trước khi demo

- Bucket: cloudnotes-starlight
- Region Sydney: ap-southeast-2
- Versioning bật, S3 Standard, SSE-S3
- Block Public Access bật, ACL disabled

**Gợi ý nói:** Ảnh trên slide chứng minh trạng thái Versioning bật. Các cấu hình còn lại được kiểm tra trong báo cáo demo. Không chỉnh public hay phát hành access key để chia sẻ tài liệu.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingBucket.html

## 38. Demo 1: Upload và download

- Upload samples/v1/ke-hoach-nhom.txt
- Quan sát object 305 byte trong bucket
- Download và mở tệp để đối chiếu
- Nội dung đúng: Thu Sau, 14:00

**Gợi ý nói:** Thao tác trực tiếp: mở bucket, Upload, Add files, chọn tệp v1 rồi Upload. Tải lại bản hiện tại bằng Download và đối chiếu. Đây là PUT và GET của cùng object.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html

## 39. Demo 2: Mô phỏng ghi đè nhầm

- Upload samples/v2/ke-hoach-nhom.txt cùng key
- Bản hiện tại đổi sang Thu Hai, 08:00
- Bật Show versions để nhìn lịch sử
- Chọn đúng Version ID của bản đầu

**Gợi ý nói:** Không đổi tên tệp v2 khi upload. Hai nội dung có cùng key nên S3 tạo version mới. Khi xem ảnh đã kiểm chứng, có ba versions vì ảnh chụp sau khi hoàn tất cả bước khôi phục.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html

## 40. Phục hồi nội dung v1 thành v3

- Tải đúng v1 từ S3 và kiểm tra nội dung
- Upload lại tệp vừa phục hồi cùng key
- Bản hiện tại trở lại Thu Sau, 14:00
- Lịch sử v1 và v2 vẫn còn

**Gợi ý nói:** Đây là cách phục hồi được chọn cho bài: tải phiên bản trước rồi ghi lại. v1, v2, v3 là nhãn trong bài, không phải định dạng Version ID thật của AWS.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/RestoringPreviousVersions.html

## 41. Demo 3: Chia sẻ đọc tạm thời

- Object URL thường: truy cập bị từ chối
- Tạo presigned URL đọc từ AWS Console
- Mở link trong thời hạn: đọc được object
- Bucket vẫn riêng tư, Block Public Access vẫn bật

**Gợi ý nói:** Hai request khác nhau vì presigned URL mang chữ ký và quyền của bên ký. Người nhận không cần đổi bucket thành public. Không chiếu URL thật chứa chữ ký lên slide hoặc đưa vào GitHub.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html

## 42. Hết hạn: Kiểm tra bằng request mới

- Kịch bản trực tiếp: chọn thời hạn 1 phút
- Mở link hợp lệ để chứng minh đọc được
- Sau hạn, gửi GET mới: Request has expired
- Ảnh kiểm thử thực tế dùng 5 phút (300 giây)

**Gợi ý nói:** Không dùng trang đã cache để kết luận URL còn hiệu lực. Kiểm tra bằng một request mới sau thời hạn. Ảnh thành công dùng ở đây và ảnh phục hồi là cùng một GET thành công, không phải hai phép thử độc lập.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html

## 43. Kết quả và dọn sau buổi học

- Đã kiểm tra upload, phục hồi và chia sẻ có hạn
- Demo nhỏ kiểm chứng chức năng, không phải benchmark
- Giữ ảnh dự phòng nếu mạng hoặc phiên đăng nhập lỗi
- Theo dõi Billing, dọn versions và bucket khi không dùng

**Gợi ý nói:** Không xóa tài nguyên trong lúc trình bày nếu chưa cần. Khi dọn phải hiểu xóa object hiện tại chưa chắc đã xóa mọi version. Hướng dẫn đầy đủ nằm trong README và kịch bản demo.

**Nguồn:** https://github.com/st4rlight3/amazon-s3-kho-tai-lieu-demo/blob/main/docs/ket-qua-demo.md

## 44. Ba điều cần nhớ

- S3 lưu object trong bucket, truy cập bằng key
- Versioning giữ lịch sử, presigned URL chia sẻ có hạn
- Dùng đúng quyền, lớp lưu trữ và cách tính phí
- Trao đổi: Vì sao URL thường bị chặn nhưng link đã ký đọc được?

**Gợi ý nói:** Mời thầy chọn một thao tác để nhóm giải thích theo luồng: người thực hiện, quyền cần có, request gửi đến S3 và kết quả nhìn thấy. Đây là cách chứng minh nhóm hiểu demo.

**Nguồn:** https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html

## 45. Tài liệu và mã nguồn bàn giao

- AWS S3 User Guide: docs.aws.amazon.com/AmazonS3/
- AWS S3 Pricing: aws.amazon.com/s3/pricing/
- Nguồn chi tiết nằm trong ghi chú từng slide
- GitHub: st4rlight3/amazon-s3-kho-tai-lieu-demo

**Gợi ý nói:** Nguồn tham khảo được đặt trong ghi chú của từng slide và tài liệu nguồn trên GitHub. Bài chỉ tuyên bố các chức năng có bằng chứng đã chạy. Nền được lấy từ bản Canva do người dùng cung cấp.

**Nguồn:** https://github.com/st4rlight3/amazon-s3-kho-tai-lieu-demo
