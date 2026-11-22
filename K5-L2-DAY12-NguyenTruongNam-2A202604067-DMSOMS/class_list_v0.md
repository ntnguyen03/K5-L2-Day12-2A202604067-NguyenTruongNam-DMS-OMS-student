# Danh sách lớp v0 — Nguyễn Trường Nam · 2A202604067

Mã bộ ảnh G09. Các trường dưới đây lấy từ Guideline Cabin v1.0. Cột chức năng mô tả cách hệ thống có thể dùng nhãn sau khi huấn luyện.

## DMS — Giám sát tài xế

| Trường | Giá trị hoặc dạng gán | Model cần nhận ra để làm gì? | Điều kiện trên NIR |
| --- | --- | --- | --- |
| `face.eye_left`, `face.eye_right` | `open`, `closed`, `unknown` cho từng mắt | Ước lượng chớp mắt và tổng thời gian nhắm mắt qua nhiều khung hình. | Chọn `unknown` khi không thấy rõ hai mí, chẳng hạn do phản xạ kính. |
| `face.gaze_zone` | `road`, `mirror_l`, `mirror_r`, `mirror_c`, `cluster`, `center`, `lap`, `other` | Phân biệt nhìn đường, liếc gương và nhìn những vùng khác để ước lượng thời gian rời mắt khỏi đường. | Cần thấy hướng mặt hoặc mắt đủ rõ. Trường hợp không chắc dùng `other` và ghi lý do. |
| `face.glasses` | `none`, `clear`, `sun`, `unknown` | Giúp hệ thống nhận biết khi kính có thể làm dấu hiệu về mắt kém tin cậy. | Một số kính râm trông trong trên NIR. Dùng `unknown` khi thiếu dấu hiệu phân biệt. |
| `face13` | 13 điểm mặt với cờ `occluded` hoặc `outside` khi cần | Cung cấp hình học để ước lượng hướng đầu và mức mở mi mắt. | Phụ thuộc kích thước mặt và độ che khuất. Mặt dưới 60 px chỉ gán box `face`. |
| `hand.on_wheel` | `yes`, `no`, `unknown`. Ghi `whose` và `side` | Ước lượng trạng thái tay trên vô lăng trong ngữ cảnh vận hành. | Chỉ xác nhận tiếp xúc khi thấy rõ. `no` mô tả tư thế trong ảnh. |
| `phone.state` | `held`, `mounted`, `lap` | Phân biệt cách đặt hoặc cầm điện thoại để đánh giá khả năng xao nhãng. | Cần thấy ít nhất cạnh, góc hoặc màn hình của máy. |
| `person.seatbelt` | `worn_correct`, `worn_incorrect`, `not_worn`, `unknown` | Phân biệt tài xế có thắt dây và cách đeo để hỗ trợ cảnh báo. | Cần thấy đường đi của dây qua vai và thân. Dây còn khuất thì dùng `unknown`. |

## OMS — Giám sát khoang hành khách

| Lớp hoặc trường | Giá trị hoặc dạng gán | Model cần nhận ra để làm gì? | Điều kiện trên IR-sim |
| --- | --- | --- | --- |
| `person` | Box cơ thể nhìn thấy và `seat` theo xe | Xác định ghế có hành khách để hỗ trợ logic theo vị trí ghế. | Thường nhận được từ hình dáng cơ thể khi còn đủ tương phản. |
| `person.seatbelt` | `not_worn` hoặc `unknown` trên SVIRO | Hỗ trợ kiểm tra dây theo từng hành khách. Dữ liệu bài lab chỉ có hai giá trị này. | `not_worn` khi nhìn rõ không có dây. Vùng dây bị tối hoặc che thì `unknown`. |
| `child_seat` | Box ghế trẻ em, `seat`, `occupied=no` hoặc `unknown` | Nhận biết ghế trẻ em và phân biệt tình trạng có thể quan sát được bên trong ghế. | Nhận biết từ khung và lòng ghế. Khi lòng ghế bị che, dùng `unknown`. |
| `infant_seat` | Box nôi xách, `seat`, `facing=rear` hoặc `front` | Xác định vị trí và hướng lắp nôi để hỗ trợ kiểm tra an toàn theo ghế. | Dựa vào hình dáng nôi, quai và hướng đầu nôi nếu thấy được. |
| `object.type` | Box đồ vật, `seat`, `bag`, `box`, `cup` hoặc `other` | Phân biệt đồ vật với người hoặc ghế trẻ em để giảm cảnh báo nhầm về hành khách. | Phân loại theo hình dạng. Vật không rõ loại thì dùng `other`. |
| `frame_meta.camera_blocked` | `yes`, `no` ở cấp ảnh | Hỗ trợ nhận biết khi camera bị che và kết quả theo ghế có thể thiếu. | Có thể nhận biết khi vật cản che vùng quan sát. |

## Hai câu hỏi cần coach xác nhận

1. **DMS · D01.** Mô hình tìm được mặt sau khi cắt vùng đầu, nhưng trạng thái mắt trái chưa đủ rõ. Nếu đường viền các điểm mắt vẫn ước lượng được và thiếu bằng chứng về mí mắt, coach muốn đánh dấu điểm nào là occluded? Hiện giữ eye_left=unknown và đã ghi cảnh báo trong log để xác nhận trên ảnh.
2. **OMS · S02_ir.** Các mô hình chưa nhất quán về loại ghế ở rear_left. Nếu phần vỏ đủ thấy nhưng phần phân biệt hướng lắp hoặc lòng ghế bị khuất, coach muốn dùng ghi chú ca khó nào để tách child_seat và infant_seat? Tạm giữ đề xuất child_seat, occupied=unknown, và đưa vào danh sách rà.
