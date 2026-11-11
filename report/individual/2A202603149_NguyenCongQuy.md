# Báo cáo thực hành Day 3

- Mã học viên theo lớp: 2A202603149
- Ngày thực hành: 11/11/2026. Môi trường: CVAT local.
- Công cụ: CVAT, SAM2, YOLO và script kiểm cấu trúc của repo. Tôi thao tác trong CVAT và hầu như không trực tiếp dùng SAM2 ở Easy và Medium. Codex hỗ trợ tạo đề xuất bằng YOLO và SAM2, rà và chỉnh mask, bổ sung nhãn ở Medium, gán nhãn Hard và sáu checkpoint, xuất ZIP và chuẩn bị báo cáo.

## 1. Bài đã nộp

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh Medium đầu tiên là `000000181542.jpg`. Vị trí mask vẽ tay đầu tiên cần đối chiếu lại. Bản lưu CVAT ghi mask người đi bộ giữa ảnh là `semi-auto`, nên chưa đủ để xác nhận đây là bản vẽ tay.
- Khi rà nhãn `person`, lấy đường viền phần người nhìn thấy, gồm quần áo, và dừng ở mép tiếp xúc với xe.
- Sau khi dùng gợi ý, Codex bổ sung mask xe buýt phía sau bên trái. Phần mask giao với xe và người ở trước được cắt theo các mask tiền cảnh.

## 3. Một lỗi đã tìm thấy và sửa

Trong ảnh Medium `000000181542.jpg`, chiếc bán tải sáng màu phía sau người đi bộ từng có nhãn `car`. Codex đối chiếu phần thùng chở hàng nhìn thấy và đổi nhãn thành `truck`, giữ biên mask. Đã lưu và xuất lại `medium_instance.zip`. Script của repo đọc được 69 mask RLE trong ZIP Medium và báo cấu trúc hợp lệ. Chưa có điểm đối chiếu reference.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Medium `000000181542.jpg`, góc dưới trái | Bánh xe đạp hoặc bánh xe máy | Chỉ thấy một đoạn bánh và chắn bùn ở mép ảnh | Để trống vì thiếu dấu hiệu xác định lớp |
| `cp1_holes`, kính chắn gió mô tô | Chi tiết thuộc xe hoặc vùng nền nhìn xuyên | Kính nằm bên trong viền chắn gió | Giữ phần kính trong mask xe. Các khe thực sự hở được để trống |
| Hard `000000350023.jpg`, đường chân trời bên trái | Tán cây hoặc biên công trình ở xa | Chi tiết nhỏ và các đường viền trùng nhau | Biên hiện tại là ước lượng theo đường nét nhìn được |
