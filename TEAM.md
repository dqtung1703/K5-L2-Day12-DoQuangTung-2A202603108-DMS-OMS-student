# TEAM — Ngày 12

Mã bộ ảnh: **G04** · Hình thức: **cá nhân**

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Đỗ Quang Tùng | 2A202603108 | có | Nguyễn Quốc Khánh (2A202603238) | 56 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- `S01_rgb`, `S01_ir`, `S03_rgb`, `S04_rgb`, `S08_ir` (`child_seat`): áp dụng thuộc tính `occupied = yes` theo file nhãn và rule cập nhật mới của giảng viên, nhưng `scripts/cabin_schema.py` trong repo gốc vẫn chỉ cho phép `unknown`/`no`.
- `D01` (`hand.on_wheel`, `eye_left`), `D03` (`seatbelt`, `eye_*`, `gaze_zone`), `D05`/`D06` (`gaze_zone`): các ca thuộc tính ranh giới mơ hồ đã ghi nhận `ambiguous` trong `disagreement_log.csv` để đối chiếu theo đáp án của coach.

## Cá nhân

### DoQuangTung-2A202603108
- Phần mình làm: Tự gán đủ 22 ảnh cốt lõi gói `G04` trên CVAT local, chạy kiểm tra Checkpoint A/B/final, đổi file `export_final.zip` để review chéo với bạn Nguyễn Quốc Khánh (`2A202603238`), tổng hợp 56 dòng trong `disagreement_log.csv`, gửi góp ý lại cho bạn Khánh và sửa các lỗi của mình thành `export_final_v2.zip`.
- Điều mình học được hôm nay: Cách ánh xạ ghế theo xe khi camera nhìn ngược, xử lý ảnh DMS xoay 90° theo trục y, dùng nguyên tắc `unknown` khi bị che/kính trên ảnh NIR, và giá trị của bước review chéo trong việc phát hiện lỗi bỏ sót đối tượng.
