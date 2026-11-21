# Khai báo dùng AI — Nguyễn Khoa Minh

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Trợ lý AI trong IDE | Giải thích cấu trúc repo, thứ tự thực hiện các bước Checkpoint A, B, Final và cú pháp chạy script `cabin_check.py`, `rgb_ir_diff.py` | Dùng để nắm quy trình làm bài và chạy lệnh kiểm tra đúng chuẩn UTF-8 trên Windows | Có, kiểm tra lại bằng `python scripts/cabin_check.py --help` và đọc đối chiếu `CHECKPOINTS.md`, `GUIDE.md` |
| 2 | Trợ lý AI trong IDE | Góp ý cách diễn đạt chức năng DMS/OMS cho bảng `class_list_v0.md` và cách trình bày câu hỏi leo thang rõ ý | Chỉnh sửa lại câu chữ theo đúng các lớp trong `labels_cabin_v1.json` và gắn với khung hình ví dụ đã quan sát | Có, tự đối chiếu từng thuộc tính với Guideline Cabin v1.0 mục 4.1–4.8 |
