# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 16.97 khớp có v > 0 mỗi người
- Tổng: v=2 384 | v=1 108 | v=0 1

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 22 | 7 | 0 | 24% |
| 1 | left_eye | 22 | 7 | 0 | 24% |
| 2 | right_eye | 23 | 6 | 0 | 21% |
| 3 | left_ear | 11 | 18 | 0 | 62% |
| 4 | right_ear | 17 | 12 | 0 | 41% |
| 5 | left_shoulder | 26 | 3 | 0 | 10% |
| 6 | right_shoulder | 28 | 1 | 0 | 3% |
| 7 | left_elbow | 26 | 3 | 0 | 10% |
| 8 | right_elbow | 26 | 3 | 0 | 10% |
| 9 | left_wrist | 19 | 10 | 0 | 34% |
| 10 | right_wrist | 20 | 9 | 0 | 31% |
| 11 | left_hip | 24 | 5 | 0 | 17% |
| 12 | right_hip | 25 | 4 | 0 | 14% |
| 13 | left_knee | 23 | 6 | 0 | 21% |
| 14 | right_knee | 25 | 4 | 0 | 14% |
| 15 | left_ankle | 25 | 4 | 0 | 14% |
| 16 | right_ankle | 22 | 6 | 1 | 21% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
