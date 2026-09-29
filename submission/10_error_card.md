# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | BOX_GEOMETRY | 1 |
| center | B4 | IGNORE_SCOPE | 1 |
| center | B4 | MISSING | 5 |
| center | B4 | SPURIOUS | 11 |
| center | B4 | WRONG_CLASS | 1 |
| center | C0 | SPURIOUS | 2 |
| edge | B4 | ATTRIBUTE | 2 |
| edge | B4 | MISSING | 1 |
| edge | B4 | SPURIOUS | 3 |
| mid | B4 | IGNORE_SCOPE | 8 |
| mid | B4 | MISSING | 2 |
| mid | B4 | SPURIOUS | 7 |
| mid | B4 | WRONG_CLASS | 2 |
| mid | C0 | SPURIOUS | 1 |
| unknown | C0 | SPURIOUS | 1 |

## Top defects
- SPURIOUS: 25 (ví dụ frame adasind_019560.jpg)
- IGNORE_SCOPE: 9 (ví dụ frame adasind_270517.jpg)
- MISSING: 8 (ví dụ frame adasind_271039.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- **Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy**:
  1. *Lỗi SPURIOUS*: Chiếm tỷ trọng cao nhất (25 ca), tập trung chủ yếu ở center và mid zone. Nguyên nhân chính do `E4_model_domain` (model baseline được huấn luyện trên ảnh phối cảnh phẳng (pinhole/rectilinear) nên bị ngợp trước độ cong quang học của thấu kính fisheye, sinh box ảo trên nền kết cấu mặt đường và bóng râm). Ở phía annotator, một số box ở xa sát ranh giới ngưỡng $H=40$ px bị gán thừa (`E1_annotator_error`).
  2. *Lỗi WRONG_CLASS* (điển hình tại `adasind_271039.jpg L3` và `adasind_295948.jpg L2`): Méo phối cảnh ở mid zone kéo giãn hình học xe ba bánh (ThreeWheeler) và xe tải nhỏ (Truck), khiến góc nhìn nghiêng bị nhầm thành xe con (`Car`). Đây là sự kết hợp giữa nhận định chủ quan của người gán (`E1_annotator_error`) và thiếu ví dụ trực quan trong quy chuẩn (`E2_guideline_gap`).
- **Cách sửa và ai nhận việc (`owner`)**:
  - *Với lỗi nhầm class và box dưới ngưỡng*: Annotator thực hiện rà soát có đối chứng ở P5, sửa nhãn đúng theo R04 và R01 (`owner: annotator`).
  - *Với khoảng trống nhận diện hình học*: Đội ngũ phụ trách quy chuẩn cần bổ sung ảnh mẫu phân biệt xe ba bánh và xe tải nhỏ góc nhìn fisheye vào `20_guideline_patch.md` (`owner: guideline`).
  - *Với lỗi model domain*: Đội ngũ AI cần thu thập dữ liệu chuyên biệt trên camera fisheye để fine-tune mô hình phát hiện đối tượng thích ứng với đặc tính méo quang học (`owner: ai_team`).
- **Bằng chứng**:
  - Các dòng findings trong [submission/findings.csv](findings.csv): `adasind_271039.jpg L3+R6` (WRONG_CLASS), `adasind_295948.jpg L2+R1` (WRONG_CLASS), `adasind_270517.jpg L3+R2` (LR_noM).
  - Quy tắc viện dẫn: **R01** (ngưỡng $H \ge 40$ px), **R04** (phân loại chuẩn ThreeWheeler/Truck), **R05** (phân biệt truncated/occluded).
  - Minh chứng hình ảnh đối chiếu trong `submission/screenshots/` và `submission/r3_diag/model_compare.html`.
