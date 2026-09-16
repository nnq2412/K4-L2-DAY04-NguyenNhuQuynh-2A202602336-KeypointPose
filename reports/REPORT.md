# Báo cáo kết quả đánh giá (Evaluator)

## 1. Chỉ số trước khi sửa
- **OKS trung bình**: 0.928
- **OKS@0.50**: 1.000
- **OKS@0.75**: 1.000
- **Đánh giá mức độ**: Xuất sắc

## 2. Các lỗi cần sửa (ưu tiên cao nhất)
Dựa theo thứ tự ưu tiên (đảo trái/phải → nhầm người → thiếu/thừa người → xoá keypoint bị che → trượt hẳn → lệch nhẹ), evaluator đã tìm thấy:
- **1 Nhầm người**: `train_04.jpg` người #1 (left_wrist). Chấm rơi sang cơ thể bên cạnh.
- **5 Lệch nhẹ**: Sửa được, ít gây hại.
- _Lưu ý_: 100 điểm khác biệt cờ v=0 của gold chỉ là thông tin chẩn đoán, hãy tiếp tục tuân theo luật của lớp (bị che nhưng trong ảnh thì vẫn giữ v=1 và chấm vị trí).

## 3. Lỗi đã sửa & Lý do
*(Bạn ghi lại vào đây những gì bạn đã sửa trên CVAT nhé)*
- `train_04.jpg` (left_wrist): Đã kéo lại điểm cổ tay trái về đúng người số 1 thay vì nhầm sang người số 2.
- ...

## 4. Chỉ số sau khi sửa
*(Sẽ được điền sau khi bạn export lại từ CVAT và chạy lại evaluator)*
- **OKS trung bình**:
- **OKS@0.50**:
- **OKS@0.75**:
