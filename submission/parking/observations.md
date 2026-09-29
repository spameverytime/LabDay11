# Quan sát vạch ô đỗ

- **Hai vạch `parking_line` đã vẽ**: Các vạch sơn trắng chia ô đỗ ở khu vực tiền cảnh (góc dưới bên phải và khu vực chính giữa tiền cảnh), phân chia các ô đỗ xe riêng biệt rõ ràng.
- **Một vạch/dấu sơn hoặc biên không vẽ, và vì sao**: Mép lề đường/biên giới hạn phía xa giáp hàng rào và các vệt sơn mờ sát mép biên không được vẽ thành `parking_line` vì chúng chỉ đóng vai trò ranh giới khu vực bãi/lối đi, không có chức năng phân tách hai ô đỗ xe riêng lẻ.
- **Polygon `free_space` dừng ở đâu; có phần bị che nào không**: Đã vẽ 2 polygon `free_space` bao phủ các lối xe chạy chính (lối đi phía tiền cảnh và lối đi xuyên ngang giữa bãi). Ranh giới polygon dừng ngay trước mép các vạch ô đỗ xe, lề biên bãi đỗ và dừng trước vị trí chiếc ô tô đỏ đỗ ở phía xa bên trái (không chạy xuyên qua xe hoặc vật cản).
- **Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”)**: Không có (các ô đỗ và lối đi trong bãi thể hiện rất thoáng và rõ ràng).
