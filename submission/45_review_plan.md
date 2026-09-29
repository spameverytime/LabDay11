# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| Vùng **mid zone** (`adasind_271039.jpg`, `adasind_295948.jpg`) | 2 ca `WRONG_CLASS` (ThreeWheeler/Truck nhầm thành Car), 2 `MISSING`, 4 `SPURIOUS` | Hiệu ứng méo quang học fisheye tăng mạnh ở vùng giữa khiến hình học xe ba bánh và xe tải nhỏ bị kéo giãn, gây nhầm lớp nghiêm trọng nhất trong các phân vùng. | Ảnh crop đối tượng nghiêng, file XML đối chiếu `compare.html`, nhật ký quyết định phân loại theo R04/R11. |
| Vùng **center zone** (`adasind_270517.jpg`, `adasind_271039.jpg`) | 5 ca `MISSING`, 11 ca `SPURIOUS` (chủ yếu từ model và đối tượng che khuất) | Trục di chuyển trực diện của xe ego với mật độ phương tiện dày đặc; bỏ sót hoặc cảnh báo ảo tại đây đe dọa trực tiếp an toàn phanh khẩn cấp (AEB). | Báo cáo `model_compare.html`, bảng phân tích `zone_table.md`, log xung đột `local_quality_conflicts.csv`. |

**Giới hạn của kết luận từ ba frame ADASIND:** Ba frame được trích từ duy nhất một camera trước (front fisheye) trên địa hình giao thông Ấn Độ. Kích thước mẫu quá nhỏ (20 vật thể ground truth) chỉ giúp nhận diện các dạng lỗi điển hình về méo quang học và che khuất, tuyệt đối không đại diện cho toàn bộ hệ thống SVM 4 camera (vốn có các góc nhìn hông/sau với điểm mù, vùng cắt seam và tính chất quang học khác biệt).

## Chuyển sang kế hoạch bốn camera giả lập

- **Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv`:**
  - *Lấy mẫu phân tán theo thời gian (temporal subsampling)*: Đặt khoảng cách tối thiểu giữa 2 frame được chọn cách nhau ít nhất 3–5 giây (hoặc di chuyển $\ge 15\text{ m}$) để tránh hiện tượng tự tương quan (autocorrelation) khi đếm các frame liên tiếp trong cùng một cảnh tĩnh.
  - *Kiểm soát độ phủ kịch bản (ODD coverage)*: Đảm bảo 200 frame phân bổ đủ các điều kiện ánh sáng (ngược sáng gắt, chói đèn pha đêm, bóng râm) và loại hình chướng ngại vật (xe máy lách sát hông, người đi bộ băng cắt, vật cản thấp cản sau).
- **Vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi:**
  - Bộ 200 frame được thiết kế theo phương pháp lấy mẫu phân tầng có chủ đích (stratified purposive sampling), trong đó các ca khó (hard case) được ưu tiên chiếm hơn 50% ngân sách nhằm tối đa hóa khả năng phát hiện lỗi biên (edge cases).
  - Vì phân phối mẫu không ngẫu nhiên đại diện cho tập 50.000 frame ban đầu, tỷ lệ lỗi đo được trên 200 frame này chỉ mang tính chất định tính để phát hiện lỗ hổng quy chuẩn và năng lực model, không dùng để suy diễn tỷ lệ lỗi tổng thể trên toàn hệ thống.
