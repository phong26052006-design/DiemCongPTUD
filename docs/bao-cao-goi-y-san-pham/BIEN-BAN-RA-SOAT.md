# Biên bản rà soát nội dung và hình thức

Ngày: 23/10/2026. Áp dụng cho bản có hậu tố **DA-RA-SOAT**.

## Các chỉnh sửa nội dung quan trọng

1. **Phương pháp và đơn vị phân tích:** thay cách gọi có thể gây nhầm là khảo sát ba website cụ thể bằng mô tả chính xác: chọn mẫu có chủ đích, phân tích ba cấu phần nền tảng qua mã nguồn. Không suy rộng về thị phần hoặc toàn bộ thị trường.
2. **Phân biệt quan sát và kết luận:** giới hạn các nhận định vào luồng xử lý, phiên bản và tệp đã khảo sát; không suy ra thuật toán độc quyền, mức độ cá nhân hóa hoặc hiệu quả kinh doanh từ tên khối giao diện.
3. **Đóng góp của đề tài:** diễn đạt theo sự khác biệt so với baseline được chọn; không tuyên bố một khoảng trống nghiên cứu chung của toàn ngành hoặc mặc định phương pháp mới tốt hơn.
4. **Công thức:** đối chiếu với tài liệu SAR, chuẩn hóa ký hiệu và thuật ngữ thời gian bán rã; làm rõ đơn vị thời gian và việc hiệu chỉnh tham số tách biệt với tập kiểm tra.
5. **Chỉ tiêu đánh giá:** phân biệt Precision@K/Recall@K với NDCG@K; phân biệt độ bao phủ sản phẩm với đa dạng danh mục; làm rõ tập tham chiếu của mẫu số trong hiện thực catalog coverage.
6. **Nguồn và tác giả:** kiểm tra lại 12 tệp nguồn đã dùng qua HTTPS và đối chiếu SHA-256; bổ sung một tệp hiện thực chỉ tiêu đánh giá. Dẫn mã nguồn theo chủ kho/tổ chức công bố, không suy đoán tác giả cá nhân. Danh mục sau sửa có 15 mục, gồm 13 tệp nguồn trực tuyến, một tài liệu học phần và một kho dự án.
7. **Dữ liệu hành vi:** phân biệt lần hiển thị với tín hiệu quan tâm; làm rõ giới hạn của phản hồi ngầm và sự khác nhau giữa giả danh hóa với ẩn danh.
8. **Văn phong và hình thức:** giảm các diễn giải lặp, thống nhất thuật ngữ và cách dẫn nguồn; kiểm tra bảng, công thức, số trang, liên kết và tệp Word/PDF. Giữ nội dung kỹ thuật cần thiết để truy vết.

## Phạm vi xác minh

- Kiểm tra lại nội dung mã nguồn Shopify Dawn, WooCommerce và nopCommerce tại các commit cố định; kiểm tra công thức trong tài liệu SAR và mã hiện thực các chỉ tiêu đánh giá.
- Đối chiếu quy định baseline với trang 3–5 của tài liệu học phần.
- Kiểm tra lại kho DiemCongPTUD và đầu nhánh main: chỉ có README tại commit được dẫn; không sửa kho mã.
- Kiểm tra sự thống nhất giữa trích dẫn và danh mục, SHA-256 của 13 tệp nguồn, cấu trúc bảng/công thức, khả năng mở Word và nội dung PDF. Kiểm tra trực quan chọn lọc các trang có bảng/công thức.

## Phần chưa thể kết luận

- Chưa có source baseline ứng dụng của nhóm; mục 2.2 vẫn là bản thảo hiện trạng và khung phân tích.
- Chưa khảo sát trực tiếp ba website bán lẻ; chưa chạy các nền tảng hoặc thực nghiệm mô hình gợi ý.
- Không xác nhận chất lượng production, tỷ lệ tăng chuyển đổi/doanh thu hoặc tính vượt trội của mô hình.

Đây là bản đã hiệu đính trong phạm vi bằng chứng hiện có; không phải chứng nhận không còn mọi sai sót hoặc đã hoàn tất các hoạt động chưa thực hiện. Các tệp cũ được bảo lưu riêng để đối chiếu.
