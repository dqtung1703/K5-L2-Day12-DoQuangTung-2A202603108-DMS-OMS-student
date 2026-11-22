# Tự đánh giá — Đỗ Quang Tùng · G04

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S02_rgb.png` | `infant_seat` | `wrong_class` (thuộc tính `facing`) | Nhầm hướng `facing` của nôi em bé (`front` thay vì `rear` khi lưng nôi quay về phía camera) | Đã sửa sang `rear` ở `export_final_v2.zip` |
| `S08_rgb.png` | `child_seat` | `missing` | Ảnh RGB gốc quá tối nên bỏ sót `child_seat`; khi tăng Brightness/Contrast trên CVAT mới thấy rõ | Đã bổ sung ở `export_final_v2.zip` |
| `D02.png` | `face` & `face13` | `guess`, `flag` | Tài xế đeo kính trong, không rõ mắt mở hay nhắm nhưng bản đầu đoán `open` và thiếu cờ cho các điểm mắt | Đã đổi sang `unknown` và cập nhật cờ ở `export_final_v2.zip` |
| `D03.png` | `hand` | `missing` | Bỏ sót 2 box bàn tay của tài xế trong bản đầu | Đã bổ sung đủ 2 box `hand` ở `export_final_v2.zip` |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

- **Lỗi:** Sót đối tượng hoặc bỏ qua bước kiểm tra kỹ chi tiết nhỏ (quên 2 box `hand` ở `D03`, quên tăng sáng kiểm tra ảnh tối ở `S08_rgb`, hộp `phone` ở `D04` còn hơi thừa mép, và suýt xóa nhầm `face13`/`person` khi sửa sang v2).
- **Vì sao mình mắc:** Chuyển ảnh nhanh và làm gộp nhiều thao tác chỉnh sửa mà không đối chiếu lại bảng checklist đối tượng theo từng ảnh và không tăng Brightness/Contrast ngay cho ảnh tối.
- **Lần sau tránh bằng cách:** Luôn đi đúng thứ tự cố định trên mỗi ảnh (`frame_meta` → `person` → `face` → `face13` → `hand` → `phone` cho DMS; tăng sáng kiểm tra ảnh tối cho OMS), và luôn so tổng số lượng đối tượng giữa bản cũ và bản mới sau mỗi lần chỉnh sửa trên CVAT.

## 3. Ghi chú về disagreement_log

- **Một dòng bạn của mình đúng và mình sai:** Dòng `D02.png | face | eye_left / eye_right` (mình ghi `open`, bạn Nguyễn Quốc Khánh ghi `unknown` kèm gắn cờ cho các điểm mắt) và dòng `D03.png | hand | box` (mình bỏ sót 2 bàn tay, bạn Khánh vẽ đủ).
- **Mình học được gì từ dòng đó:** Phải tuân thủ chặt quy tắc "không thấy rõ thì chọn `unknown`" thay vì suy đoán khi mắt nằm sau tròng kính trên ảnh NIR, và việc review chéo độc lập giúp phát hiện ngay các lỗi bỏ sót (như thiếu `hand`, thiếu `child_seat` ở ảnh tối) mà bản thân rất dễ nhìn lướt qua.
