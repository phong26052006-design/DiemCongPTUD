# Hướng dẫn sử dụng bản nghiên cứu

Ngày: 23/10/2026. Đề tài được người dùng xác nhận: gợi ý sản phẩm liên quan dựa trên hành vi người dùng.

## Trạng thái bàn giao

- Mục 2.1: bản khảo sát kỹ thuật ba cấu phần nền tảng Shopify Dawn, WooCommerce và nopCommerce; có so sánh, phân tích và nguồn cố định theo commit. Đây chưa phải khảo sát trực tiếp ba website bán lẻ cụ thể.
- Mục 2.2: bản thảo có căn cứ về hiện trạng, chưa phải phân tích một baseline ứng dụng được chọn. Kho được cung cấp mới có README; còn cần URL/source và phiên bản baseline thực tế để hoàn thiện phần công nghệ, DB và chức năng hiện có.
- Không khảo sát UI trực tiếp, không đo performance/CTR/conversion, không chạy các hệ thống tham chiếu và không huấn luyện/test một mô hình gợi ý trong công việc nghiên cứu này.
- Không sửa kho mã, không lựa chọn baseline thay nhóm và không gán stack Node/MySQL của đề tài đặt sân cũ cho đề tài mới.

## Điều chỉnh mục lục cho nhất quán với hướng đã xác nhận

| Mục | Tên đề xuất |
|---|---|
| 2.4 | Phân tích chức năng gợi ý sản phẩm dựa trên hành vi người dùng |
| 2.4.1 | Quy trình ghi nhận và xử lý hành vi người dùng |
| 2.4.2 | Tiêu chí lựa chọn, xếp hạng và lọc sản phẩm gợi ý |
| 3.4 | Xây dựng chức năng gợi ý sản phẩm dựa trên hành vi người dùng |
| 3.4.1 | Ghi nhận và quản lý dữ liệu tương tác |
| 3.4.2 | Xây dựng và tích hợp cơ chế gợi ý sản phẩm |
| 3.4.3 | Hiển thị kết quả, cập nhật và xử lý trường hợp thiếu dữ liệu |
| 4.2 | Kiểm thử và đánh giá chức năng gợi ý sản phẩm |

Đây là gợi ý đổi tên để thống nhất chủ đề, chưa phải yêu cầu xây dựng thêm chức năng.

## Những điểm phải giữ khi đưa vào báo cáo

1. Giữ nguyên phương pháp khảo sát: phân tích mã nguồn/tài liệu, không đổi thành tuyên bố đã trực tiếp dùng website.
2. Giữ chú thích “chưa xác định” trong bảng so sánh. Không đổi thành “không có” khi chưa kiểm tra toàn bộ hệ thống/plugin.
3. Không biến công thức tham khảo hoặc trọng số đề xuất thành mô hình đã được nhóm triển khai và chứng minh tối ưu.
4. Không nộp mục 2.2 như bản mô tả hoàn chỉnh baseline ứng dụng khi chưa có source. Phần khung kiểm tra cần được thay bằng kết quả thực tế sau khi baseline được cung cấp.
5. Không thêm số liệu doanh thu/thị phần/lượt dùng/độ chính xác nếu không có nguồn và phương pháp kiểm chứng.

## Các tệp

- BAO-CAO-MUC-2.1-2.2-DA-RA-SOAT.docx: bản Word chỉnh sửa được, sau rà soát.
- BAO-CAO-MUC-2.1-2.2-DA-RA-SOAT.pdf: bản đọc và kiểm tra trình bày, sau rà soát.
- 21-KHAO-SAT-HE-THONG.md: nội dung mục 2.1.
- 22-PHAN-TICH-BASELINE.md: bản thảo mục 2.2 có ghi rõ điểm còn thiếu.
- 23-TAI-LIEU-THAM-KHAO.md: danh mục nguồn và giới hạn sử dụng.
- NGUON-VA-BANG-CHUNG.json: URL cố định, commit, dòng mã và checksum.
- HIEN-TRANG-BASELINE.json: ảnh chụp kết quả kiểm tra kho dự án.

Tệp PDF được bổ sung sau bước chuyển đổi Word. Kho lưu trữ chỉ chứa bản tổng hợp và metadata bằng chứng, không đóng gói toàn bộ mã nguồn hoặc sách/tài liệu gốc.

## Phụ lục hình ảnh bổ sung ngày 24/10/2026

[Xem 9 ảnh minh chứng cùng URL nguồn và chú thích](minh-chung-website/README.md), hoặc tải [phụ lục PDF](minh-chung-website/PHU-LUC-MINH-CHUNG-HINH-ANH.pdf), [Word](minh-chung-website/PHU-LUC-MINH-CHUNG-HINH-ANH.docx) và [ZIP](minh-chung-website/MINH-CHUNG-WEBSITE-CO-NGUON.zip).

Bộ ảnh có 6 ảnh giao diện từ tài liệu/tài nguyên chính thức và 3 ảnh chụp trang mã nguồn. Việc bổ sung này không thay đổi giới hạn của báo cáo: chưa khảo sát demo trực tiếp và chưa có source baseline ứng dụng của nhóm.
