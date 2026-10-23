# 2.2. Phân tích hệ thống nền tảng (Baseline)

> Giới hạn bằng chứng: chưa xác định được mã nguồn baseline thương mại điện tử mà nhóm lựa chọn. Mục 2.2.1 trình bày hiện trạng kho được cung cấp; mục 2.2.2 là khung phân tích cần hoàn thiện khi có baseline. Các yêu cầu mở rộng được nêu dưới đây chưa phải chức năng đã tồn tại hoặc kết quả triển khai.

## 2.2.1. Tổng quan và công nghệ sử dụng

### a) Khái niệm và phạm vi xác định baseline

Trong phạm vi đề tài, baseline phần mềm được hiểu là hệ thống thương mại điện tử có mã nguồn, cấu trúc dữ liệu và tập chức năng ban đầu mà nhóm kế thừa để phát triển chức năng gợi ý sản phẩm liên quan dựa trên hành vi người dùng. Việc phân tích baseline nhằm xác định ranh giới giữa chức năng có sẵn, chức năng cần điều chỉnh và phần đóng góp mới của nhóm. Quy định đồ án yêu cầu nhóm giải thích được kiến trúc, cơ sở dữ liệu và luồng xử lý của hệ thống được sử dụng; các chức năng đã có trong baseline không được coi là chức năng mới do nhóm xây dựng [13].

Baseline phần mềm cần được phân biệt với phương pháp đối chứng trong thực nghiệm gợi ý. Một ứng dụng thương mại điện tử có thể là nền tảng triển khai, trong khi các cách gợi ý như “cùng danh mục” hoặc “phổ biến” là những phương pháp đối chứng dùng để đánh giá thuật toán. Hai khái niệm có vai trò khác nhau và cần được mô tả riêng để tránh nhầm lẫn giữa mức độ hoàn thiện ứng dụng và chất lượng mô hình gợi ý.

### b) Hiện trạng kho mã đã kiểm chứng

Trong môi trường nghiên cứu hiện tại, kho `phong26052006-design/DiemCongPTUD` được kiểm tra tại commit `871a8e1de37d6cdc18593ce933748b14224c34e9`. Kết quả liệt kê cây mã nguồn cho thấy kho chỉ có tệp `README.md`, với nội dung tiêu đề dự án; chưa có mã nguồn ứng dụng, tệp khai báo phụ thuộc, cấu hình triển khai, migration hoặc tập lệnh khởi tạo cơ sở dữ liệu [14]. Đầu nhánh `main` trên remote tại thời điểm kiểm tra trùng với commit nói trên.

**Bảng 2.2. Hiện trạng bằng chứng về hệ thống nền tảng**

| Thành phần | Bằng chứng kiểm tra | Kết luận trong phạm vi kho được cung cấp |
|---|---|---|
| Định danh và phiên bản | Tên kho và commit Git đầy đủ | Xác định được ảnh chụp mã nguồn đang có |
| Giao diện | Chưa có HTML, template hoặc mã frontend trong cây Git | Chưa có căn cứ xác định công nghệ và trang chức năng |
| Backend | Chưa có mã server hoặc manifest ứng dụng | Chưa xác định ngôn ngữ, framework và cấu trúc xử lý |
| Phụ thuộc | Chưa có manifest/lockfile của ứng dụng | Chưa xác định phiên bản công cụ và thư viện |
| Cơ sở dữ liệu | Chưa có schema, model, migration hoặc SQL | Chưa xác định DBMS, thực thể và quan hệ thực tế |
| Chức năng thương mại điện tử | Chưa có controller/service/API/template tương ứng | Chưa thể xác nhận chức năng hiện có |
| Chức năng gợi ý | Chưa có module, endpoint, job hoặc mô hình gợi ý | Chưa có bằng chứng triển khai trong kho này |
| Kiểm thử và vận hành | Chưa có mã kiểm thử hoặc hướng dẫn chạy ứng dụng | Chưa thực hiện được kiểm thử chức năng của baseline |

*Nguồn: kiểm tra cây Git, commit và README của kho được cung cấp ngày 23/10/2026. Kết luận chỉ giới hạn ở kho và commit đã kiểm tra; không chứng minh rằng nhóm không có source ở một vị trí khác.*

Các bằng chứng hiện có chưa cho phép xác định ngôn ngữ, framework hoặc hệ quản trị cơ sở dữ liệu của ứng dụng. Những công nghệ xuất hiện trong tài liệu học phần và các trường hợp tham chiếu tại mục 2.1 chỉ cung cấp bối cảnh kỹ thuật; chưa xác lập lựa chọn công nghệ của nhóm.

### c) Nội dung cần bổ sung khi xác định được baseline

Khi có mã nguồn baseline, mô tả công nghệ cần dựa trên tệp cấu hình và cấu trúc thực tế thay vì chỉ dựa vào tên hệ thống hoặc thông tin quảng bá. Cụ thể, cần xác định: nguồn cung cấp và quyền sử dụng; phiên bản hoặc commit; ngôn ngữ và framework; thư viện truy cập dữ liệu; hệ quản trị cơ sở dữ liệu; công nghệ giao diện; cơ chế xác thực/phân quyền; các dịch vụ ngoài; và phương thức chạy hoặc triển khai. Những yếu tố này tạo cơ sở đánh giá khả năng tích hợp chức năng ghi nhận hành vi và cung cấp gợi ý.

Phân tích kiến trúc cần truy vết ít nhất luồng xem sản phẩm, giỏ hàng và đặt hàng từ giao diện đến backend và cơ sở dữ liệu. Đối với mỗi luồng, cần nêu điểm tiếp nhận yêu cầu, nơi kiểm tra quyền và dữ liệu, nơi thực hiện nghiệp vụ, đối tượng dữ liệu bị tác động và đầu ra trả về. Chỉ sau khi đọc mã và chạy kiểm tra phù hợp mới có thể kết luận luồng đó đã hoạt động đúng; biểu đồ kiến trúc do nhóm dự kiến xây dựng không thay thế bằng chứng của hệ thống hiện có.

## 2.2.2. Phân tích cơ sở dữ liệu và chức năng hiện có

### a) Kết quả kiểm tra dữ liệu hiện tại

Do chưa có lược đồ, mô hình dữ liệu, migration hoặc dữ liệu mẫu, nghiên cứu chưa xác lập được cấu trúc lưu trữ, khóa, chỉ mục và quan hệ thực tế của baseline. Bảng 2.3 vì vậy trình bày các nhóm dữ liệu cần kiểm tra, không khẳng định sự hiện diện của các bảng hoặc tập hợp dữ liệu tương ứng trong hệ thống hiện tại.

**Bảng 2.3. Các nhóm dữ liệu cần kiểm tra trên baseline sau khi được cung cấp**

| Nhóm dữ liệu | Câu hỏi phân tích | Vai trò đối với chức năng gợi ý | Trạng thái hiện tại |
|---|---|---|---|
| Sản phẩm và phân loại | Định danh sản phẩm/biến thể, danh mục, thuộc tính và trạng thái bán được lưu ở đâu? | Xác định item, tạo ứng viên và kiểm tra điều kiện hiển thị | Chưa có schema để xác minh |
| Khách hàng và phiên | Phân biệt tài khoản, khách chưa đăng nhập và phiên truy cập như thế nào? | Xác định chủ thể tương tác; tránh hợp nhất sai người dùng | Chưa có mã/schema để xác minh |
| Giỏ hàng | Sự kiện thêm/xóa có được lưu, hay chỉ còn trạng thái giỏ hiện tại? | Giỏ hàng có thể cung cấp tín hiệu ý định, nhưng trạng thái không thay thế nhật ký sự kiện | Chưa xác minh |
| Đơn hàng và chi tiết | Trạng thái đơn, trạng thái thanh toán, sản phẩm và thời gian được liên kết thế nào? | Xác định tín hiệu mua hợp lệ và tránh tính đơn hủy như mua thành công | Chưa xác minh |
| Lịch sử xem/tìm kiếm | Có dữ liệu sự kiện, timestamp và định danh liên quan không? | Phản ánh hành vi trước mua và sở thích ngắn hạn | Chưa xác minh |
| Quan hệ sản phẩm | Quan hệ liên quan do quản trị thiết lập hay do thuật toán tạo? | Phân biệt chức năng kế thừa với đóng góp mới | Chưa xác minh |
| Hiển thị và nhấp gợi ý | Có request/list ID, vị trí, phiên bản mô hình và timestamp không? | Đánh giá phản hồi đối với danh sách gợi ý | Chưa xác minh |

*Bảng này là khung kiểm tra, không phải danh sách bảng hoặc chức năng đã có của baseline.*

### b) Nguyên tắc phân tích các chức năng hiện có

Khi có baseline, các nhóm chức năng cần được phân loại theo trạng thái: có sẵn và đã kiểm thử; có mã nhưng chưa kiểm thử; cần điều chỉnh; cần xây dựng mới; hoặc không thuộc phạm vi. Cách phân loại này giúp tách biệt bằng chứng triển khai với tuyên bố trong tài liệu và tránh quy toàn bộ chức năng hệ thống thành đóng góp mới của nhóm.

Đối với quản lý và tìm kiếm sản phẩm, cần kiểm tra điều kiện công bố, khả năng bán, danh mục, thuộc tính, phân trang và quyền truy cập. Kết quả gợi ý phải tuân thủ các ràng buộc này; điểm xếp hạng cao không thay thế điều kiện hợp lệ của sản phẩm.

Đối với tài khoản và phiên sử dụng, cần xác định cách nhận diện khách đã đăng nhập và khách ẩn danh, thời hạn phiên và cách xử lý dữ liệu sau đăng nhập. Không mặc định cookie đồng nghĩa với một cá nhân ổn định trên nhiều thiết bị; cũng không được tự động liên kết lịch sử của các người dùng khác nhau trên thiết bị dùng chung.

Đối với giỏ hàng và đơn hàng, cần phân biệt hành động tương tác với trạng thái hiện tại. Một bản ghi đang có trong giỏ không cho biết đầy đủ chuỗi thêm, sửa số lượng, xóa hoặc thời điểm diễn ra. Tương tự, bản ghi tạo đơn chưa chắc phản ánh giao dịch đã hoàn tất. Định nghĩa tín hiệu “mua hàng” cần dựa trên trạng thái nghiệp vụ được xác minh, đồng thời quy định cách xử lý đơn hủy, hoàn tiền và bản ghi trùng.

Đối với các khối sản phẩm liên quan có sẵn, cần kiểm tra nguồn sinh danh sách và tiêu chí sắp xếp. Như kết quả mục 2.1 cho thấy, quan hệ do quản trị viên thiết lập, danh sách cùng danh mục và danh sách đã xem có thể tồn tại độc lập với một cơ chế xếp hạng theo hành vi. Do đó, tên giao diện hoặc sự hiện diện của lịch sử xem chưa đủ để xác nhận baseline đã có chức năng mà đề tài hướng đến.

### c) Đánh giá khoảng cách dữ liệu phục vụ chức năng gợi ý

Một baseline đáp ứng luồng mua bán chưa chắc đã cung cấp đủ dữ liệu cho phương pháp gợi ý được lựa chọn. Cần đánh giá xem hệ thống chỉ lưu trạng thái giao dịch hay còn ghi nhận chuỗi tương tác có thời gian và ngữ cảnh. Mức độ cần bổ sung dữ liệu phụ thuộc vào thuật toán, ngữ cảnh cung cấp gợi ý và phương pháp đánh giá dự kiến.

Về mặt yêu cầu mở rộng, một sự kiện tương tác tối thiểu có thể cần: định danh sự kiện, chủ thể hoặc phiên được giả danh hóa, mã sản phẩm, loại hành động và thời gian do hệ thống quản lý. Tùy mục tiêu đánh giá, có thể bổ sung nguồn phát sinh, mã danh sách gợi ý, vị trí hiển thị và phiên bản cơ chế gợi ý. Đây là các trường thông tin đề xuất để phân tích, chưa phải tên cột hoặc cấu trúc bảng đã tồn tại. Thiết kế vật lý chi tiết cần được đặt tại mục 2.5.3 sau khi đã thống nhất phạm vi.

Chất lượng sự kiện cần được kiểm soát bằng cơ chế phát hiện bản ghi trùng do gửi lại, nhận diện truy cập tự động và thao tác quản trị, xác minh mã sản phẩm, phân biệt thời điểm hành động với thời điểm tiếp nhận và xác định thời hạn lưu trữ. Định danh giả danh hóa vẫn có thể liên kết với một chủ thể; không đồng nghĩa dữ liệu đã được ẩn danh hoàn toàn. Việc thu thập và sử dụng cần được giới hạn theo mục đích, quyền truy cập và chính sách áp dụng.

Khi diễn giải phản hồi ngầm, cần phân biệt cơ hội tiếp xúc với tín hiệu quan tâm. Lần hiển thị cho biết sản phẩm có cơ hội được quan sát, không tự chứng minh sự yêu thích; việc không nhấp hoặc không mua cũng chưa đủ để kết luận người dùng không quan tâm. Các giới hạn này cần được phản ánh trong cách xây dựng nhãn, trọng số tương tác và diễn giải kết quả.

Về đánh giá, cần phân biệt dữ liệu huấn luyện với dữ liệu kiểm tra theo thời gian phù hợp. Việc sử dụng lịch sử mua, độ phổ biến hoặc quan hệ sản phẩm từ giai đoạn sau thời điểm dự đoán có thể làm rò rỉ thông tin và dẫn đến đánh giá quá lạc quan. Với chỉ tiêu nhấp vào gợi ý, việc bổ sung nhật ký hiển thị và ngữ cảnh danh sách là điều kiện cần để xác định mẫu số và truy vết kết quả.

### d) Ranh giới giữa kế thừa và đóng góp dự kiến

Ở mức định hướng, chức năng mới dự kiến bao gồm: ghi nhận tương tác phù hợp với phạm vi dữ liệu; chuyển đổi tương tác thành đầu vào có thể xử lý; xây dựng cơ chế lựa chọn và xếp hạng sản phẩm liên quan; cung cấp kết quả cho giao diện; và đánh giá so với phương pháp đối chứng. Tuy nhiên, phần nào thực sự là mới chỉ có thể được xác định sau khi kiểm tra baseline được chọn. Nếu hệ thống đã có một phần các năng lực này, báo cáo phải mô tả rõ phần kế thừa và phần nhóm điều chỉnh hoặc phát triển thêm.

Các chức năng thương mại điện tử cốt lõi như tài khoản, catalog, giỏ hàng, đặt hàng và thanh toán cần được giữ nhất quán với hệ thống nền tảng. Mô-đun gợi ý không nên làm thay đổi ngoài ý muốn các quy tắc về giá, tồn kho, quyền truy cập hoặc trạng thái đơn. Khi không thể trả về kết quả gợi ý, hệ thống cần có hành vi dự phòng để luồng mua hàng cốt lõi vẫn tiếp tục theo thiết kế.

Tóm lại, bằng chứng hiện tại mới cho phép xác nhận kho khởi tạo dự án, chưa cho phép xác nhận một baseline thương mại điện tử có thể vận hành. Phân tích đầy đủ mục 2.2 cần được hoàn thiện bằng URL hoặc source baseline, phiên bản được chọn, cấu trúc dữ liệu và kết quả kiểm tra các luồng chức năng. Các nội dung đề xuất ở trên là cơ sở cho bước kiểm tra tiếp theo, không phải xác nhận hệ thống đã có hoặc đã triển khai các chức năng tương ứng.
