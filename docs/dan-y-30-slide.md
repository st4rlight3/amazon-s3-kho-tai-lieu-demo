# Amazon S3 — Dàn ý 30 slide cho Canva

**Thời lượng mục tiêu: 35 phút 30 giây**, gồm 7 phút 30 giây demo trực tiếp. Nội dung được đối chiếu với tài liệu AWS ngày **28/10/2026**.

Mỗi mục bên dưới tương ứng đúng một trang Canva. Chỉ đưa phần **Nội dung trên slide** lên trang; dán **Lời thuyết trình** vào phần ghi chú. Phần demo là một dự án cấu hình và vận hành **AWS Console**: một general purpose bucket riêng tư, S3 Standard, ba chức năng. Không có ứng dụng web, HTML hay Python trong phạm vi sản phẩm này.

Dùng khổ 16:9, nền sáng hoặc xanh đậm, một màu cam làm điểm nhấn; mỗi trang chỉ có một hình chính. Link nguồn có thể đặt nhỏ ở chân trang. Các đường dẫn ảnh là vị trí dự kiến để chèn ảnh thật sau khi chạy demo; không được xem ảnh chưa có là bằng chứng đã chạy. Che thông tin tài khoản và URL có chữ ký trước khi chụp.

## Slide 01 — Amazon S3: Lưu trữ đơn giản, hiểu từ một tệp nhỏ

**Thời lượng:** 0 phút 30 giây.

**Nội dung trên slide:**

- Amazon Simple Storage Service
- Từ bài toán lưu tệp đến dịch vụ đám mây
- Demo: lưu, khôi phục, chia sẻ có thời hạn
- Nhóm: [điền tên] · Lớp: [điền lớp]

**Lời thuyết trình:**

Hôm nay nhóm trình bày Amazon S3 qua một tình huống rất gần với việc học: cả nhóm cùng lưu và chia sẻ một tệp kế hoạch. Chúng em sẽ giải thích những khái niệm cần dùng, sau đó thao tác trực tiếp trên AWS Console. Sản phẩm tập trung vào ba việc: tải tệp lên và lấy về, phục hồi nội dung cũ khi bị ghi đè, rồi tạo liên kết đọc có thời hạn. Mục tiêu là sau buổi này, chúng ta hiểu mỗi thao tác đang thay đổi điều gì trong dịch vụ và vì sao chọn cách cấu hình đó.

**Gợi ý hình:** Biểu tượng bucket ở giữa, ba nhánh nhỏ ghi “Lưu”, “Khôi phục”, “Chia sẻ”; thêm tên nhóm ở chân trang.

**Nguồn:** Phạm vi và mục tiêu do nhóm thiết kế.

## Slide 02 — Một tệp nhóm, ba vấn đề quen thuộc

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Tệp nằm rải rác trên nhiều máy
- Bản sửa mới làm mất nội dung cũ
- Chia sẻ nhầm hoặc để link tồn tại quá lâu
- Cần một nơi lưu với quyền truy cập rõ ràng

**Lời thuyết trình:**

Giả sử nhóm có tệp kế hoạch thuyết trình. Một bạn giữ bản đầu, bạn khác sửa lịch, rồi gửi lại qua nhiều kênh. Đến lúc tổng hợp, mọi người khó biết bản nào đang được dùng. Nếu nội dung bị sửa sai, nhóm cần lấy lại bản trước. Nếu chỉ muốn gửi cho người xem trong một khoảng thời gian, quyền chia sẻ cũng phải phù hợp. Đây là tình huống giả định để đặt yêu cầu cho demo. Nhóm chọn một tệp văn bản nhỏ để người xem đọc được ngay sự thay đổi, thay vì phải suy đoán từ tên tệp.

**Gợi ý hình:** Ba máy tính với ba bản “kế hoạch” khác nhau; khoanh ba vấn đề “Phân tán”, “Ghi đè”, “Quyền chia sẻ”.

**Nguồn:** Tình huống minh họa do nhóm xây dựng.

## Slide 03 — Sau bài này cần hiểu được điều gì?

**Thời lượng:** 0 phút 30 giây.

**Nội dung trên slide:**

- Hiểu bucket, object, key và version
- Giải thích bảo mật, độ bền và chi phí
- Chọn trường hợp phù hợp với S3
- Chứng minh ba chức năng bằng demo

**Lời thuyết trình:**

Bài trình bày có bốn phần nối tiếp nhau. Đầu tiên là lý do cần một dịch vụ lưu trữ như S3. Tiếp theo là mô hình dữ liệu và cách truy cập, để chúng ta đọc được giao diện Console. Phần thứ ba xem xét các lựa chọn vận hành như bảo mật, phiên bản, lớp lưu trữ và chi phí. Cuối cùng, nhóm dùng đúng những kiến thức đó trong demo. Mọi thành viên cần giải thích được toàn bộ luồng, từ tệp trên máy đến object trên S3, rồi từ object đến người nhận liên kết tạm thời.

**Gợi ý hình:** Đường đi bốn chặng: “Bài toán → Mô hình → Lựa chọn → Demo”; đánh dấu ba thuật ngữ trọng tâm.

**Nguồn:** Cấu trúc bài trình bày do nhóm thiết kế.

## Slide 04 — Trước đám mây: Tự chuẩn bị nơi lưu dữ liệu

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Chuẩn bị máy chủ, ổ đĩa và mạng
- Dự tính dung lượng trước khi sử dụng
- Theo dõi hỏng hóc, sao lưu và mở rộng
- Càng tăng dữ liệu, càng thêm việc vận hành

**Lời thuyết trình:**

Hãy hình dung một nhóm tự dựng máy chủ để lưu tài liệu. Ngoài việc chép tệp, nhóm còn phải chọn dung lượng, cấp điện, kết nối mạng, theo dõi ổ đĩa và chuẩn bị khi thiết bị gặp lỗi. Nếu mua thiếu, việc mở rộng có thể làm gián đoạn kế hoạch; nếu mua dư, một phần tài nguyên chưa được sử dụng. Mô hình tự quản vẫn phù hợp trong nhiều hoàn cảnh, nhưng đòi hỏi người vận hành có thời gian và kỹ năng. Đây là bối cảnh giúp hiểu giá trị của dịch vụ được quản lý: chuyển một phần công việc hạ tầng cho nhà cung cấp.

**Gợi ý hình:** Hai cột “Việc muốn làm: lưu dữ liệu” và “Việc phải chuẩn bị: máy chủ, ổ đĩa, mạng, sao lưu”.

**Nguồn:** Bối cảnh hạ tầng trong [AWS — Our Origins](https://aws.amazon.com/about-aws/our-origins/); ví dụ lớp học do nhóm diễn giải.

## Slide 05 — S3 ra đời để đơn giản hóa lưu trữ qua Internet

**Thời lượng:** 0 phút 45 giây.

**Nội dung trên slide:**

- Công bố ngày 14/03/2006
- Cung cấp lưu trữ qua giao diện web service
- Cho lập trình viên dùng hạ tầng có thể mở rộng
- Giảm công việc tự xây và quản lý hạ tầng

**Lời thuyết trình:**

Amazon công bố S3 ngày 14 tháng 3 năm 2006. Thông điệp khi ra mắt là cung cấp một giao diện đơn giản để lập trình viên lưu và lấy dữ liệu qua Internet trên hạ tầng có khả năng mở rộng. Điều đáng nhớ ở đây là cách sử dụng: người làm ứng dụng gọi dịch vụ thay vì phải bắt đầu bằng việc sở hữu một hệ thống lưu trữ. Từ góc nhìn bài học, S3 thể hiện ý tưởng sử dụng tài nguyên khi cần. Các con số giá hoặc giới hạn xuất hiện trong thông báo năm 2006 chỉ có ý nghĩa lịch sử, không dùng để mô tả dịch vụ hiện nay.

**Gợi ý hình:** Một mốc thời gian lớn “14.03.2006”, nối sang biểu tượng API và bucket; không cần timeline dài.

**Nguồn:** [Amazon Press Center — Amazon Web Services Launches, 14/03/2006](https://press.aboutamazon.com/2006/3/amazon-web-services-launches).

## Slide 06 — S3 là gì?

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Dịch vụ lưu trữ đối tượng trên AWS
- Lưu ảnh, tài liệu, video và bản sao lưu
- Dữ liệu nằm trong bucket dưới dạng object
- Truy cập bằng Console hoặc API

**Lời thuyết trình:**

Tên đầy đủ của S3 là Amazon Simple Storage Service. Đây là dịch vụ lưu trữ đối tượng. Với ví dụ của nhóm, một tệp văn bản được tải lên sẽ trở thành một object trong bucket. Người dùng có thể thao tác bằng Console; các ứng dụng có thể dùng API hoặc công cụ lập trình để làm việc tương tự. S3 đảm nhiệm việc lưu trữ, còn nội dung và cách sử dụng dữ liệu do chúng ta quyết định. Vì vậy, khi muốn xây một hệ thống lớn hơn, S3 thường đóng vai trò nơi chứa dữ liệu và kết hợp với những thành phần xử lý hoặc hiển thị khác.

**Gợi ý hình:** “Tệp trên máy → Bucket S3 → Người dùng/ứng dụng”; dưới bucket đặt nhãn “Object storage”.

**Nguồn:** [AWS User Guide — What is Amazon S3?](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html).

## Slide 07 — Object, file và block khác nhau ở cách làm việc

**Thời lượng:** 1 phút 15 giây.

**Nội dung trên slide:**

- File: tổ chức theo tệp và thư mục
- Block: đọc/ghi các khối trên một volume
- Object: dữ liệu, metadata và định danh
- Ví dụ AWS: EFS · EBS · S3

**Lời thuyết trình:**

Có thể phân biệt ba cách lưu bằng đơn vị mà người dùng làm việc. File storage cho ứng dụng làm việc với tệp và cây thư mục. Block storage cung cấp các khối dữ liệu của một volume, thường dùng cùng hệ điều hành hoặc cơ sở dữ liệu. Object storage lưu một đơn vị dữ liệu cùng thông tin mô tả và định danh để truy cập. Ví dụ trong AWS lần lượt là EFS, EBS và S3. Trong demo, chúng ta chọn object bằng key rồi tải xuống hoặc tải bản mới lên. Hiểu đơn vị truy cập sẽ giúp tránh chọn dịch vụ chỉ vì thấy tất cả đều có thể chứa dữ liệu.

**Gợi ý hình:** Bảng ba cột với hình cây thư mục, các ô khối và một thẻ object; mỗi cột có một ví dụ dịch vụ.

**Nguồn:** [AWS — Block vs. File vs. Object Storage](https://aws.amazon.com/compare/the-difference-between-block-file-object-storage/).

## Slide 08 — Bucket: Nơi chứa và cấu hình chung

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Tạo bucket trước khi tải object
- Chọn tên và một AWS Region
- Quyền truy cập và Versioning đặt ở cấp bucket
- Demo dùng một general purpose bucket riêng tư

**Lời thuyết trình:**

Bucket là tài nguyên chứa các object và nhiều cấu hình chung của chúng. Khi tạo, chúng ta chọn Region và đặt tên theo quy tắc tương ứng. Nếu dùng shared global namespace, tên cần duy nhất trong AWS partition; nhóm sẽ dùng tên riêng khi thực hành. Sau đó, các lựa chọn như Versioning và chặn truy cập công khai được kiểm tra trên bucket này. Hãy coi bucket là ranh giới quản lý của demo: mọi tệp thử nghiệm đều nằm trong cùng một nơi, giúp theo dõi quyền và dọn tài nguyên sau buổi học. Một bucket là đủ cho ba chức năng đã chọn.

**Gợi ý hình:** Khung bucket chứa ba thẻ object; phía ngoài gắn nhãn “Region”, “Quyền”, “Versioning”. Ảnh minh họa dự kiến: `assets/demo/01-bucket-rieng-tu.jpg`.

**Nguồn:** [AWS User Guide — General purpose buckets overview](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingBucket.html).

## Slide 09 — Bên trong một object có gì?

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Dữ liệu: nội dung tệp
- Key: tên dùng để tìm object
- Metadata: thông tin mô tả
- Version ID: phân biệt các phiên bản

**Lời thuyết trình:**

Với tệp kế hoạch, phần dữ liệu là những dòng văn bản mà chúng ta đọc. Key là tên được sử dụng để truy cập object trong bucket. Metadata mô tả object, chẳng hạn loại nội dung; AWS cũng quản lý một số thông tin hệ thống để vận hành object. Khi bật Versioning, version ID giúp phân biệt các bản cùng key. Trong phần demo, tên vẫn giữ nguyên nhưng nội dung thay đổi, nên chỉ nhìn tên sẽ chưa đủ để biết lịch sử. Bốn thành phần trên giúp chúng ta đọc đúng trang chi tiết object và hiểu vì sao S3 có thể giữ nhiều bản của cùng một tên.

**Gợi ý hình:** Một thẻ object chia bốn hàng: “Nội dung”, “Key”, “Metadata”, “Version ID”; dùng ví dụ `ke-hoach-nhom.txt`.

**Nguồn:** [AWS User Guide — Amazon S3 objects overview](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingObjects.html).

## Slide 10 — Key và prefix: Hiểu đúng “thư mục” trên Console

**Thời lượng:** 1 phút 15 giây.

**Nội dung trên slide:**

- Key xác định object trong bucket
- `tai-lieu/ke-hoach.txt` là một key đầy đủ
- Prefix giúp nhóm các key có phần đầu giống nhau
- Demo dùng key gốc `ke-hoach-nhom.txt`

**Lời thuyết trình:**

Trong general purpose bucket, mô hình key là phẳng. Console có thể trình bày thành các folder nhờ prefix và dấu gạch chéo trong tên key. Ví dụ, phần tai-lieu ở đầu tên giúp giao diện nhóm các object có liên quan. Với demo này, chúng ta đặt ke-hoach-nhom.txt ngay ở gốc bucket để việc ghi đè và theo dõi phiên bản thật rõ. Hai tệp trên máy nằm trong samples/v1 và samples/v2 có cùng tên; khi tải lên đúng gốc, chúng cùng trỏ tới một key. Nếu vô tình tải vào hai prefix khác nhau, chúng sẽ thành hai key khác nhau.

**Gợi ý hình:** Hai ô so sánh: key `ke-hoach-nhom.txt` và key `tai-lieu/ke-hoach-nhom.txt`; tô màu phần prefix.

**Nguồn:** [AWS User Guide — Naming Amazon S3 objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-keys.html).

## Slide 11 — Region và Availability Zone: Dữ liệu được đặt ở đâu?

**Thời lượng:** 1 phút 15 giây.

**Nội dung trên slide:**

- Region: một khu vực địa lý của AWS
- AZ: một hoặc nhiều trung tâm dữ liệu tách biệt
- S3 Standard lưu dữ liệu trên ít nhất ba AZ
- Chọn Region theo vị trí, chi phí và yêu cầu dữ liệu

**Lời thuyết trình:**

Region là khu vực địa lý nơi AWS tập hợp các trung tâm dữ liệu. Bên trong có nhiều Availability Zone, được thiết kế tách biệt về hạ tầng. Khi dùng S3 Standard, dữ liệu được lưu dự phòng trên ít nhất ba AZ trong Region. Nhóm chọn Region khi tạo bucket và kiểm tra lại trước demo. Hình này chỉ thể hiện một Region; nó không có nghĩa S3 tự sao chép dữ liệu của nhóm tới mọi nơi trên thế giới. Nếu cần bản sao ở Region khác, phải có thiết kế và cấu hình tương ứng. Với bài học này, một Region là đủ để quan sát mô hình nhiều AZ.

**Gợi ý hình:** Một khung Region chứa ba khung AZ; cùng một object xuất hiện bằng nét mờ ở cả ba. Không vẽ ba quốc gia.

**Nguồn:** [AWS — Regions and Availability Zones](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/); [AWS — S3 storage class comparison](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html).

## Slide 12 — Bốn thao tác cơ bản với object

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- PUT: ghi object
- GET: lấy nội dung object
- LIST: xem danh sách object
- DELETE: xóa theo trạng thái Versioning

**Lời thuyết trình:**

Các thao tác trên Console có thể liên hệ với những yêu cầu cơ bản này. Khi tải tệp nhỏ lên, chúng ta đang ghi object. Khi tải xuống, chúng ta lấy nội dung của object. Khi mở danh sách, giao diện yêu cầu liệt kê object trong bucket. Xóa cần xem trạng thái Versioning: có thể xóa dữ liệu hoặc tạo dấu xóa thay vì xóa bản cũ ngay. Demo chủ yếu dùng ghi, đọc và liệt kê; chức năng khôi phục sẽ tải phiên bản cũ rồi ghi lại thành phiên bản mới. Gọi đúng tên thao tác giúp giải thích cả hành vi, quyền cần có và nguồn phát sinh chi phí.

**Gợi ý hình:** Bốn mũi tên quanh bucket, mỗi mũi tên gắn một động từ; đánh dấu PUT, GET và LIST là thao tác sẽ quan sát.

**Nguồn:** AWS API Reference: [PutObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_PutObject.html), [GetObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_GetObject.html), [ListObjectsV2](https://docs.aws.amazon.com/AmazonS3/latest/API/API_ListObjectsV2.html), [DeleteObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_DeleteObject.html).

## Slide 13 — Khả năng mở rộng: Tăng dữ liệu mà ít quản trị phần cứng

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Lưu số lượng object theo nhu cầu
- AWS vận hành hạ tầng lưu trữ bên dưới
- Hiệu năng mở rộng theo tải và thiết kế truy cập
- Mạng, kích thước tệp và cách dùng vẫn ảnh hưởng

**Lời thuyết trình:**

Với một tệp nhỏ, lợi ích mở rộng chưa nổi bật. Hãy tưởng tượng nhu cầu tăng thành nhiều ảnh, video hoặc dữ liệu của nhiều người dùng. Dịch vụ giúp nhóm tránh tự thay ổ đĩa mỗi lần dữ liệu tăng. Tuy nhiên, mở rộng không đồng nghĩa mọi yêu cầu đều nhanh như nhau. Tốc độ còn chịu ảnh hưởng của đường truyền, kích thước dữ liệu và cách tổ chức truy cập. Tài liệu AWS cũng lưu ý việc thích nghi với tải tăng diễn ra dần. Vì vậy, trong bài này nhóm kiểm chứng chức năng bằng tệp nhỏ; chúng em không dùng kết quả đó để kết luận về hiệu năng của hệ thống lớn.

**Gợi ý hình:** Ba bucket minh họa quy mô dữ liệu tăng dần và một mũi tên; thêm biểu tượng mạng ở phía người dùng.

**Nguồn:** [AWS User Guide — Optimizing Amazon S3 performance](https://docs.aws.amazon.com/AmazonS3/latest/userguide/optimizing-performance.html); [AWS — Uploading objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html).

## Slide 14 — Giữ được dữ liệu và truy cập được dữ liệu là hai việc

**Thời lượng:** 1 phút 30 giây.

**Nội dung trên slide:**

- Durability: khả năng giữ dữ liệu lâu dài
- Availability: khả năng truy cập khi cần
- S3 Standard: thiết kế 99.999999999% độ bền
- S3 Standard: thiết kế 99.99% độ sẵn sàng
- Versioning vẫn cần để xử lý ghi đè nhầm

**Lời thuyết trình:**

Một tài liệu có thể vẫn còn nguyên nhưng chúng ta tạm thời không lấy được; đó là lý do phải tách hai khái niệm. Durability liên quan đến việc dữ liệu có bị mất hay không. Availability liên quan đến khả năng dịch vụ đáp ứng truy cập. AWS công bố S3 Standard được thiết kế cho độ bền mười một số chín và độ sẵn sàng 99,99 phần trăm trong năm. Đây là mục tiêu thiết kế, không phải lời hứa rằng mọi tình huống đều an toàn tuyệt đối. Nếu người có quyền ghi đè nội dung, độ bền hạ tầng không giúp chọn lại nội dung đúng; Versioning sẽ phục vụ nhu cầu đó.

**Gợi ý hình:** Hai thẻ lớn: “Dữ liệu còn?” và “Lấy được lúc này?”; đặt hai tỷ lệ tương ứng, làm nổi chữ “S3 Standard”.

**Nguồn:** [AWS User Guide — Data protection in Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/DataDurability.html).

## Slide 15 — Strong consistency: Ghi thành công, đọc được bản mới

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Ghi mới thành công → đọc thấy object
- Ghi đè thành công → đọc thấy bản mới
- LIST phản ánh thay đổi đã thành công
- Không đồng nghĩa mọi bản sao xuyên Region tức thời

**Lời thuyết trình:**

Tính nhất quán trả lời câu hỏi: sau khi lưu thành công, lần đọc tiếp theo sẽ thấy gì? Với các thao tác object đang xét, S3 cung cấp strong read-after-write consistency. Sau khi ghi mới hoặc ghi đè thành công, các lần đọc sau nhận dữ liệu mới nhất; LIST cũng phản ánh thay đổi. Trong demo, chúng ta dùng điều này để mở bản vừa tải lên và kiểm tra nội dung. Tuy nhiên, cần bắt đầu từ phản hồi thành công của thao tác ghi. Khái niệm này không thay thế việc xác nhận upload, cũng không nói rằng mọi thay đổi cấu hình hay sao chép sang Region khác đều diễn ra ngay lập tức.

**Gợi ý hình:** Trục thời gian “PUT thành công → GET → bản mới”, bên dưới “LIST → có thay đổi”; không thêm thời gian chờ giả định.

**Nguồn:** [AWS — Amazon S3 Strong Consistency](https://aws.amazon.com/s3/consistency/).

## Slide 16 — Trách nhiệm được chia giữa AWS và người dùng

**Thời lượng:** 1 phút 15 giây.

**Nội dung trên slide:**

- AWS: hạ tầng chạy dịch vụ
- Người dùng: dữ liệu và người được truy cập
- Người dùng: cấu hình, vòng đời và cách sử dụng
- Bảo mật cần cả dịch vụ lẫn lựa chọn đúng

**Lời thuyết trình:**

S3 là dịch vụ được quản lý, nhưng người dùng vẫn có trách nhiệm. AWS bảo vệ và vận hành hạ tầng chạy dịch vụ. Phía nhóm cần biết dữ liệu nào được đưa lên, ai được phép đọc hoặc ghi, và cấu hình nào đang được áp dụng. Một ví dụ dễ hiểu là AWS cung cấp khả năng chặn public, còn chúng ta phải chọn cách chia sẻ phù hợp với tài liệu. Trong demo, nhóm chủ động giữ bucket riêng tư, kiểm tra Versioning và chỉ chia sẻ object mẫu trong thời gian ngắn. Cách chia trách nhiệm này giải thích vì sao dùng đám mây vẫn phải học cấu hình và hiểu hậu quả của từng thay đổi.

**Gợi ý hình:** Hai nửa chiếc khiên: “AWS: hạ tầng” và “Nhóm: dữ liệu + quyền + cấu hình”; không cần liệt kê dịch vụ bảo mật khác.

**Nguồn:** [AWS User Guide — Security in Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security.html).

## Slide 17 — Ai được làm gì? Ba công cụ cần phân biệt

**Thời lượng:** 1 phút 15 giây.

**Nội dung trên slide:**

- IAM policy: quyền gắn với danh tính
- Bucket policy: quy tắc gắn với bucket
- Block Public Access: lớp chặn truy cập công khai
- Cấp đúng quyền cần dùng, kiểm tra trước khi chia sẻ

**Lời thuyết trình:**

IAM policy giúp mô tả một danh tính được phép thực hiện hành động nào. Bucket policy đặt quy tắc ngay trên tài nguyên bucket và object liên quan. Block Public Access bổ sung các cơ chế ngăn việc công khai ngoài ý muốn. Khi xét quyền, phải xem các lớp liên quan cùng nhau, vì một cấu hình ở bucket chưa kể hết điều kiện hiệu lực. Nhóm không cần viết một chính sách công khai để thực hiện demo. Chúng ta giữ các tùy chọn chặn public và dùng quyền của người tạo để cấp liên kết tạm thời. Mục tiêu của phần này là phân biệt nơi đặt quyền với quyết định công khai dữ liệu.

**Gợi ý hình:** Ba lớp cửa: “Danh tính → Quy tắc tài nguyên → Chặn public”; chèn vùng đã che thông tin của `assets/demo/01-bucket-rieng-tu.jpg` khi có.

**Nguồn:** [AWS User Guide — Access control in Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-management.html); [AWS — Configuring Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/userguide/configuring-block-public-access-bucket.html).

## Slide 18 — Mã hóa: Bảo vệ dữ liệu khi lưu và khi truyền

**Thời lượng:** 0 phút 45 giây.

**Nội dung trên slide:**

- Object mới có mã hóa phía máy chủ mặc định
- Demo dùng SSE-S3, khóa do S3 quản lý
- Truy cập bằng HTTPS để bảo vệ đường truyền
- Quyền truy cập vẫn phải cấu hình đúng

**Lời thuyết trình:**

Mã hóa có hai ngữ cảnh cần nhớ: khi dữ liệu đang được lưu và khi dữ liệu đi trên đường truyền. Với demo, nhóm dùng SSE-S3, mức mã hóa nền tảng cho object tải lên mới, và truy cập qua HTTPS. Điều cần tránh nhầm là xem mã hóa như một quyết định cấp quyền. Nếu một người đã được phép đọc object, dịch vụ có thể trả nội dung cho người đó theo quyền. Vì vậy, câu hỏi dữ liệu có được mã hóa hay không luôn đi cùng câu hỏi ai được đọc. Nhóm sẽ chỉ kiểm tra cấu hình cần dùng, không mở thêm phần quản lý khóa nâng cao.

**Gợi ý hình:** Máy người dùng nối tới bucket bằng đường “HTTPS”; trong bucket có biểu tượng khóa “SSE-S3”.

**Nguồn:** [AWS — Default encryption FAQ](https://docs.aws.amazon.com/AmazonS3/latest/userguide/default-encryption-faq.html); [AWS — Security best practices for S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html).

## Slide 19 — Versioning: Cùng key, nhiều phiên bản

**Thời lượng:** 1 phút 15 giây.

**Nội dung trên slide:**

- Bật Versioning trước khi thử ghi đè
- Cùng key, nội dung mới → phiên bản mới
- Chọn version ID để đọc bản trước
- Khôi phục v1 bằng tải về rồi upload thành v3
- Mỗi phiên bản tiếp tục dùng dung lượng

**Lời thuyết trình:**

Versioning giúp lưu nhiều bản của cùng object. Trong demo, bản đầu là kế hoạch ban đầu; bản thứ hai mô phỏng nội dung đã bị sửa. Vì cùng key và bucket đã bật Versioning, S3 giữ cả hai bản với version ID khác nhau. Để phục hồi, nhóm tải đúng bản đầu về, kiểm tra nội dung rồi upload lại cùng key. Kết quả là một phiên bản thứ ba có nội dung của bản đầu; lịch sử hai bản trước vẫn còn. Chúng em dùng v1, v2 và v3 làm cách gọi dễ hiểu, còn version ID thực tế do S3 tạo. Các bản được giữ lại đều phải tính vào dung lượng.

**Gợi ý hình:** Dòng thời gian “v1 → v2 → v3”, với mũi tên từ nội dung v1 sang v3; gắn nhãn “cùng key”.

**Nguồn:** [AWS — S3 Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html); [AWS — Restoring previous versions](https://docs.aws.amazon.com/AmazonS3/latest/userguide/RestoringPreviousVersions.html).

## Slide 20 — Storage class: Chọn theo tần suất và tốc độ cần đọc

**Thời lượng:** 1 phút 15 giây.

**Nội dung trên slide:**

- Standard: truy cập thường xuyên, phù hợp demo
- Intelligent-Tiering: tần suất khó dự đoán
- Standard-IA / One Zone-IA: ít truy cập
- Glacier: nhiều mức truy xuất để lưu trữ dài hạn
- So cả phí đọc, thời gian chờ và khả năng chịu lỗi

**Lời thuyết trình:**

S3 có nhiều lớp vì dữ liệu không phải lúc nào cũng được dùng như nhau. Tệp đang làm việc cần truy cập thường xuyên, nên Standard dễ phù hợp. Với dữ liệu ít dùng, có thể xem các lớp IA; nếu tần suất khó dự đoán, Intelligent-Tiering hỗ trợ chuyển tier theo cách sử dụng. Nhóm Glacier phục vụ lưu trữ dài hạn với các lựa chọn truy xuất khác nhau. Chọn lớp cần xét cả giá lưu, phí lấy dữ liệu, thời gian chờ và số AZ. Trong demo ngắn, nhóm giữ Standard để tập trung vào chức năng; việc chuyển lớp chỉ để minh họa có thể tạo thêm điều kiện tính phí không cần thiết.

**Gợi ý hình:** Bảng bốn hàng “Đang dùng / Khó dự đoán / Ít dùng / Archive”; ghi chú nhỏ “One Zone: cân nhắc mất AZ”.

**Nguồn:** [AWS User Guide — Understanding and managing Amazon S3 storage classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html).

## Slide 21 — Lifecycle: Đặt quy tắc cho dữ liệu theo thời gian

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Tự chuyển lớp khi dữ liệu đủ điều kiện
- Tự hết hạn theo quy tắc đã đặt
- Có thể quản lý cả các phiên bản cũ
- Phải xét thời gian lưu và chi phí chuyển lớp

**Lời thuyết trình:**

Lifecycle là tập quy tắc giúp xử lý dữ liệu theo vòng đời. Ví dụ về mặt ý tưởng, tài liệu đang làm việc được giữ ở lớp truy cập thường xuyên; sau khi ít dùng, có thể chuyển sang lớp phù hợp hơn; hết thời gian cần giữ thì áp dụng quy tắc hết hạn. Với Versioning, cần xem cả phiên bản hiện tại lẫn các bản cũ. Những mốc thời gian phải dựa vào nhu cầu thật và điều kiện của lớp lưu trữ. Nhóm chỉ giải thích nguyên lý ở đây, vì Lifecycle không phải chức năng cần chứng minh trong vài phút demo và có thể tác động đến dữ liệu đang có.

**Gợi ý hình:** Trục “Đang dùng → Ít dùng → Archive → Hết hạn”; để mốc “theo nhu cầu” thay vì đưa lịch mặc định.

**Nguồn:** [AWS User Guide — Managing the lifecycle of objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html).

## Slide 22 — Chi phí: Không chỉ có dung lượng lưu

**Thời lượng:** 1 phút 15 giây.

**Nội dung trên slide:**

- Dung lượng và thời gian lưu, kể cả phiên bản cũ
- Requests: ghi, đọc, liệt kê và thao tác liên quan
- Retrieval, truyền dữ liệu và tính năng bổ sung
- Free Tier phụ thuộc tài khoản và điều kiện hiện hành
- Demo nhỏ, Standard; theo dõi Billing và dọn sau học

**Lời thuyết trình:**

Khi ước tính tiền, cần xét cách sử dụng chứ không chỉ kích thước tệp. S3 có nhóm phí lưu trữ, requests, lấy dữ liệu và truyền dữ liệu, cùng tính năng bổ sung nếu bật. Ngay cả duyệt bucket bằng Console cũng tạo requests. Giá còn phụ thuộc Region và lớp lưu trữ. Free Tier hiện có chương trình credits cho tài khoản mới, nên không áp dụng mặc định hướng dẫn cũ cho mọi tài khoản. Với bài học, nhóm dùng vài tệp nhỏ, ít thao tác và Standard để kiểm soát phạm vi. Sau buổi trình bày vẫn cần kiểm tra Billing và dọn cả các phiên bản cũ.

**Gợi ý hình:** Bốn ô chi phí và dòng dưới “Tổng phụ thuộc cách dùng”; ảnh nhỏ của Billing chỉ chèn nếu đã che thông tin.

**Nguồn:** [AWS — Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/); [AWS Billing — Explore AWS services with AWS Free Tier](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier.html).

## Slide 23 — Ưu điểm: Những việc S3 làm tốt

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Giảm việc tự vận hành hạ tầng lưu trữ
- Mở rộng theo nhu cầu dữ liệu
- Nhiều lựa chọn bảo vệ và quản lý object
- Truy cập qua công cụ hoặc tích hợp vào ứng dụng

**Lời thuyết trình:**

Từ các phần trước, có thể tổng hợp bốn ưu điểm chính. Thứ nhất, người dùng tập trung vào dữ liệu nhiều hơn vì không tự quản lý ổ đĩa của dịch vụ. Thứ hai, mô hình phù hợp khi số lượng dữ liệu tăng. Thứ ba, các lựa chọn như Versioning, mã hóa và kiểm soát truy cập hỗ trợ nhu cầu vận hành khác nhau. Cuối cùng, có thể bắt đầu bằng Console rồi tích hợp bằng API khi cần. Đây là các khả năng của dịch vụ; để nhận được giá trị, người dùng vẫn phải chọn cấu hình hợp lý. Demo sẽ cho thấy ba lợi ích cụ thể thay vì chỉ đọc danh sách tính năng.

**Gợi ý hình:** Bốn thẻ biểu tượng “Hạ tầng”, “Mở rộng”, “Bảo vệ”, “Tích hợp”; mỗi thẻ chỉ có một câu ngắn.

**Nguồn:** Tổng hợp từ các slide 06, 13, 16–19; đối chiếu [AWS — Amazon S3](https://aws.amazon.com/s3/).

## Slide 24 — Hạn chế: Khi nào phải cân nhắc thêm?

**Thời lượng:** 1 phút 15 giây.

**Nội dung trên slide:**

- Truy cập object khác cách làm việc trên ổ đĩa
- Phụ thuộc mạng và độ trễ
- Nhiều lớp phí, cần hiểu cách sử dụng
- Sai quyền hoặc quy tắc có thể gây hậu quả
- Archive có thể cần chờ để lấy dữ liệu

**Lời thuyết trình:**

Chọn S3 cần nhìn cả điểm phải đánh đổi. Ứng dụng quen thao tác với volume hoặc giao thức file có thể cần thiết kế khác khi làm việc với API object. Người dùng ở xa hoặc mạng yếu cũng có trải nghiệm khác nhau. Giá lưu thấp hơn ở một lớp chưa chắc làm tổng chi phí thấp hơn nếu thường xuyên lấy dữ liệu. Ngoài ra, quyền truy cập và quy tắc vòng đời phải được kiểm tra cẩn thận. Nếu chọn lớp archive, cần xem thời gian khôi phục. Vì vậy, nhóm chọn Standard và tệp nhỏ cho bài học, còn một dự án thật cần đánh giá đúng kiểu truy cập và yêu cầu của người dùng.

**Gợi ý hình:** Bảng “Nhu cầu cần hỏi” gồm giao thức, mạng, chi phí, quyền và thời gian đọc; không dùng biểu tượng cảnh báo quá nhiều.

**Nguồn:** [AWS — Block, file, object comparison](https://aws.amazon.com/compare/the-difference-between-block-file-object-storage/); [AWS — Storage classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html); [AWS — S3 Pricing](https://aws.amazon.com/s3/pricing/).

## Slide 25 — Ứng dụng thực tế: Từ tệp nhóm đến dữ liệu lớn

**Thời lượng:** 1 phút.

**Nội dung trên slide:**

- Lưu ảnh, tài liệu và nội dung ứng dụng
- Backup và khôi phục dữ liệu
- Lưu trữ lâu dài ít truy cập
- Data lake và dữ liệu đầu vào phân tích

**Lời thuyết trình:**

Bài toán tệp nhóm là ví dụ nhỏ của nhiều cách sử dụng rộng hơn. Một ứng dụng có thể lưu ảnh và tài liệu trên S3. Một hệ thống khác dùng S3 làm nơi giữ bản sao lưu hoặc dữ liệu cần lưu lâu. Trong phân tích, S3 còn được dùng làm nơi tập trung dữ liệu cho các công cụ xử lý phía sau. Hãy phân biệt nơi chứa với chức năng xử lý: việc có dữ liệu trong bucket chưa tự tạo ra báo cáo, giao diện hay luồng công việc. Nhóm chọn phạm vi lưu và chia sẻ để có thể giải thích đầy đủ từ cấu hình tới kết quả quan sát được.

**Gợi ý hình:** Bucket ở giữa, bốn nhánh “Nội dung”, “Backup”, “Archive”, “Phân tích”; đặt demo nhóm ở góc như ví dụ đơn giản.

**Nguồn:** [AWS — Amazon S3 use cases](https://aws.amazon.com/s3/); [AWS User Guide — What is Amazon S3?](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html).

## Slide 26 — Sản phẩm demo: Kho tài liệu nhóm trên AWS Console

**Thời lượng:** 0 phút 45 giây.

**Nội dung trên slide:**

- Một general purpose bucket, S3 Standard
- Riêng tư · Versioning bật · SSE-S3
- Key gốc: `ke-hoach-nhom.txt`
- Ba chức năng: lưu, phục hồi, chia sẻ tạm thời
- GitHub chứa tài liệu, mẫu và bằng chứng đã che thông tin

**Lời thuyết trình:**

Đây là kiến trúc đầy đủ của sản phẩm trong bài học. Người thao tác đăng nhập AWS Console để quản lý một bucket riêng tư. Tệp mẫu trên máy được tải lên cùng một key. Khi chia sẻ tạm thời, người nhận dùng trình duyệt mở presigned URL để đọc object theo quyền được cấp. GitHub lưu hướng dẫn tái hiện, tệp mẫu và ảnh kết quả đã xử lý thông tin nhạy cảm; việc đẩy repository không tự triển khai bucket. Sản phẩm thuộc dạng cấu hình dịch vụ trên Console, nên phần cần hiểu là tài nguyên, quyền, các thao tác và kết quả. Không có mã HTML hay Python cần giải thích trong phạm vi này.

**Gợi ý hình:** “Máy nhóm → AWS Console → S3”; một nhánh “Người nhận ← URL có hạn ← S3”; GitHub đặt riêng để chứa tài liệu. Ảnh dự kiến: `assets/demo/01-bucket-rieng-tu.jpg`.

**Nguồn:** Kiến trúc demo do nhóm thiết kế; cơ chế Console/API tại [AWS — General purpose buckets overview](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingBucket.html).

## Slide 27 — Demo 1: Tải lên và lấy lại đúng nội dung

**Thời lượng:** 2 phút, gồm thao tác trực tiếp.

**Nội dung trên slide:**

- Kiểm tra bucket, Region và Versioning
- Upload `samples/v1/ke-hoach-nhom.txt` vào gốc
- Quan sát object có key `ke-hoach-nhom.txt`
- Download, mở tệp và đối chiếu nội dung v1

**Lời thuyết trình:**

Trước khi tải lên, nhóm chỉ ra bucket đang dùng và trạng thái Versioning. Tiếp theo, em chọn tệp trong samples/v1 rồi upload ngay tại gốc bucket. Tên object cần thấy là ke-hoach-nhom.txt. Khi Console báo thành công, em mở danh sách, chọn object và tải về. Nhóm mở tệp vừa nhận để đọc một chi tiết của kế hoạch, rồi đối chiếu với bản mẫu đầu tiên. Như vậy, kết quả được kiểm chứng bằng nội dung cụ thể. Đây là luồng ghi và đọc đơn giản nhất. Bucket vẫn riêng tư; thao tác tải xuống thành công do phiên đăng nhập hiện tại có quyền phù hợp.

**Gợi ý hình:** Chèn `assets/demo/02-upload-thanh-cong.jpg` cạnh hai trạng thái “Trên máy” và “Trong bucket”. Khi trình chiếu, chuyển sang Console thật.

**Nhịp thao tác cho người demo:** 20 giây kiểm tra cấu hình; 40 giây upload và quan sát key; 45 giây download và mở nội dung; 15 giây chốt kết quả. Tệp tải xuống có thể được trình duyệt thêm hậu tố tên; kiểm tra đúng bản mới nhận.

**Nguồn:** [AWS — Uploading objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html); [AWS — Downloading objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/download-objects.html).

## Slide 28 — Demo 2: Phục hồi bản đầu mà vẫn giữ lịch sử

**Thời lượng:** 3 phút, gồm thao tác trực tiếp.

**Nội dung trên slide:**

- Upload `samples/v2/ke-hoach-nhom.txt` cùng key
- Xem hai version và đọc nội dung v2
- Chọn đúng v1 trên S3, tải về và kiểm tra
- Upload bản vừa phục hồi cùng key để tạo v3
- Bản hiện tại có nội dung v1; lịch sử vẫn còn

**Lời thuyết trình:**

Bây giờ em tải tệp trong samples/v2 vào đúng gốc và cùng key. Nhóm đọc bản hiện tại để thấy nội dung đã thay đổi. Trong danh sách phiên bản, em chọn bản đầu theo thời điểm và version ID, rồi tải chính bản đó từ S3 về. Sau khi mở kiểm tra, em bảo đảm tệp vẫn mang tên ke-hoach-nhom.txt và upload lại cùng key. S3 tạo phiên bản thứ ba. Khi tải bản hiện tại xuống, nội dung khớp v1, còn danh sách vẫn giữ các bản trước. Đây là phục hồi nội dung bằng một lần ghi mới; chúng ta chứng minh được lịch sử mà không phải xóa phiên bản nào.

**Gợi ý hình:** Hai ảnh cạnh nhau: `assets/demo/03-cac-phien-ban.jpg` và `assets/demo/04-khoi-phuc-v1.jpg`; dùng mũi tên “Tải v1 từ S3 → Upload cùng key → v3”.

**Nhịp thao tác cho người demo:** 45 giây upload/đọc v2; 45 giây mở Versions và download đúng v1; 45 giây kiểm tra, sửa lại basename nếu trình duyệt thêm hậu tố, upload thành v3; 45 giây kiểm tra nội dung hiện tại và ba versions. Không dùng tệp v1 có sẵn trên máy để thay cho bước tải bản cũ từ S3, vì sẽ không chứng minh khả năng lấy lại dữ liệu đang lưu.

**Nguồn:** [AWS — Restoring previous versions](https://docs.aws.amazon.com/AmazonS3/latest/userguide/RestoringPreviousVersions.html); [AWS — Uploading objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html).

## Slide 29 — Demo 3: Chia sẻ đọc tạm thời, bucket vẫn riêng tư

**Thời lượng:** 2 phút 30 giây, gồm thao tác và chờ hết hạn.

**Nội dung trên slide:**

- Mở Object URL thường trong cửa sổ riêng tư: bị chặn
- Tạo presigned URL đọc, thời hạn 1 phút
- Mở link tạm thời: đọc được object
- Sau hạn, tạo request mới: truy cập bị từ chối
- Block Public Access vẫn bật

**Lời thuyết trình:**

Đầu tiên, nhóm mở Object URL thông thường trong cửa sổ riêng tư để thấy người chưa được cấp quyền bị từ chối. Sau đó, em tạo presigned URL cho object hiện tại, chọn một phút và mở để kiểm tra nội dung. Trong lúc chờ, cần hiểu rằng ai có link hợp lệ đều có thể dùng quyền đọc tạm thời này. Link không chỉ dùng một lần. Sau thời hạn, em mở request mới ở cửa sổ riêng tư mới để tránh nhầm với nội dung đã tải. Kết quả mong đợi là bị từ chối. Bucket vẫn riêng tư; thời gian hiệu lực còn phụ thuộc credentials tạo link.

**Gợi ý hình:** Ba trạng thái “Link thường: chặn → Link tạm: được → Hết hạn: chặn”. Ảnh dự kiến: `assets/demo/05-truy-cap-bi-chan.jpg`, `assets/demo/06-link-tam-thoi.jpg`, `assets/demo/07-link-het-han.jpg`; che toàn bộ query có chữ ký.

**Nhịp thao tác cho người demo:** 20 giây mở link thường; 25 giây tạo và thử presigned URL; dùng khoảng chờ để giải thích quyền và xem lại Block Public Access; sau thời điểm tạo hơn 60 giây, mở URL bằng request mới; dành thời gian còn lại đối chiếu kết quả. Không chờ bằng cách chỉ nhìn tab đã mở, vì nội dung đó không tự biến mất. Không đưa link còn hiệu lực vào slide hoặc GitHub.

**Nguồn:** [AWS — Download and upload objects with presigned URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html); [AWS — Sharing objects with presigned URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html).

## Slide 30 — Ba điều cần nhớ và trao đổi với thầy

**Thời lượng:** 1 phút, gồm kết luận và một câu hỏi ngắn.

**Nội dung trên slide:**

- S3 lưu object theo bucket và key
- Versioning giữ lịch sử; presigned URL chia sẻ có hạn
- Dùng đúng quyền, lớp lưu trữ và cách tính phí
- Câu hỏi: Vì sao URL thường bị chặn mà link tạm mở được?
- GitHub: https://github.com/st4rlight3/amazon-s3-kho-tai-lieu-demo

**Lời thuyết trình:**

Từ một tệp nhỏ, nhóm đã đi qua mô hình object, cấu hình bảo mật và cách kiểm chứng kết quả. Ba thao tác demo liên hệ trực tiếp với nhu cầu ban đầu: lưu tập trung, lấy lại nội dung cũ và chia sẻ trong một khoảng thời gian. Nếu thầy hỏi vì sao link thường bị chặn mà link tạm mở được, câu trả lời là presigned URL mang chữ ký và quyền có thời hạn của người tạo; bucket không cần trở thành công khai. Repository chứa tài liệu để người khác tái hiện. Sau buổi học, nhóm kiểm tra chi phí và dọn tài nguyên, gồm cả các phiên bản đã lưu.

**Gợi ý hình:** Ba biểu tượng “Object”, “Version”, “Quyền có hạn”; thêm QR repository. Repository hiện public, người xem có thể mở không cần đăng nhập GitHub; có thể đặt link tới tài liệu nguồn trong repository bằng chữ nhỏ. Bucket S3 của demo vẫn riêng tư.

**Nguồn:** Tổng hợp các phần đã trình bày; xem [Danh mục nguồn AWS đã đối chiếu](nguon-tham-khao.md).

---

**Kiểm tra trước khi đưa vào Canva:** đúng 30 trang; thay tên nhóm; kiểm tra link repository mở được không cần đăng nhập; ảnh demo phải lấy từ lần chạy thật; giữ các ghi chú thời gian ngoài phần hiển thị. Tổng thời lượng theo thứ tự slide: **0:30 + 1:00 + 0:30 + 1:00 + 0:45 + 1:00 + 1:15 + 1:00 + 1:00 + 1:15 + 1:15 + 1:00 + 1:00 + 1:30 + 1:00 + 1:15 + 1:15 + 0:45 + 1:15 + 1:15 + 1:00 + 1:15 + 1:00 + 1:15 + 1:00 + 0:45 + 2:00 + 3:00 + 2:30 + 1:00 = 35:30**. Nếu phần hỏi đáp kéo dài, dành thêm tối đa khoảng bốn phút để tổng buổi vẫn dưới 40 phút.
