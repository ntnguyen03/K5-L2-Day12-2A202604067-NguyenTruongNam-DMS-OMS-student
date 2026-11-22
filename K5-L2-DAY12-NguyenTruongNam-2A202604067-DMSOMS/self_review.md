# Tự đánh giá — Nguyễn Trường Nam · 2A202604067 · G09

## 1. Rà bốn ảnh từ bản export của CVAT

| Ảnh | Nhãn đã rà | Mục kiểm | Kết quả và xử lý |
| --- | --- | --- | --- |
| `S01_ir.png` | `object` ở `rear_middle` | `wrong_class` | Vùng túi ở giữa giữ vị trí gần như nhau trong dự đoán RGB và IR-sim. Giữ nhãn túi. Khi rà thủ công, xác nhận bằng đường viền và quai thay vì màu. |
| `S07_ir.png` | `object` ở `rear_right` | `guess` | Mô hình phát hiện thấy vùng giống túi, trong khi mô hình phân loại crop nghiêng về ghế trống. Dùng `other` cho đề xuất hiện tại và giữ ca này trong danh sách rà thủ công. |
| `D01.png` | `face.eye_left` | `guess` | Mặt chỉ được nhận diện sau khi cắt vùng đầu. Kết quả mô hình chưa đủ rõ để phân biệt mở và nhắm mắt trái. Giữ `unknown`. Chưa xác nhận điểm nào bị che nên giữ cờ hiện tại và giải thích cảnh báo trong log. |
| `D06.png` | `face13` | `lr_flip` | `left_eye_outer` có y cao hơn về trị số so với `right_eye_outer` (595,56 px và 441,88 px). Giữ nhãn trái/phải theo người trên ảnh xoay. |

## 2. Lỗi dễ lặp lại và cách tránh

Các mô hình có thể đổi lớp của cùng một vùng khi chuyển từ RGB sang IR-sim. Vùng nhô lên trên ghế dễ bị gọi nhầm là người hoặc túi. Khi rà lại, kiểm cả cặp ảnh, xem phần nào của vật thực sự nhìn thấy trong từng ảnh, rồi mới xác nhận lớp và thuộc tính đó. Dùng `unknown` cho trường có hỗ trợ khi thiếu bằng chứng quan sát.

## 3. Review chéo

Không thực hiện review chéo trong hồ sơ này. Phiếu tự kiểm mô hình ghi các ca cần xem lại trực tiếp trong task G09.
