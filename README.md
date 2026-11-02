# Bài tập Session 15 – Ex06: Không gian cộng tác dự án Green-Tech

Họ và tên: Thi Thành Đạt  
MSSV: N26DTCN041  
Lớp: CNTT2  
Môn học: Nhập môn Công nghệ thông tin  
Email: thithanhdat111@gmail.com

## 1. Cấu trúc lưu trữ và cách làm việc

Em chọn Google Drive để lưu bản sao code và báo cáo, GitHub **riêng tư** để quản lý phiên bản code, Slack để trao đổi và giao việc. Repository công khai dùng để nộp bài này chỉ chứa bản thiết kế, không chứa code thật hoặc mật khẩu.

```text
Green-Tech (Google Drive, chỉ trưởng dự án quản lý thư mục gốc)
├── 01-SaoLuu-Code/          Bản sao thư mục sensors của từng Dev
├── 02-BaoCao-NoiBo/         Báo cáo đang soạn, chỉ người trong dự án
└── 03-ChiaSe-BenNgoai/      Bản báo cáo cho nhà đầu tư và tài liệu xin góp ý
```

Trong `01-SaoLuu-Code`, mỗi Dev có một thư mục riêng, không cùng sửa trực tiếp một bản sao. Dev dùng Google Drive for desktop để đồng bộ thư mục `sensors` của mình trong đó và giữ bản dùng được khi không có mạng trên máy. Sau khi lưu, Dev kiểm tra biểu tượng đồng bộ đã hoàn tất; khi mất mạng, file vẫn còn trên máy và sẽ được tải lên khi có mạng trở lại. Để ghép code của cả đội và xem lại các lần sửa, Dev dùng Git: tạo nhánh, commit và push lên repository GitHub riêng tư sau mỗi phần việc. **Ctrl+S chỉ lưu trên máy; không thể coi là đã sao lưu xong nếu Drive chưa đồng bộ hoặc Git chưa được push.**

File `.env` chứa mật khẩu cảm biến nằm **ngoài mọi thư mục đang đồng bộ**, chỉ ở máy của người được giao quản lý. Thêm `.env` vào `.gitignore`, không gửi qua chat, không đưa lên Drive hoặc GitHub. Có thể đưa `.env.example` chỉ gồm tên biến, không có mật khẩu, vào repo để các Dev biết cần cấu hình gì. Nếu mật khẩu từng bị đưa lên repo, phải đổi mật khẩu và xử lý bản đã lộ; thêm `.gitignore` sau đó không xóa được lịch sử cũ.

## 2. Phân quyền chia sẻ

Toàn bộ Drive để **Restricted**, mời đúng tài khoản cần dùng. Không cấp quyền Editor ở thư mục gốc cho người ngoài vì quyền của thư mục có thể áp dụng xuống tệp bên trong.

| Tài liệu / khu vực | Đội Dev | Nhà đầu tư | Đối tác thiết bị | Cách cấp quyền |
|---|---|---|---|---|
| `01-SaoLuu-Code/` và repo code riêng tư | Editor / quyền đóng góp code theo nhiệm vụ | Không truy cập | Không truy cập | Chỉ mời đội kỹ thuật; mỗi Dev sửa bản của mình |
| `02-BaoCao-NoiBo/` | Chỉ người được giao viết báo cáo mới là Editor | Không truy cập | Không truy cập | Không chia sẻ cả thư mục cho bên ngoài |
| `BaoCao_NhaDauTu.pdf` trong `03-ChiaSe-BenNgoai/` | Trưởng dự án quản lý | Viewer | Không truy cập | Mời riêng email nhà đầu tư, không dùng Anyone with the link |
| `GopY_ThietBi` trong `03-ChiaSe-BenNgoai/` | Người phụ trách tài liệu là Editor | Không truy cập | Commenter | Mời riêng email đối tác để họ nhận xét mà không sửa nội dung |
| `.env` chứa mật khẩu | Chỉ người được giao quản lý | Không truy cập | Không truy cập | Lưu cục bộ ngoài vùng đồng bộ và repo |

Hai tài liệu chia sẻ bên ngoài là **hai tệp riêng**. Em không cấp quyền cho nhà đầu tư hoặc đối tác trên cả thư mục `03-ChiaSe-BenNgoai/`, tránh việc họ nhìn thấy tệp của nhau. Khi hết việc, trưởng dự án mở **Share → Manage access** để kiểm tra và thu hồi quyền không còn cần thiết.

## 3. Kênh giao tiếp và chuyển lỗi thành Task

- `#thong-bao`: Mốc tiến độ, quyết định đã chốt và deadline; hạn chế tán gẫu.
- `#loi-cam-bien`: Mỗi lỗi có một tin nhắn nêu mã cảm biến, hiện tượng, cách tái hiện và kết quả mong đợi. Phản hồi bằng **Reply in Thread** để không làm trôi lỗi khác.
- `#dev-code`: Trao đổi cách sửa, nhánh Git và kết quả kiểm tra.
- `#trao-doi-chung`: Câu hỏi chung không thuộc một lỗi cụ thể.

Em dùng **Slack Lists** cho danh sách Task. Khi có tin báo lỗi ở `#loi-cam-bien`, mở dấu ba chấm của tin nhắn → **Add to list**; ghi tên việc cần làm, người phụ trách, hạn hoàn thành và trạng thái. Ví dụ **giả định**: “Sửa cảm biến độ ẩm không gửi dữ liệu”, giao cho Dev phụ trách cảm biến, hạn **17:00 ngày 04/11/2026**. Người sửa cập nhật tiến độ trên Task và trả lời trong thread của lỗi; khi kiểm tra xong thì đánh dấu hoàn thành. Như vậy lỗi không chỉ dừng ở một đoạn chat dễ bị trôi.

## 4. Bàn giao khi kết thúc bài tập nhóm

Trưởng dự án chọn người nhận bàn giao, chia sẻ trước từng tệp/thư mục Drive cho người đó, rồi dùng **Share → Transfer ownership**. Sau đó kiểm tra người mới đã là Owner của **từng tệp quan trọng**, vì chuyển Owner của thư mục không tự chuyển Owner của các tệp bên trong. Nếu dùng tài khoản trường/công ty, người nhận thường phải ở cùng tổ chức theo quy định của Google Drive. Với GitHub riêng tư và Slack, bàn giao quyền quản trị bằng chức năng riêng của từng dịch vụ, rồi thu hồi quyền của người không còn tham gia. Không đưa mật khẩu `.env` vào tài liệu bàn giao công khai.

## 5. Kiểm thử giả định: lỡ xóa sạch `sensors`

Đây là **quy trình giả định**, chưa phải kết quả chạy thử trên một dự án thật:

1. Báo cả nhóm tạm ngừng sửa và kiểm tra trạng thái đồng bộ. Nếu thư mục vừa bị xóa trên máy, kiểm tra **Recycle Bin**; nếu lệnh xóa đã đồng bộ lên Drive, vào **Trash** của tài khoản sở hữu, tìm `sensors` và chọn **Restore**. Không tạo ngay một thư mục mới cùng tên để tránh lẫn phiên bản.
2. Đợi Drive đồng bộ lại, mở vài file quan trọng và đối chiếu với bản code trên GitHub. Tệp trong Drive Trash thường được giữ **30 ngày** nếu chưa xóa vĩnh viễn. Nếu không còn bản trong Trash nhưng code đã được commit, dùng bản commit tốt gần nhất trên GitHub để lấy lại các file `sensors` đã được Git theo dõi. File chưa từng đồng bộ hoặc commit có thể không khôi phục được từ hai nguồn này.
3. Chạy kiểm tra cơ bản cho cảm biến, xác nhận đủ file, rồi cho nhóm tiếp tục làm việc. Ghi lại nguyên nhân xóa nhầm và kiểm tra lại quyền Editor của thư mục sao lưu.

Mô hình này có bản làm việc trên máy, bản sao trên Cloud và lịch sử sửa code trên GitHub. Việc khôi phục nhanh phụ thuộc vào bản sao hoặc commit thực sự đã hoàn tất trước lúc xóa.
