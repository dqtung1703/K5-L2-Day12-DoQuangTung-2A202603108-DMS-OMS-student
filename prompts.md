# Khai báo dùng AI — Đỗ Quang Tùng

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Antigravity (AI assistant) | Tóm tắt đề bài Lab Ngày 12 và quy trình thực hiện theo hình thức cá nhân (nhóm 1 người) với gói G04 | Lập thứ tự làm việc từ Task 0 đến Task 4 và câu lệnh chạy `cabin_check.py` đúng tham số | Có, đối chiếu trực tiếp với `README.md`, `GUIDE.md`, `RULES.md` và `CHECKPOINTS.md` |
| 2 | Antigravity (AI assistant) | So sánh file `labels_cabin_v1.json` giảng viên mới gửi với file gốc trong `G04/` và giải thích ý nghĩa thuộc tính `occupied`, `facing`, thao tác copy shape trên CVAT | Hiểu rõ sự khác nhau ở `child_seat.occupied` và cách dùng `Ctrl+B` (Propagate) trên CVAT | Có, kiểm tra lại trong `GUIDE.md` và `scripts/cabin_schema.py` |
| 3 | Antigravity (AI assistant) | Giải thích các dòng `[WARN]`/`[ERROR]` trong `check_final.txt` và phân loại các nhóm bất đồng trong `disagreement_log.csv` khi diff với bạn Nguyễn Quốc Khánh | Xác định các lỗi cần sửa trên CVAT cho bản `export_final_v2.zip` (bổ sung `hand` ở `D03`, `child_seat` ở `S08_rgb`, sửa `eye_*` ở `D02`, `facing` ở `S02`, thu gọn box `phone` ở `D04`) và phát hiện lỗi xóa nhầm `face13`/`person` khi sửa | Có, tự mở lại từng ảnh trên CVAT kiểm tra thực tế và chạy lại `cabin_check.py` trên `export_final_v2.zip` |
| 4 | Antigravity (AI assistant) | Hỗ trợ soạn nháp và rà soát câu chữ cho `disagreement_log.csv`, `ir_log.csv`, `class_list_v0.md`, `self_review.md`, `TEAM.md` dựa trên các ghi nhận thực tế của mình | Hoàn thiện các file báo cáo đúng mẫu và đủ yêu cầu rubric | Có, tự đọc lại toàn bộ nội dung từng file trước khi đóng gói nộp |
