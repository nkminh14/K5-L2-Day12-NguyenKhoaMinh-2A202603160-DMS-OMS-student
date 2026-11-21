# Tự đánh giá — Nguyễn Khoa Minh · G06

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S06_rgb.png` | `person` (`rear_left`) | `guess` | Ảnh RGB rất tối, vùng ngực người ngồi ghế `rear_left` chìm trong bóng tối nhưng ở bản v1 mình lỡ suy từ `S06_ir.png` sang để gán `seatbelt = not_worn` | Đã sửa thành `seatbelt = unknown` ở `export_final_v2.zip` |
| `S01_rgb.png` | `infant_seat`, `object`, `person` | `ok` | Đã kiểm tra kỹ hướng ghế theo xe: nôi em bé bên trái ảnh là `rear_right`, thùng carton ở `rear_middle`, người áo đỏ bên phải ảnh là `rear_left` | Không cần sửa (`ok`) |
| `D03.png` | `face` (`driver`) | `guess` | Đốm phản xạ đèn LED trên tròng kính che mắt trái tài xế, bản v1 mình gán nhầm `eye_left = closed` và bị `cabin_check` cảnh báo mâu thuẫn với 4 điểm `left_eye_*` có cờ `occluded=1` | Đã sửa thành `eye_left = unknown` ở `export_final_v2.zip` |
| `D05.png` | `face13` (`driver`) | `ok` | Trục mắt xếp dọc đúng theo người lái (`y` mắt trái lớn hơn mắt phải), 4 điểm vùng miệng bị chai nước che đều đã bật `occluded = 1` đầy đủ | Không cần sửa (`ok`) |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

- **Lỗi:** Thói quen "đoán trạng thái" (`guess`) thay vì chọn `unknown` khi chi tiết bị bóng tối hoặc đốm phản xạ che khuất (như đoán dây an toàn trên `S06_rgb.png` từ ảnh IR cùng cảnh, hoặc đoán trạng thái mắt/dây an toàn khi đang thao tác ở `D03.png`, `D06.png`).
- **Vì sao mình mắc:** Khi vừa xem ảnh `S06_ir.png` rất sáng rõ hoặc nhìn tổng thể tư thế tài xế, não có xu hướng tự điền thông tin còn thiếu vào ảnh đang gán.
- **Lần sau tránh bằng cách:** Luôn tự hỏi câu kiểm tra trong guideline trước khi chọn thuộc tính: *"Trên chính khung hình này mình có nhìn thấy trực tiếp khe mắt / mí mắt khép / dải dây đã cài xong hay không?"* — nếu không thấy trực tiếp trên khung đó thì chọn ngay `unknown` và bật cờ `occluded`.

## 3. Ghi chú về disagreement_log

- **Một dòng bạn của mình đúng và mình sai:** Dòng `S06_rgb.png | person | seatbelt` (mình gán `not_worn`, bạn gán `unknown`) và dòng `D06.png | person | seatbelt` (mình gán `worn_correct`, bạn gán `unknown`).
- **Mình học được gì từ dòng đó:** Mình nhận ra quy tắc 4.4-1 (không suy từ ảnh IR sang ảnh RGB cùng cảnh) và quy tắc 4.7 (đang thắt dở phải ghi `unknown`) rất quan trọng để không dạy model học từ dữ liệu nhiễu hoặc trạng thái chuyển tiếp chưa hoàn tất.
