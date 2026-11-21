# Danh sách lớp v0 — Nguyễn Khoa Minh · G06

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (7 lớp / thuộc tính)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `face` (`eye_left`, `eye_right`) | `open` / `closed` / `unknown` | Theo dõi tần suất chớp mắt (PERCLOS) và thời gian nhắm mắt liên tục để phát hiện tài xế buồn ngủ hoặc ngủ gật | Có trên NIR cả ngày lẫn đêm, trừ khi tròng kính bị lóa đèn LED (như `D03.png`) hoặc góc cúi sâu (`D02.png`) |
| 2 | `face` (`glasses`) | `none` / `clear` / `sun` / `unknown` | Đánh giá độ tin cậy của bộ phát hiện mắt và hướng nhìn; chọn chế độ xử lý lóa kính hoặc cảnh báo khi kính râm che mắt | Có, nhưng trên NIR tròng kính râm đôi khi bị nhìn xuyên qua giống kính thường nên cần chú ý gọng và độ tối |
| 3 | `face` (`gaze_zone`) | `road` / `mirror_l` / `mirror_r` / `mirror_c` / `cluster` / `center` / `lap` / `other` | Phát hiện xao nhãng thị giác (visual distraction) khi tài xế rời mắt khỏi mặt đường quá ngưỡng thời gian an toàn | Có khi thấy rõ đồng tử và hướng đầu; khó phân biệt giữa `center` và `lap` nếu mắt bị che |
| 4 | `face13` (skeleton 13 điểm) | Tọa độ (x, y) + cờ `occluded` / `outside` | Ước lượng tư thế đầu 3D (yaw, pitch, roll), độ mở miệng (ngáp khi mệt mỏi) và độ mở mí mắt | Có nếu khuôn mặt đủ lớn (rộng từ 60 px trở lên); các điểm bị vật cản như chai nước (`D05.png`) phải gắn cờ `occluded` |
| 5 | `hand` (`whose`, `side`, `on_wheel`) | `driver`/`passenger` · `left`/`right` · `yes`/`no`/`unknown` | Kiểm tra tay tài xế có đặt trên vô lăng hay không (hands-on-wheel detection), đặc biệt quan trọng khi chuyển giao quyền lái L2/L3 | Có, bàn tay phản xạ NIR rất rõ; dễ tách tay trái/phải của tài xế với tay hành khách |
| 6 | `phone` (`state`) | `held` / `mounted` / `lap` | Cảnh báo hành vi sử dụng điện thoại khi lái xe (gọi điện áp tai như `D04.png` hoặc cầm nhắn tin) gây mất tập trung nhận thức và thao tác | Có, nhận diện tốt qua hình dáng cạnh máy và vị trí bàn tay cầm, dù không có màu sắc màn hình |
| 7 | `person` (`seat=driver`, `seatbelt`) | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Xác nhận vị trí tài xế và kiểm tra dây an toàn được thắt đúng quy cách qua vai xuống hông (phát hiện thắt sai hoặc đang thắt dở như `D06.png`) | Có, dải dây an toàn tạo tương phản rõ trên áo sáng màu dưới đèn NIR, nhưng khó thấy hơn nếu áo tối màu |

## OMS (6 lớp / thuộc tính)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`, `seatbelt`) | `rear_left` / `rear_middle` / `rear_right` · `not_worn` / `unknown` ... | Biết chính xác ghế nào có hành khách để nhắc thắt dây an toàn theo từng vị trí ghế và điều chỉnh lực bung túi khí | Có, thậm chí trên ảnh tối như `S06_ir.png` còn thấy rõ người và vùng ngực hơn bản `S06_rgb.png` |
| 2 | `face` (hành khách OMS) | Hộp giới hạn khuôn mặt | Xác định hướng đầu và vị trí phần trên cơ thể hành khách để tối ưu hướng túi khí rèm và theo dõi trạng thái hành khách | Có, hình khối khuôn mặt giữ nguyên trên ảnh IR dù mất màu da |
| 3 | `infant_seat` (`seat`, `facing`) | `rear` / `front` theo ghế | Nhận diện nôi trẻ sơ sinh (đặc biệt loại quay ngược `facing=rear` như `S01`, `S02`) để cảnh báo bỏ quên trẻ (CPD) và khóa túi khí nếu lắp ghế trước | Có, khung nôi và tay xách nhìn rất rõ qua hình dạng hình học trên IR |
| 4 | `child_seat` (`seat`, `occupied`) | `no` / `unknown` theo ghế | Phát hiện ghế trẻ em trên hàng ghế sau (`S02`, `S03`, `S04`, `S06`, `S07`, `S08`) và kiểm tra trạng thái có vật/người bên trong để hỗ trợ hệ thống an toàn cabin | Có, trên ảnh IR-sim (`S06_ir.png`, `S07_ir.png`) lòng ghế sáng rõ hơn hẳn so với vùng tối đen trên ảnh RGB |
| 5 | `object` (`seat`, `type`) | `bag` / `box` / `cup` / `other` | Phân biệt đồ vật bỏ quên hoặc hành lý (thùng carton ở `S01`, `S03`; cốc ở `S03`, `S04`, `S05`; túi ở `S09`) với người/trẻ em để tránh báo động giả | Có về mặt hình dạng, nhưng mất màu sắc nên những vật tối màu hoặc bề mặt đồng nhất cần dựa vào đường viền |
| 6 | `frame_meta` (`modality`, `light`, `camera_blocked`) | `rgb`/`ir` · `day`/`night`/`unknown` · `yes`/`no` | Cung cấp thông tin ngữ cảnh toàn khung hình để hệ thống chọn nhánh model (RGB hay IR) và báo lỗi ngay nếu camera bị che khuất (`camera_blocked=yes`) | Có, xác định trực tiếp từ cảm biến và độ sáng/độ rõ toàn ảnh |

## 2 câu hỏi leo thang

1. **Câu hỏi:** Trong các cảnh có búp bê/mô hình trẻ em đặt nằm trong nôi hoặc ngồi trên ghế trẻ em (mục 3 GUIDE nói bộ ảnh không có trẻ em ngồi, còn quy đổi SVIRO ở mục 4.2 chỉ có `infant_seat` và `child_seat` với `occupied = no` hoặc `unknown`), khi triển khai thực tế nếu có mô hình thử nghiệm (dummy) hoặc búp bê đồ chơi kích thước lớn trong ghế trẻ em thì khách hàng muốn gán thêm một box `object` (`type=other`) nằm trong `child_seat`/`infant_seat` hay chỉ giữ box ghế với thuộc tính riêng?
   - **Khung ví dụ:** `S01_rgb.png`, `S03_rgb.png`, `S06_ir.png`, `S07_ir.png`
   - **Bạn tạm gán thế nào và vì sao:** Em tuân thủ đúng Guideline v1.0 mục 3 và 4.2 (không tự ý gán trẻ em, chỉ gán box `infant_seat` hoặc `child_seat` theo ghế xe, và ở các cảnh tối như `S06_rgb.png`, `S07_rgb.png` không nhìn rõ lòng ghế thì gán `occupied = unknown`, còn khi thấy rõ bề mặt ghế theo quy đổi SVIRO thì gán `occupied = no`). Cách này tránh tạo nhãn sai schema (`occupied` không có giá trị `yes`) và giữ nhất quán với tập kiểm tra.

2. **Câu hỏi:** Khi tài xế đang dùng tay kéo dây an toàn qua ngực (đang trong quá trình thao tác thắt hoặc tháo dây, dây đã vắt chéo qua người nhưng tay vẫn giữ gần khóa và chưa rõ chốt đã vào ngàm hay chưa), guideline muốn quy định ngưỡng nào giữa `worn_correct`, `worn_incorrect` và `unknown`?
   - **Khung ví dụ:** `D06.png`
   - **Bạn tạm gán thế nào và vì sao:** Ở bản đầu em từng phân vân với `worn_correct`, nhưng sau khi đối chiếu quy tắc 4.7 ("`unknown`: không thấy (tối, bị che, đang thắt dở)"), em đã thống nhất với bạn review chéo và sửa thành `seatbelt = unknown` ở bản v2 vì cả hai tay tài xế đang cầm trên dải dây ở trạng thái thắt dở.
