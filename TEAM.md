# TEAM — Ngày 12

Mã bộ ảnh: **G06** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Khoa Minh | 2A202603160 | có | Bạn cùng mã G06 (`peer_export_final.zip`) | 7 / 7 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- `D01.png` (`face.gaze_zone`): Tài xế vừa cúi nhẹ vừa đưa tay phải về phía bảng điều khiển/cần số giữa xe; phân vân giữa `center` và `lap`. Sau khi hỏi coach và đối chiếu mục 4.5, thống nhất giữ `center` vì hướng mặt và thao tác tay đang hướng vào cụm điều khiển trung tâm.

## Cá nhân

### NguyenKhoaMinh-2A202603160
- Phần mình làm: Tự gán đủ 22 ảnh cốt lõi (S01–S08 RGB+IR và D01–D06 NIR) cùng 4 ảnh mở rộng (S09–S10), chạy kiểm tra qua các mốc Checkpoint A, B, Final, đối chiếu 7 điểm khác biệt trong `disagreement_log.csv` và sửa lại 3 thuộc tính ở bản `export_final_v2.zip`.
- Điều mình học được hôm nay: Nắm vững quy ước gọi tên ghế theo chiều xe (`rear_right` ở bên trái ảnh OMS), quy ước trái/phải theo chủ thể trên ảnh xoay 90° (`y` mắt trái lớn hơn mắt phải), nguyên tắc không đoán nhãn qua kênh ảnh khác khi bị tối/lóa kính mà phải ghi `unknown`, và sự khác biệt bản chất giữa IR mô phỏng (SVIRO) với NIR thật (Drive&Act).
