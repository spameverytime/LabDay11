# Guideline patch

- **Rule mới đề xuất:** **R11 — Nhận diện ThreeWheeler và Truck dưới biến dạng thấu kính fisheye**: Khi xe ba bánh (ThreeWheeler) hoặc xe tải nhỏ (Truck) xuất hiện ở góc nhìn nghiêng tại vùng mid và edge, nếu quan sát thấy mui bạt, khung cabin hở hoặc kết cấu đầu xe thon gọn đặc trưng thì bắt buộc phân loại đúng `ThreeWheeler` hoặc `Truck`, không được gán nhãn `Car` dù méo quang học làm kích thước ngang bị kéo giãn tương đương xe con.
- **Áp dụng cho:** Các lớp `ThreeWheeler`, `Truck`, `Car` tại vùng `mid` và `edge` trên ảnh fisheye.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** Quy tắc R04 trong bản v1.0.0 chỉ liệt kê danh mục ánh xạ tên phương tiện trên lý thuyết, hoàn toàn thiếu tiêu chí phân định hình học thực tế khi đối tượng bị méo góc rộng (barrel distortion), dẫn đến hiện tượng nhầm lẫn class thường xuyên giữa ThreeWheeler và Car ở khoảng cách trung bình.
- **`rules_version` mới:** v1.1.0
- **Hiệu lực từ:** Vòng rework (P5) và toàn bộ các đợt mở rộng dữ liệu sau này.
