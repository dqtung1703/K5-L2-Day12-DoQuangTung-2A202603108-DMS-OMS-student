# Danh sách lớp v0 — Đỗ Quang Tùng · G04

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `eye_left` / `eye_right` | `open` / `closed` / `unknown` | Phát hiện buồn ngủ, chớp mắt kéo dài (PERCLOS) để cảnh báo tài xế kịp thời | Có, trừ khi bị chói LED trên kính hoặc kính râm dày che khuất |
| 2 | `face13` (13 điểm mặt) | 13 điểm tọa độ + cờ `occluded` / `outside` | Ước lượng tư thế đầu (head pose: yaw/pitch/roll), độ mở mắt (EAR) và độ mở miệng (ngáp) | Có, ngoại trừ các điểm bị che bởi tay, kính phản xạ hoặc góc quay lớn |
| 3 | `gaze_zone` | `road` / `mirror_l` / `mirror_r` / `mirror_c` / `cluster` / `center` / `lap` / `other` | Phát hiện mất tập trung (rời mắt khỏi đường quá lâu) và phân biệt quan sát gương hợp lệ với nhìn màn hình/đùi | Có (dựa vào hướng đầu và mắt), giảm độ chính xác khi mắt bị kính che |
| 4 | `glasses` | `none` / `clear` / `sun` / `unknown` | Điều chỉnh ngưỡng tin cậy của thuật toán theo dõi mắt/đồng tử khi tài xế đeo kính cận hoặc kính râm | Một phần: thấy gọng kính rõ, nhưng kính râm có thể trông trong suốt trên NIR nên dễ nhầm `clear` với `sun` |
| 5 | `hand` (`whose`, `side`, `on_wheel`) | `driver`/`passenger` · `left`/`right` · `yes`/`no`/`unknown` | Kiểm tra tài xế có đặt tay lên vô lăng (hands-on-wheel) để hỗ trợ chuyển giao quyền điều khiển ADAS/tự lái | Có (dựa vào hình dạng bàn tay và vị trí so với vô lăng) |
| 6 | `phone` (`state`) | `held` / `mounted` / `lap` | Cảnh báo hành vi sử dụng điện thoại gây mất tập trung khi lái xe | Có nếu thấy rõ cạnh/góc/màn hình sáng; khó hơn khi máy tối màu bị ngón tay che |
| 7 | `person.seatbelt` (tài xế) | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Cảnh báo tài xế chưa thắt dây hoặc thắt dây sai cách (luồn dưới nách, sau lưng) | Có nếu có tương phản giữa dải dây và áo; khó thấy trên áo tối đồng màu hoặc bị tay che |

## OMS (7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`) | `rear_left` / `rear_middle` / `rear_right` / `front_passenger` | Xác định số lượng và vị trí hành khách trên từng ghế để kích hoạt/điều chỉnh túi khí và cảnh báo an toàn | Có (dựa vào hình dạng cơ thể), kể cả trong cabin tối |
| 2 | `person.seatbelt` (hành khách) | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Nhắc nhở hành khách hàng ghế sau/trước thắt dây an toàn đúng cách (seatbelt reminder) | Hạn chế khi quần áo tối màu trùng độ sáng với dây an toàn |
| 3 | `face` (OMS) | Bounding box khuôn mặt | Hỗ trợ xác nhận sự hiện diện của người ngồi và phân biệt người thật với đồ vật/ghế trống | Có, rõ hơn RGB trong điều kiện thiếu sáng |
| 4 | `child_seat` (`seat`, `occupied`) | `seat` · `no` / `unknown` (và `yes` theo rule cập nhật) | Phát hiện vị trí lắp ghế trẻ em và tình trạng có trẻ ngồi để cảnh báo bỏ quên trẻ trong xe (CPD) | Có (hình dạng ghế đặc trưng); phần bên trong khó thấy nếu bị che/tối |
| 5 | `infant_seat` (`seat`, `facing`) | `seat` · `rear` / `front` | Nhận diện nôi em bé và hướng lắp (quay sau/quay trước) để tự động ngắt túi khí tương ứng và cảnh báo quên trẻ | Có (dựa vào hình dáng nôi và lưng nôi quay hướng nào) |
| 6 | `object` (`seat`, `type`) | `bag` / `box` / `cup` / `other` | Phân biệt đồ vật đặt trên ghế với người ngồi để tránh báo động giả dây an toàn (false SBR) và nhắc đồ bỏ quên | Có về hình dạng/vị trí, nhưng mất thông tin màu sắc nên khó phân biệt chất liệu |
| 7 | `frame_meta` (`modality`, `light`, `camera_blocked`) | `rgb`/`ir` · `day`/`night`/`unknown` · `yes`/`no` | Phát hiện camera bị che khuất (occlusion/tampering) để báo lỗi hệ thống và chọn pipeline xử lý phù hợp với ảnh màu/hồng ngoại | Có (`camera_blocked` phát hiện trực tiếp trên khung hình IR) |

## 2 câu hỏi leo thang

1. **Câu hỏi:** Trong gói `G04` có các khung hình xuất hiện hình trẻ em/búp bê ngồi trong ghế trẻ em, và giảng viên đã cập nhật file `labels_cabin_v1.json` bổ sung giá trị `child_seat.occupied = yes`, nhưng Guideline v1.0 gốc và `scripts/cabin_schema.py` vẫn chỉ cho phép `no` và `unknown`. Trong phiên bản Guideline v1.1 tới, nên thống nhất cho phép `occupied = yes` trong cả schema/script kiểm tra hay tách riêng trẻ em thành một lớp `child` riêng bên trong `child_seat`?
   - **Khung ví dụ:** `S01_rgb.png`, `S01_ir.png`, `S03_rgb.png`, `S04_rgb.png`, `S08_ir.png` (gói `G04`).
   - **Bạn tạm gán thế nào và vì sao:** Tạm gán `child_seat` với `occupied = yes` theo đúng file nhãn và quy định cập nhật mới của giảng viên, đồng thời ghi chú rõ sự lệch phiên bản với `cabin_schema.py` gốc.

2. **Câu hỏi:** Khi tài xế đeo kính trong trên ảnh NIR thật làm vùng mắt bị mờ, không phân biệt được mắt mở hay nhắm nhưng vẫn ước lượng tương đối được vị trí mắt sau tròng kính, ranh giới cụ thể để gắn cờ `occluded` so với `outside` cho 8 điểm mắt của `face13` là gì? (Trong review chéo, đây là điểm dễ gây bất đồng hàng loạt trên cả 8 điểm mắt).
   - **Khung ví dụ:** `D02.png` (gói `G04`).
   - **Bạn tạm gán thế nào và vì sao:** Sau khi review chéo với bạn cùng mã, mình đổi `eye_left` và `eye_right` sang `unknown` theo luật 4.4-1/4.5 và gắn cờ cho các điểm mắt bị che không rõ trong `export_final_v2.zip` thay vì giữ trạng thái mặc định như bản đầu.
