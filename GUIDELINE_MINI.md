# Mini guideline - nhóm: SOLO |  người gán: Nguyễn Như Quỳnh  |  ngày: 17/09/2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | Gắn v=1 (occluded) và ước lượng vị trí | Bị lớp vải che khuất hoàn toàn bề mặt thật |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | Gắn v=1 nếu bị che một phần | Không thấy rõ điểm chuẩn của tai |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Các khớp ngoài ảnh gắn v=0 | Khớp không tồn tại trong khung hình |
| Cổ tay nằm sau tay lái / sau thân mình | Gắn v=1 và ước lượng vị trí | Vẫn nằm trong ảnh nhưng bị vật khác che |
| Hai người chồng lên nhau | Gắn v=1 cho khớp của người bị che | Khớp nằm trong ảnh nhưng không nhìn thấy trực tiếp |
| Người nhỏ đến mức nào thì không gán nữa | Dưới 20x20 pixel | Không thể nhận diện chính xác các khớp |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_16`, người thứ `1`, khớp `vai và hông`

- Mơ hồ ở chỗ nào: Người chụp quay lưng hay quay mặt lại phía camera dẫn đến khó xác định trái/phải.
- Bạn quyết thế nào: Dựa vào hướng của bàn chân/tay để phân biệt bên trái và phải, hoặc sửa lại trên CVAT.
- Vì sao: Để đảm bảo tính nhất quán của cơ thể.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model sẽ nhầm lẫn trái phải, ảnh hưởng đến bài toán nhận diện tư thế.

### Ca 2 - ảnh `train_04`, người thứ `2`, khớp `box`

- Mơ hồ ở chỗ nào: Bounding box vượt ra ngoài giới hạn ảnh (không chuẩn hóa trong [0, 1]).
- Bạn quyết thế nào: Cần giới hạn box lại trong viền ảnh khi gán.
- Vì sao: Format YOLO yêu cầu box chuẩn hoá trong giới hạn [0, 1].
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model YOLO sẽ lỗi hoặc loss tính sai khi toạ độ > 1.

### Ca 3 - ảnh `train_01`, người thứ `1`, khớp `left_ankle`

- Mơ hồ ở chỗ nào: Khớp nằm ngoài mép ảnh (bị cắt) nhưng ban đầu bị gán v=2 thay vì v=0.
- Bạn quyết thế nào: Bắt buộc chọn trạng thái "Outside of image" (v=0).
- Vì sao: Nếu điểm nằm ngoài khung hình thì không được tính là visible hay occluded.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model học toạ độ ảo nằm ngoài ảnh gây nhiễu mô hình.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `left_ear` (bạn `62%` / họ `30%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: Một bên dùng Outside thay cho Occluded cho những điểm bị tóc che khuất.
- Luật mới bổ sung vào mục 2 sau khi thống nhất: Khớp bị che khuất nhưng vẫn nằm trong ảnh phải gắn v=1 (Occluded), chỉ dùng v=0 (Outside) khi thực sự ra ngoài mép ảnh.
