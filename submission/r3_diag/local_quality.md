# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `23f89abbc030fd7c28a342362f530ca5f0164ed25209c581efda35142cce846a`; slice `B4-center`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_270517.jpg, adasind_271039.jpg, adasind_295948.jpg. Frame thiếu trong export: không.
TP=16; FP=8; FN=4; số lần đối chiếu=25; mean IoU của TP=0.837.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.640 | 0.904 | 0.840 |
| precision | 0.667 | 0.648 | 0.500 |
| recall | 0.800 | 0.815 | 0.667 |
| jaccard | 0.571 | 0.553 | 0.500 |
| dice | 0.727 | 0.710 | 0.667 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 1 | 1 | 0.920 | 0.667 | 0.667 | 0.500 | 0.667 |
| Car | 4 | 3 | 1 | 0.840 | 0.571 | 0.800 | 0.500 | 0.667 |
| Pedestrian | 6 | 2 | 1 | 0.880 | 0.750 | 0.857 | 0.667 | 0.800 |
| ThreeWheeler | 3 | 1 | 1 | 0.920 | 0.750 | 0.750 | 0.600 | 0.750 |
| Truck | 1 | 1 | 0 | 0.960 | 0.500 | 1.000 | 0.500 | 0.667 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_270517.jpg | 7 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_271039.jpg | 8 | 4 | 2 | 0.615 | 0.667 | 0.800 |
| adasind_295948.jpg | 1 | 4 | 2 | 0.200 | 0.200 | 0.333 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 0 | 1 | 0 | 0 | 0 |
| Car | 0 | 4 | 0 | 0 | 1 | 0 |
| Pedestrian | 0 | 0 | 6 | 0 | 0 | 1 |
| ThreeWheeler | 0 | 1 | 0 | 3 | 0 | 0 |
| Truck | 0 | 0 | 0 | 0 | 1 | 0 |
| <extra> | 1 | 2 | 1 | 1 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
