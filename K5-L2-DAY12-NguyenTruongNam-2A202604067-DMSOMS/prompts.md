# Khai báo dùng AI — Nguyễn Trường Nam · 2A202604067

| # | Công cụ | Nội dung trao đổi | Cách dùng | Đối chiếu |
| ---: | --- | --- | --- | --- |
| 1 | Trợ lý AI của OpenAI | Tóm tắt đề DMS/OMS, gợi ý cách hiểu nhãn và câu chữ cho danh sách lớp, chuẩn bị lệnh PowerShell chạy checker trên Windows. | Dùng bản hướng dẫn chạy tại máy và kiểm lại nội dung danh sách lớp theo Guideline Cabin v1.0. | Đối chiếu với `GUIDE.md`, `CHECKPOINTS.md` và `cabin_check.py` trong repo. |
| 2 | Trợ lý AI của OpenAI | Giải thích vì sao dùng NIR, cách tính thời gian từ số khung hình và sự khác nhau giữa ảnh cabin với ảnh ngoài xe. | Dùng để tự đối chiếu các khái niệm trong exit ticket. | Kiểm phép tính theo số khung được nêu và phần mô tả hai bộ ảnh trong `GUIDE.md`. |
| 3 | Mô hình cục bộ YOLO, YOLOE, CLIP và MediaPipe | Tạo đề xuất box, phân loại vùng ghế và định vị mặt, tay, điểm mặt cho bộ G09. | Nhập các đề xuất vào task CVAT #23. Các ca mô hình bất đồng được ghi trong phiếu tự kiểm. | Xuất lại ZIP từ CVAT và kiểm bằng checker trên 22 ảnh. |

Ảnh được xử lý tại máy. Nhật ký mô tả phần kiểm với mô hình và checker. Không thực hiện review chéo trong hồ sơ này.
