# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao?
   - **Trả lời**: Đây **không phải lỗi `DUPLICATE`**, mà bắt buộc cần một **quy tắc riêng (cross-camera fusion policy)**. Trong hệ thống SVM 360°, hai camera liền kề (như front và left) có vùng nhìn chồng lấn vật lý (overlap seam). Một vật thể thực tại seam xuất hiện trên cả 2 camera là hoàn toàn tự nhiên và cả hai box đều là nhãn hợp lệ (valid observations) trên không gian ảnh 2D của từng sensor. Lỗi DUPLICATE chỉ xảy ra khi cùng một camera vẽ nhiều box đè lên cùng một vật thể. Việc gộp hai box thành một thực thể duy nhất phải được giải quyết ở tầng hợp nhất dữ liệu (sensor fusion / BEV projection), không thể tùy tiện coi một trong hai box là lỗi thừa.

2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.
   - **Trả lời**:
     - *Giữ cùng track ID*: Khi vật thể di chuyển liên tục trong khung hình với quỹ đạo mượt mà, có thể suy đoán vị trí dù bị che khuất tạm thời (short occlusion) mà không đổi nhân dạng.
     - *Thêm keyframe*: Khi vật thể thay đổi đột ngột về hướng chuyển động, thay đổi góc nhìn/hình dáng (pose change) hoặc chuyển đổi tương tác (như người dắt xe bắt đầu ngồi lên xe để lái).
     - *Trạng thái Outside*: Khi vật thể đi hoàn toàn ra ngoài vòng tròn nhìn thấy của thấu kính (vượt qua lens border hoặc mép ảnh) để tránh model nội suy sai vị trí khi vật không còn trong tầm nhìn.
     - *Bằng chứng cần trước khi nối track qua hai camera*: (1) Đồng bộ xung thời gian phần cứng chuẩn mili-giây (hardware timestamp synchronization); (2) Ma trận hiệu chuẩn ngoại suy (extrinsic calibration) chính xác để chiếu tọa độ về cùng mặt phẳng Bird's Eye View (BEV); (3) Sự tương thích về vector vận tốc và khoảng cách không gian (spatial-temporal continuity) để đảm bảo không gộp nhầm hai phương tiện khác nhau đi gần nhau ở vùng ranh giới.

3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?
   - **Trả lời**:
     - *Tình huống*: Tại frame `adasind_271039.jpg` đối tượng `L3+M12`, cả tôi và mô hình YOLO đều phát hiện một phương tiện di chuyển ở phía xa bên trái ($w=44.4, h=43.0\text{ px} \ge 40\text{ px}$), nhưng teaching reference lại bỏ sót đối tượng này (tạo ra conflict `LM_noR`).
     - *Cách xử lý*: Tôi đã không mù quáng xóa nhãn của mình để khớp số với reference, mà bảo vệ quyết định bằng cách phân loại nguyên nhân `E0_reference_defect` với hành động `action=escalate` trong `findings.csv`, lập phiếu leo thang chi tiết tại `30_escalation_ticket.md` kèm ảnh chụp minh chứng `conflict_271039_L3_M12.jpg` và ghi nhận vào nhật ký quyết định `40_decision_log.csv` (mã `D-03`).
     - *Rút kinh nghiệm*: Nếu làm lại slice này, tôi sẽ đo kiểm kích thước pixel cẩn thận ngay từ đầu để loại trừ sớm các box nhỏ mấp mé dưới ngưỡng 40px (như chiếc xe $h=25\text{ px}$ trên frame 2), đồng thời kiểm tra kỹ góc nhìn nghiêng của các xe ba bánh và xe tải nhỏ ở mid zone để tránh lỗi nhầm class ngay từ vòng nháp.
