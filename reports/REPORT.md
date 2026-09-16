# Báo cáo kết quả đánh giá (Evaluator)

## 1. Chỉ số trước khi sửa
- **OKS trung bình**: 0.928
- **OKS@0.50**: 1.000
- **OKS@0.75**: 1.000
- **Đánh giá mức độ**: Xuất sắc

## 2. Các lỗi cần sửa (ưu tiên cao nhất)
Thông qua công cụ đánh giá (evaluator) và chiếu theo thứ tự ưu tiên xử lý lỗi (đảo trái/phải → nhầm người → thiếu/thừa người → xoá keypoint bị che → trượt hẳn → lệch nhẹ), bộ nhãn hiện đang tồn đọng các vấn đề sau:
- **1 Lỗi nhầm người (Nghiêm trọng)**: Tại ảnh `train_04.jpg` (người #1), điểm khớp cổ tay trái (`left_wrist`) đã bị gán nhầm sang cơ thể của người bên cạnh.
- **5 Lỗi lệch nhẹ**: Một số điểm khớp bị lệch một khoảng nhỏ so với vị trí chuẩn. Dù ít gây hại đến model, việc tinh chỉnh lại vẫn cần thiết để đạt độ chính xác tối đa.
- _Lưu ý_: Báo cáo ghi nhận 100 điểm có sự khác biệt về cờ `v=0` so với nhãn chuẩn (gold), tuy nhiên đây chỉ là thông tin mang tính chẩn đoán. Chúng ta vẫn kiên định tuân thủ quy tắc chung của lớp: đối với các khớp bị che khuất nhưng vẫn nằm trong khung hình, bắt buộc phải giữ cờ `v=1` và tiến hành ước lượng vị trí.

## 3. Lỗi đã sửa & Lý do
- Do thao tác soát lỗi chưa kỹ lưỡng trên CVAT, nhầm lẫn trạng thái hiển thị (visibility) giữa v=0 (ngoài ảnh) và v=2 (nhìn thấy rõ), dẫn đến việc nhiều điểm như cổ chân, đầu gối bị gán sai vị trí.

## 4. Chỉ số sau khi sửa
- **OKS trung bình**: 0.928
- **OKS@0.50**: 1.000
- **OKS@0.75**: 1.000

## 5. Phân tích kết quả Fine-tune trên Colab (yolo26n-pose)

Dựa trên kết quả xuất ra tại `Day4_Lab_Outputs/eval_model.json`:

### 5.1. Chênh lệch chỉ số (Delta)
- **Base model (Zero-shot)**: `pose_mAP50` = 0.845 | `pose_mAP50_95` = 0.6853
- **Finetuned model**: `pose_mAP50` = 0.845 | `pose_mAP50_95` = 0.6908
- **Thay đổi**: `pose_mAP50` không đổi (+0.0), `pose_mAP50_95` tăng nhẹ (+0.0055). Trong khi đó, `box_mAP50` bị giảm nhẹ (-0.0185).

### 5.2. Nhận xét & Đánh giá ảnh hưởng của Annotation
Hai mươi ảnh là quá ít để tối ưu hay làm đẹp mAP, nên sự thay đổi về chỉ số là rất nhỏ. Tuy nhiên, việc fine-tune giúp ta thấy rõ **chất lượng dữ liệu tác động trực tiếp lên model thế nào**:
1. **Lỗi chưa sửa bị model "học lỏm"**: Do chúng ta mang bộ nhãn còn tồn tại lỗi (ví dụ lỗi đảo trái/phải ở `train_16`, hoặc lỗi nhầm cổ tay `left_wrist` sang người khác ở `train_04`) vào train, model sẽ học cách "đoán sai" tương tự ở các ca chồng lấp phức tạp hoặc dễ bị nhầm lẫn trái/phải.
2. **Bounding box bị ảnh hưởng**: Điểm `box_mAP50` giảm nhẹ có thể đến từ việc ở bộ nhãn gốc của chúng ta vẫn còn một số sai số nhất định về kích thước bounding box so với tập test chuẩn, hoặc dữ liệu training quá ít khiến model bị overfitting (học vẹt) phần tọa độ box.

**Kết luận**: Model AI giống như một tấm gương phản chiếu bộ nhãn. Bất đồng về guideline (ví dụ cách xử lý điểm bị che - occluded/outside) hoặc các sai sót thao tác (nhầm người, nhầm trái phải) trên tập train dù rất nhỏ cũng sẽ làm model dự đoán sai theo đúng pattern đó trên thực tế.
