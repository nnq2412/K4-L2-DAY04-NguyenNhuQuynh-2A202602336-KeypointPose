# Review Partner Report

## Lỗi tìm được

| Ảnh | Người thứ | Khớp | Lỗi gì | Sửa thế nào |
| --- | ---: | --- | --- | --- |
| train_16.txt | 1 | left_shoulder, right_shoulder | Vai trái/phải bị ngược chiều so với mắt | Đổi lại nhãn trái/phải trên CVAT |
| train_16.txt | 1 | left_hip, right_hip | Hông trái/phải bị ngược chiều so với mắt | Đổi lại nhãn trái/phải trên CVAT |
| train_01.txt | 1 | left_ankle | Điểm nằm ngoài ảnh (> 1.0) nhưng gán v=2 | Chuyển sang Outside (v=0) trên CVAT |
| train_01.txt | 2 | right_knee, right_ankle | Điểm nằm ngoài ảnh nhưng gán v=2 | Chuyển sang Outside (v=0) |
| train_04.txt | 1 | left/right knee & ankle | Điểm nằm ngoài ảnh nhưng gán v=2 | Chuyển sang Outside (v=0) |
| train_04.txt | 2 | box | Bounding box không nằm trong [0, 1] | Chỉnh lại box không vượt mép ảnh |
| train_04.txt | 2 | Nhiều khớp | Nằm ngoài ảnh nhưng gán v=2 | Chuyển sang Outside (v=0) |
| train_07.txt | 1 | left_ankle, right_ankle | Nằm ngoài ảnh nhưng gán v=2 | Chuyển sang Outside (v=0) |
| train_10.txt | 1 | box | Bounding box không nằm trong [0, 1] | Chỉnh lại box không vượt mép ảnh |
| train_10.txt | 1 | left/right knee & ankle | Nằm ngoài ảnh nhưng gán v=2 | Chuyển sang Outside (v=0) |
| train_11.txt | 1 | left_ankle | Nằm ngoài ảnh nhưng gán v=2 | Chuyển sang Outside (v=0) |
| train_13.txt | 2 | box | Bounding box không nằm trong [0, 1] | Chỉnh lại box không vượt mép ảnh |
| train_13.txt | 2 | left/right knee & ankle | Nằm ngoài ảnh nhưng gán v=2 | Chuyển sang Outside (v=0) |
| train_13.txt | 3 | left_ankle, right_ankle | Nằm ngoài ảnh nhưng gán v=2 | Chuyển sang Outside (v=0) |

## Hai câu kết luận

- Lỗi lặp đi lặp lại nhiều nhất của bài này: Nhầm lẫn giữa Visible (v=2) và Outside (v=0) cho các điểm nằm ngoài mép ảnh, cũng như kéo bounding box vượt ra ngoài khung hình.
- Nó là lỗi **thao tác** hay lỗi **guideline chưa rõ**: Chủ yếu là lỗi thao tác do không kiểm tra kỹ trạng thái visibility trên CVAT cho các điểm bị khuất hoặc bị cắt bởi viền ảnh.
