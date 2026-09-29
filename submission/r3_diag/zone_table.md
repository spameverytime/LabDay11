# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 12 | 2 | 4 | 4 | 7 | SPURIOUS (3) |
| mid | 5 | 2 | 3 | 2 | 4 | WRONG_CLASS (2) |
| edge | 3 | 0 | 1 | 1 | 1 | SPURIOUS (1) |

## Nhận xét

- **Zone người (L) và model (M) gãy nhiều nhất**: Vùng **center** có số lượng lỗi tuyệt đối lớn nhất ở cả người (L: 2 missing, 4 spurious) và model (M: 4 missing, 7 spurious). Tuy nhiên, xét theo tỷ lệ, vùng **mid** gãy nặng nề nhất về phân loại đối tượng khi có tới 2/5 đối tượng bị nhầm lớp (WRONG_CLASS), model cũng có 2 missing và 4 spurious.
- **Giả thuyết nguyên nhân**:
  1. *Vùng center*: Mật độ phương tiện tập trung dày đặc trên trục đường chính, nhiều đối tượng bị che khuất đan xen (occlusion) dẫn đến model dễ sinh box ảo (7 spurious) và khó phân tách ranh giới chính xác giữa các xe đi sát nhau.
  2. *Vùng mid*: Hiệu ứng méo góc rộng của thấu kính fisheye bắt đầu tác động rõ rệt, làm biến dạng hình học của các xe ba bánh (ThreeWheeler) và xe tải nhỏ (Truck), dẫn đến nhầm lẫn class giữa ThreeWheeler, Car và Truck.
  3. *Vùng edge*: Do đặc thù có ít đối tượng (n=3), người bắt trọn 3/3 vật thể (missing=0); lỗi spurious chủ yếu do ranh giới tiếp giáp với vành đen `lens_border`.
- **Giới hạn của slice 3 frame**: Tập mẫu 3 frame với tổng cộng 20 đối tượng ground truth chỉ mang tính minh họa hình thái lỗi cục bộ. Kích thước mẫu quá nhỏ, không đại diện cho toàn bộ phân phối dữ liệu lái xe thực tế (thiếu cảnh ban đêm, thời tiết mưa gió, ngược sáng gắt), do đó các chỉ số đo đạc chỉ phục vụ việc chẩn đoán ca khó thay vì đánh giá năng lực tổng thể của annotator hay model.
