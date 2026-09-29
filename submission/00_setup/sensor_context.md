# Sensor context

- **Rig**: Camera fisheye đơn (single front fisheye camera) gắn phía trước phương tiện (trên nóc hoặc kính chắn gió/gương chiếu hậu), hướng góc nhìn chúc nhẹ xuống mặt đường giao thông, bao quát góc siêu rộng phía trước phương tiện.
- **`ego_body`**: Nhìn thấy ở mép dưới đáy của khung hình (phần nắp capo/thân trước của xe ego). Xuất hiện ở hầu hết các frame (46/48 frame) dọc theo cạnh dưới của vòng tròn fisheye; ngoại trừ 2 frame ngoại lệ (`adasind_006840.jpg` và `adasind_271039.jpg`) không nhìn thấy thân xe.
- **Vòng kính (lens circle)**: Vòng tròn thấu kính fisheye nằm ở trung tâm ảnh, chiếm phần lớn diện tích khung hình (khoảng 80–85%), xung quanh 4 góc là viền đen quang học do trường nhìn tròn của thấu kính fisheye (được che bằng `lens_border`).
