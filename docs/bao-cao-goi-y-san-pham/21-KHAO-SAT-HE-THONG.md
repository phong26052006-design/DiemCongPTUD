# 2.1. Khảo sát các website thương mại điện tử tương tự

## 2.1.1. Khảo sát một số website tiêu biểu

### a) Mục tiêu, đối tượng và phương pháp khảo sát

Đối với đề tài “Xây dựng chức năng gợi ý sản phẩm liên quan dựa trên hành vi người dùng cho website thương mại điện tử”, khảo sát hệ thống tương tự nhằm nhận diện cách thức hình thành, cung cấp và kiểm soát danh sách sản phẩm gợi ý; từ đó xác lập cơ sở lựa chọn phương án phát triển phù hợp với phạm vi đồ án. Đối tượng khảo sát không chỉ là vị trí hiển thị các khối sản phẩm, mà còn bao gồm dữ liệu đầu vào, cơ chế lựa chọn ứng viên, phương thức tích hợp với trang sản phẩm và các giới hạn có thể kiểm chứng của từng hệ thống.

Nghiên cứu sử dụng phương pháp chọn mẫu có chủ đích, lựa chọn ba trường hợp tham chiếu ở cấp cấu phần nền tảng: giao diện Dawn của Shopify, mã nguồn lõi WooCommerce và mã nguồn lõi nopCommerce. Tiêu chí lựa chọn là khả năng truy cập nguồn chính thức, truy vết phiên bản và đối chiếu các cơ chế cung cấp sản phẩm liên quan. Các trường hợp này cho phép phân tích cơ chế gọi dịch vụ gợi ý, lựa chọn sản phẩm theo phân loại và khai thác quan hệ sản phẩm được cấu hình sẵn [1]–[8]. Mẫu khảo sát có giá trị tham chiếu kỹ thuật; không được sử dụng để suy rộng về thị phần hoặc mức độ phổ biến của từng cơ chế trên thị trường.

**Phạm vi phương pháp:** đơn vị phân tích là cấu phần mã nguồn, không phải ba website bán lẻ cụ thể đã được quan sát trực tiếp. Nghiên cứu chưa thực hiện thử nghiệm tài khoản, đo chuyển đổi hoặc phỏng vấn người sử dụng. Các kết luận vì vậy được giới hạn ở cấu trúc và luồng xử lý đã kiểm tra, không bao quát mọi phần bổ sung hoặc cửa hàng triển khai trên cùng nền tảng. Nếu yêu cầu học phần đòi hỏi khảo sát trực tiếp ba website đang vận hành, cần bổ sung hoạt động đó cùng minh chứng quan sát.

Các phiên bản được cố định theo commit để tránh thay đổi nội dung khi nhánh phát triển được cập nhật: Shopify Dawn `05222537f672`; WooCommerce `e8732426f5bf`; nopCommerce `f9e883bc9586`. Mã commit đầy đủ, đường dẫn và thời điểm thu thập được cung cấp trong danh mục tài liệu tham khảo và nhật ký nguồn. Những phiên bản này là ảnh chụp của các nhánh được khảo sát, không mặc định là phiên bản ổn định mà nhóm sẽ sử dụng.

Khung khảo sát gồm năm tiêu chí: (i) ngữ cảnh xuất hiện gợi ý; (ii) dữ liệu và quan hệ được sử dụng; (iii) cơ chế tạo danh sách; (iv) khả năng suy ra mức độ cá nhân hóa từ bằng chứng; và (v) bài học có thể vận dụng vào đề tài. Các tiêu chí này giúp phân biệt sự hiện diện của một khối “sản phẩm liên quan” với việc hình thành gợi ý theo lịch sử tương tác của từng người dùng.

### b) Shopify Dawn: tích hợp dịch vụ gợi ý vào giao diện cửa hàng

Dawn được Shopify công bố như một giao diện cửa hàng có mã nguồn công khai. Trong cấu phần `sections/related-products.liquid`, khu vực sản phẩm liên quan sử dụng phần tử `product-recommendations`, cấu hình địa chỉ `routes.product_recommendations_url`, giới hạn số lượng và mã sản phẩm đang xem. Khi kết quả đã được xử lý và danh sách trả về không rỗng, giao diện lặp qua `recommendations.products` để hiển thị các thẻ sản phẩm [1].

Ở phía trình duyệt, lớp `ProductRecommendations` trong `assets/global.js` sử dụng `IntersectionObserver` để xác định thời điểm cần tải nội dung. Phương thức `loadRecommendations` gửi yêu cầu đến địa chỉ đã cấu hình, kèm `product_id` và `section_id`, rồi đưa phần HTML phù hợp vào khu vực gợi ý [2]. Cấu trúc này thể hiện sự phân tách trách nhiệm giữa lớp trình bày và dịch vụ tạo kết quả: giao diện tổ chức cách tải và hiển thị, trong khi logic sinh danh sách nằm ở phía dịch vụ.

Về phương diện kiến trúc, trường hợp Dawn gợi mở cách tích hợp chức năng gợi ý mà không buộc trang chi tiết sản phẩm phải chứa toàn bộ logic truy xuất và xếp hạng. Đây là cơ sở tham khảo cho việc thiết kế một dịch vụ gợi ý có hợp đồng đầu vào, đầu ra và cơ chế xử lý trường hợp không có kết quả. Tuy nhiên, việc có tải nội dung bất đồng bộ chỉ cho thấy cách thức triển khai; nghiên cứu chưa đo lường được mức cải thiện thời gian tải hoặc trải nghiệm thực tế.

Phạm vi mã giao diện được khảo sát không cho phép xác định đầy đủ thuật toán của dịch vụ gợi ý Shopify. Sự xuất hiện của `product_id` trên URL chỉ xác nhận một đầu vào được truyền từ giao diện; chưa đủ để xác định toàn bộ ngữ cảnh mà dịch vụ sử dụng. Bằng chứng hiện có do đó xác nhận được cơ chế tích hợp và hiển thị, nhưng chưa xác nhận thuật toán nội bộ, trọng số hành vi hoặc mức độ cá nhân hóa đối với từng khách hàng.

**Bài học áp dụng:** tách lớp giao diện khỏi logic gợi ý; sử dụng ngữ cảnh sản phẩm hiện tại khi phù hợp; hỗ trợ tải nội dung độc lập; xử lý danh sách rỗng và không làm gián đoạn chức năng xem sản phẩm khi dịch vụ gợi ý gặp lỗi. Khả năng cá nhân hóa cần được chứng minh bằng dữ liệu và thực nghiệm riêng của hệ thống nghiên cứu, không suy ra từ tên gọi của khối giao diện.

### c) WooCommerce: lựa chọn sản phẩm liên quan theo danh mục và thẻ

Trong mã nguồn lõi WooCommerce được khảo sát, hàm `wc_get_related_products` tiếp nhận mã sản phẩm, giới hạn kết quả và danh sách sản phẩm cần loại trừ. Đường thực thi mặc định sử dụng các nhóm phân loại `product_cat` và `product_tag` làm căn cứ xác định những sản phẩm có liên quan. Hàm đồng thời loại sản phẩm hiện tại khỏi danh sách, sử dụng bộ nhớ đệm cho kết quả và cho phép điều chỉnh thông qua các bộ lọc mở rộng của nền tảng [3].

Tại lớp truy cập dữ liệu, phương thức `get_related_products_query` xây dựng truy vấn lựa chọn các sản phẩm đã công bố, kết hợp các quan hệ phân loại và loại trừ sản phẩm không được xuất hiện trong danh mục. Khi cấu hình cửa hàng yêu cầu ẩn sản phẩm hết hàng, truy vấn bổ sung điều kiện loại trừ tương ứng [4]. Các điều kiện này cho thấy tính liên quan về nội dung phải đi kèm tính hợp lệ của ứng viên trước khi được hiển thị.

Theo đường thực thi đã kiểm tra, danh sách sản phẩm liên quan được xác lập chủ yếu từ quan hệ phân loại và ngữ cảnh sản phẩm đang xem; chưa có căn cứ cho thấy hàm mặc định này tự tổng hợp lịch sử tương tác của từng khách hàng để học sở thích cá nhân. Việc kết quả có thể được xáo trộn thông qua `shuffle` cũng không đồng nghĩa với cá nhân hóa: thay đổi thứ tự ngẫu nhiên và điều chỉnh thứ tự theo hồ sơ hành vi là hai cơ chế khác nhau [3].

Ưu điểm của cách tiếp cận này là dễ giải thích và có thể hoạt động ngay khi chưa tích lũy dữ liệu tương tác. Chất lượng kết quả phụ thuộc vào cấu trúc danh mục, chất lượng gắn thẻ và mức độ phù hợp của tập ứng viên. Mặt khác, các sản phẩm cùng phân loại không nhất thiết đáp ứng cùng nhu cầu, ngân sách hoặc ý định mua của mọi khách hàng. Đây là giới hạn phân tích của một cơ chế dựa vào phân loại; chưa phải kết quả đo lường độ chính xác trên một tập người dùng thực tế.

WooCommerce có các điểm mở rộng (hooks) và phần bổ sung (plugins) cho phép thay đổi hành vi mặc định. Kết luận trên vì vậy chỉ áp dụng cho cấu phần lõi và phiên bản được khảo sát; không xác lập sự vắng mặt của gợi ý theo hành vi trong toàn bộ hệ sinh thái WooCommerce.

**Bài học áp dụng:** cơ chế dựa trên danh mục hoặc thẻ có thể được sử dụng làm phương pháp đối chứng và phương án dự phòng khi dữ liệu hành vi còn hạn chế. Chức năng mới cần thể hiện được cách dữ liệu hành vi tham gia lựa chọn hoặc xếp hạng ứng viên, đồng thời duy trì các điều kiện về trạng thái công bố, khả năng bán và loại trừ sản phẩm không phù hợp. Việc thay đổi cơ chế không mặc nhiên bảo đảm chất lượng gợi ý tốt hơn; kết luận đó cần được kiểm chứng bằng thực nghiệm.

### d) nopCommerce: quan hệ sản phẩm được cấu hình và lịch sử xem

Trong nopCommerce, thực thể `RelatedProduct` biểu diễn một quan hệ có hướng giữa hai sản phẩm thông qua `ProductId1` và `ProductId2`, kèm thuộc tính `DisplayOrder`. Phương thức `GetRelatedProductsByProductId1Async` truy xuất các quan hệ theo sản phẩm nguồn, loại sản phẩm đã xóa hoặc chưa công bố tùy tham số, rồi sắp xếp theo thứ tự hiển thị [5], [6].

Trong khu vực quản trị, tác vụ thêm sản phẩm liên quan tạo bản ghi với hai mã sản phẩm tương ứng. Bằng chứng này cho thấy danh sách liên quan trong đường thực thi đang xét có thể được hình thành từ cấu hình quan hệ của người quản trị, thay vì tự động học quan hệ từ lịch sử hành vi [8]. Khi hiển thị ra phía khách hàng, `RelatedProductsViewComponent` tiếp tục kiểm tra quyền truy cập, ánh xạ cửa hàng, thời gian khả dụng và điều kiện hiển thị độc lập của sản phẩm [7].

Bên cạnh quan hệ sản phẩm liên quan, nopCommerce có dịch vụ `RecentlyViewedProductsService`. Trong cấu phần được khảo sát, dịch vụ lưu danh sách mã sản phẩm đã xem bằng cookie, giới hạn số lượng theo cấu hình và lọc các sản phẩm không còn được công bố hoặc đã xóa khi đọc lại [9]. Đây là cơ chế ghi nhớ hành vi xem ở phạm vi trình duyệt, nhưng chưa đủ để kết luận rằng danh sách “sản phẩm liên quan” đã được xếp hạng từ toàn bộ lịch sử hành vi. Việc trình bày lại các sản phẩm đã xem và suy luận những sản phẩm mới có khả năng phù hợp cần được phân biệt về mục tiêu và phương pháp.

Xét về khả năng kiểm soát nghiệp vụ, quan hệ được cấu hình sẵn tạo điều kiện cho người quản trị chủ động xác định các sản phẩm thay thế hoặc bổ trợ. Tuy nhiên, nếu chỉ sử dụng cấu hình này, hệ thống chưa có bằng chứng về khả năng tự điều chỉnh theo thay đổi sở thích của từng khách hàng. Nhận định này chỉ áp dụng cho các đường thực thi được dẫn nguồn; các plugin và phần tùy biến ngoài phạm vi khảo sát có thể bổ sung những cơ chế khác.

**Bài học áp dụng:** hệ thống cần phân biệt dữ liệu quản trị quan hệ sản phẩm, dữ liệu lịch sử xem và kết quả suy luận gợi ý. Danh sách được thuật toán đề xuất vẫn phải tuân thủ các ràng buộc công bố, quyền truy cập và khả năng bán của hệ thống nền tảng. Không nên coi dữ liệu lịch sử xem đã tồn tại là bằng chứng một mô hình cá nhân hóa đã được triển khai.

## 2.1.2. So sánh và đánh giá

### a) Kết quả so sánh theo bằng chứng

**Bảng 2.1. So sánh các cấu phần gợi ý sản phẩm trong ba trường hợp khảo sát**

| Tiêu chí | Shopify Dawn | WooCommerce lõi | nopCommerce lõi |
|---|---|---|---|
| Căn cứ khảo sát | Phân vùng giao diện Liquid và mã JavaScript tải gợi ý [1], [2] | Hàm sản phẩm liên quan và truy vấn dữ liệu [3], [4] | Thực thể, dịch vụ, thành phần hiển thị và tác vụ quản trị [5]–[9] |
| Ngữ cảnh đã xác minh | Sản phẩm hiện tại và phân vùng hiển thị | Sản phẩm hiện tại và quan hệ danh mục/thẻ | Sản phẩm nguồn và các quan hệ đã lưu |
| Cơ chế tạo hoặc nhận danh sách | Giao diện gọi dịch vụ gợi ý của nền tảng | Truy vấn theo phân loại, bộ lọc và cấu hình liên quan | Truy xuất quan hệ sản phẩm; sắp xếp theo DisplayOrder |
| Sử dụng lịch sử hành vi để xếp hạng | Chưa xác định được từ mã giao diện | Chưa được chứng minh trong luồng mặc định đã xét | Chưa được chứng minh trong luồng RelatedProduct; lịch sử đã xem là cấu phần riêng |
| Kiểm soát sản phẩm hiển thị | Nhận và trình bày kết quả dịch vụ; điều kiện kết quả không rỗng | Trạng thái công bố, loại trừ và điều kiện ẩn hết hàng khi được bật | Công bố/xóa, ACL, ánh xạ cửa hàng, thời gian khả dụng, hiển thị độc lập |
| Khả năng giải thích từ mã công khai | Giải thích được hợp đồng tích hợp; chưa giải thích đầy đủ dịch vụ nội bộ | Giải thích được theo phân loại sản phẩm | Giải thích được bằng quan hệ cấu hình và thứ tự hiển thị |
| Giá trị tham khảo cho đề tài | Phân tách giao diện và dịch vụ | Đối chứng theo danh mục/thẻ và phương án dự phòng | Kiểm soát nghiệp vụ và phân biệt lịch sử xem với gợi ý |

*Nguồn: tổng hợp từ phân tích mã nguồn chính thức tại các commit nêu trong mục 2.1.1. “Chưa được chứng minh” biểu thị giới hạn bằng chứng, không khẳng định tính năng đó không tồn tại trong toàn bộ nền tảng.*

Các trường hợp khảo sát cho thấy “sản phẩm liên quan” không phải một khái niệm đồng nhất về phương pháp. Một danh sách có thể được tạo bằng cấu hình biên tập, quan hệ phân loại, dịch vụ gợi ý phía máy chủ hoặc mô hình sử dụng dữ liệu tương tác. Nếu chỉ đánh giá sự xuất hiện của khối sản phẩm trên giao diện, nghiên cứu sẽ khó phân biệt đóng góp thực sự của từng cách tiếp cận.

Do chưa có cùng tập dữ liệu, cùng tập ứng viên và cùng quy trình thực nghiệm trên ba hệ thống, nghiên cứu không xếp hạng hệ thống nào “chính xác nhất” hoặc “cá nhân hóa tốt nhất”. Tương tự, không có căn cứ để gán tỷ lệ tăng doanh thu, tăng nhấp chuột hoặc cải thiện chuyển đổi cho các cấu phần chỉ dựa trên việc đọc mã nguồn.

### b) Cơ sở xác định khoảng trống và hướng phát triển

Đối với đề tài, vấn đề cần giải quyết là xây dựng một quy trình có thể kiểm chứng để sử dụng lịch sử tương tác trong lựa chọn hoặc xếp hạng sản phẩm liên quan. Kết quả khảo sát không đủ để xác lập một khoảng trống nghiên cứu chung của toàn ngành. Ở phạm vi đồ án, đóng góp cần được xác định bằng sự khác biệt so với hệ thống nền tảng được lựa chọn, thông qua dữ liệu đầu vào, cơ chế xử lý và kết quả có thể đánh giá.

Tài liệu kỹ thuật của SAR trong dự án Recommenders mô tả hai thành phần: ma trận mức độ gắn kết giữa người dùng và sản phẩm, cùng ma trận tương tự giữa các sản phẩm. Điểm gợi ý được hình thành từ sự kết hợp hai thành phần này; tài liệu cũng trình bày cách phân biệt loại tương tác và giảm ảnh hưởng của các sự kiện cũ [10]. Đây là căn cứ tham khảo cho việc đưa lịch sử hành vi vào quá trình xếp hạng, thay vì chỉ căn cứ vào phân loại sản phẩm.

Một cách biểu diễn mức độ gắn kết có xét thời gian là:

\[
a_{u,i}(t_0)=\sum_{e\in E_{u,i},\;t_e\leq t_0} w_{\operatorname{type}(e)}\,2^{-\frac{t_0-t_e}{h}},\qquad h>0.
\]

Trong đó, \(E_{u,i}\) là tập tương tác hợp lệ của người dùng \(u\) với sản phẩm \(i\); \(w_{\operatorname{type}(e)}\) là trọng số của loại tương tác; \(t_e\) là thời điểm tương tác; \(t_0\) là thời điểm tham chiếu; và \(h\) là thời gian bán rã, sử dụng cùng đơn vị thời gian với hiệu \(t_0-t_e\). Khi độ tuổi của một tương tác bằng \(h\), đóng góp của tương tác đó giảm còn một nửa. Biểu thức được diễn giải từ cơ chế mức độ gắn kết (affinity) có suy giảm thời gian trong tài liệu SAR [10]; đây là một phương án tham khảo, chưa phải mô hình đã được nhóm triển khai. Các trọng số và thời gian bán rã cần được lựa chọn bằng dữ liệu huấn luyện, hiệu chỉnh trên dữ liệu xác thực và đánh giá trên tập kiểm tra độc lập, tránh điều chỉnh tham số trực tiếp theo kết quả kiểm tra.

Với bài toán gợi ý sản phẩm liên quan trên trang chi tiết, ngữ cảnh có thể đồng thời bao gồm sản phẩm hiện tại và lịch sử tương tác của khách hàng. Vì vậy, nhóm cần xác định rõ đối tượng cần gợi ý là sản phẩm thay thế, sản phẩm bổ trợ hay một tập hợp có kiểm soát của cả hai. Hai sản phẩm thường được xem hoặc mua cùng nhau không nhất thiết tương tự về công dụng; ngược lại, hai sản phẩm cùng danh mục không mặc nhiên có xác suất được lựa chọn như nhau đối với mọi người dùng.

Ở mức tài liệu giới thiệu mã nguồn, kho DIN cung cấp một hiện thực tham khảo cho bài toán dự đoán tỷ lệ nhấp; kho SimRec giới thiệu một phương pháp hướng đến vấn đề khởi đầu lạnh trong gợi ý tuần tự bằng cách tích hợp độ tương tự sản phẩm [11], [12]. Các nguồn này chỉ được sử dụng để nhận diện hướng tham khảo, không làm căn cứ mô tả đầy đủ kiến trúc hoặc hiệu quả của bài báo gốc. Đặc biệt, README của DIN nêu các vấn đề của phiên bản demo [11]. Việc lựa chọn mô hình cho đồ án vẫn cần căn cứ quy mô dữ liệu, tài nguyên, khả năng tái lập và yêu cầu giải thích; không mặc định phải sử dụng học sâu.

### c) Định hướng kế thừa và tiêu chí đánh giá cho đề tài

Từ kết quả khảo sát, đề tài có thể kế thừa bốn nguyên tắc triển khai. Thứ nhất, tách dịch vụ gợi ý khỏi lớp trình bày để thuận tiện thay đổi thuật toán và kiểm thử. Thứ hai, duy trì cơ chế lọc tính hợp lệ của sản phẩm sau khi sinh ứng viên hoặc xếp hạng. Thứ ba, phân biệt dữ liệu hành vi với cấu hình sản phẩm liên quan do người quản trị thiết lập. Thứ tư, duy trì phương án dự phòng khi người dùng hoặc sản phẩm chưa có đủ tương tác.

Để chứng minh vai trò của dữ liệu hành vi, thiết kế thực nghiệm nên có ít nhất một phương pháp đối chứng không cá nhân hóa, chẳng hạn sản phẩm cùng danh mục hoặc sản phẩm phổ biến. Các phương pháp phải được đánh giá trên cùng tập kiểm tra và cùng điều kiện xác định ứng viên. Đối với dữ liệu có thời gian, cần kiểm soát việc sử dụng thông tin tương lai: dữ liệu dùng để xây dựng đặc trưng, tính độ phổ biến hoặc học quan hệ sản phẩm phải có trước thời điểm dự đoán được đánh giá.

Với nhãn phù hợp dạng nhị phân và danh sách K sản phẩm, Precision@K đo tỷ lệ sản phẩm được gán nhãn phù hợp trong danh sách gợi ý; Recall@K đo tỷ lệ sản phẩm phù hợp của tập kiểm tra được tìm thấy trong danh sách đó. Hai chỉ tiêu này đánh giá khả năng lựa chọn sản phẩm phù hợp nhưng không phân biệt thứ tự giữa các sản phẩm bên trong danh sách. NDCG@K bổ sung yếu tố vị trí bằng cách chiết khấu giá trị của kết quả ở các vị trí thấp và chuẩn hóa theo thứ tự lý tưởng [15]. Trường hợp không có nhãn phù hợp, danh sách ngắn hơn K hoặc giá trị chuẩn hóa bằng không cần có quy ước xử lý được công bố trước khi tính toán.

Độ bao phủ sản phẩm (catalog coverage) có thể bổ sung góc nhìn về mức độ tập trung của kết quả: đó là tỷ lệ sản phẩm phân biệt xuất hiện trong các danh sách gợi ý so với tập sản phẩm tham chiếu được xác định trong cùng phạm vi đánh giá [15]. Cần phân biệt chỉ tiêu này với mức độ đa dạng về danh mục sản phẩm. Trong hiện thực được dẫn nguồn, mẫu số là số sản phẩm phân biệt trong dữ liệu huấn luyện; nếu sử dụng toàn bộ sản phẩm đủ điều kiện bán làm tập tham chiếu, cần điều chỉnh và công bố quy ước thay vì mặc định hai tập này trùng nhau. Khi báo cáo kết quả, phải nêu định nghĩa nhãn, tập người dùng, tập ứng viên, K, cách tổng hợp chỉ tiêu và phương pháp chia dữ liệu. Đánh giá ngoại tuyến không tự xác lập ảnh hưởng nhân quả đến doanh thu hoặc chuyển đổi.

Nếu đo tỷ lệ nhấp vào gợi ý, hệ thống cần ghi nhận cả lần hiển thị đủ điều kiện và lượt nhấp, gắn với cùng ngữ cảnh và phiên bản cơ chế gợi ý. Chỉ có nhật ký nhấp chuột mà không có dữ liệu hiển thị thì chưa đủ mẫu số để tính tỷ lệ nhấp một cách có ý nghĩa. Việc đánh giá hiệu quả kinh doanh bằng thử nghiệm A/B chỉ phù hợp khi có lưu lượng, cách phân nhóm và thời gian quan sát đủ để phân tích; đây chưa phải hoạt động đã thực hiện trong khảo sát này.

Như vậy, kết quả khảo sát định hướng đề tài theo một chuỗi xử lý có khả năng truy vết: ghi nhận tương tác hợp lệ; hình thành dữ liệu đầu vào; tạo và xếp hạng ứng viên theo mục tiêu đã xác định; lọc điều kiện kinh doanh; hiển thị kết quả; và ghi nhận phản hồi phục vụ đánh giá. Giá trị của chức năng sẽ được xác lập bằng thực nghiệm và bằng chứng triển khai của nhóm trong các chương tiếp theo.
