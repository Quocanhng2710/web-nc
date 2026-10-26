# TIGER SHOP — HỆ THỐNG THƯƠNG MẠI ĐIỆN TỬ TÍCH HỢP AI

Tiger Shop là hệ thống website thương mại điện tử hỗ trợ bán hàng trực tuyến, quản lý sản phẩm, đơn hàng, khách hàng, nhân sự và chăm sóc khách hàng thông qua Chatbot AI và hệ thống trò chuyện thời gian thực.

Dự án được phát triển với ReactJS, Node.js, ExpressJS và MySQL.

## 1. Công nghệ sử dụng

| Thành phần | Công nghệ |
|---|---|
| Frontend | ReactJS, HTML, CSS, Bootstrap |
| Backend | Node.js, ExpressJS |
| Database | MySQL |
| Xác thực | JWT, bcrypt |
| Chat thời gian thực | Socket.IO |
| AI Chatbot | Google Generative AI (Gemini) |
| Giao tiếp | REST API, WebSocket |
| Quản lý mã nguồn | Git, GitHub |

## 2. Cấu trúc dự án

```text
Tiger-Shop/
├── backend/
│   ├── config/          # Cấu hình hệ thống và database
│   ├── controllers/     # Xử lý request
│   ├── middlewares/     # Xác thực, phân quyền
│   ├── models/          # Xử lý dữ liệu
│   ├── routes/          # Định nghĩa API
│   ├── services/        # Xử lý nghiệp vụ
│   ├── utils/           # Tiện ích
│   ├── server.js        # Khởi động backend
│   └── package.json
├── frontend/
│   ├── public/
│   ├── src/
│   ├── package.json
│   └── package-lock.json
├── database/
│   ├── ecommerce.sql
│   └── migrations/
├── package.json
└── README.md
```

## 3. Yêu cầu trước khi cài đặt

Máy tính cần có:

- Windows 10/11.
- Node.js và npm.
- MySQL Server hoặc Laragon/XAMPP có MySQL.
- Visual Studio Code (khuyến nghị).
- Git (nếu tải mã nguồn bằng lệnh clone).
- Trình duyệt Chrome hoặc Edge.
- Kết nối Internet để tải thư viện.

Phiên bản Node.js 22.20.0 đã được sử dụng trong quá trình kiểm tra mã nguồn. Phiên bản Node.js tối thiểu chưa được xác minh.

Kiểm tra Node.js và npm:

```powershell
node -v
npm -v
```

## 4. Tải mã nguồn

Truy cập:

https://github.com/Quocanhng2710/web-nc

Chọn **Code → Download ZIP**, sau đó giải nén vào thư mục mong muốn.

Hoặc sử dụng Git:

```powershell
git clone https://github.com/Quocanhng2710/web-nc.git
cd web-nc
```

Mở thư mục dự án bằng Visual Studio Code.

## 5. Cài đặt cơ sở dữ liệu MySQL

### Bước 1: Khởi động MySQL

Nếu sử dụng Laragon:

1. Mở Laragon.
2. Chọn Start All.
3. Kiểm tra MySQL đã hoạt động.
4. Mở phpMyAdmin hoặc công cụ quản trị MySQL.

### Bước 2: Tạo database

Chạy lệnh:

```sql
CREATE DATABASE IF NOT EXISTS ecommerce
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_ci;
```

### Bước 3: Import cơ sở dữ liệu

Trong phpMyAdmin:

1. Chọn database `ecommerce`.
2. Chọn tab Import.
3. Chọn file `database/ecommerce.sql`.
4. Nhấn Import/Go.
5. Kiểm tra các bảng đã được tạo.

Dự án có các migration SQL từ `001` đến `014` trong `database/migrations/`.

**Lưu ý:** Không tự động chạy toàn bộ migration khi chưa kiểm tra trạng thái database. Một số migration có thể thay đổi cấu trúc hoặc dữ liệu hiện có.

Để sử dụng đầy đủ các chức năng, có thể cần thêm dữ liệu mẫu và cấu trúc được cập nhật sau schema gốc.

### Bước 4: Cấu hình kết nối

Mở:

```text
backend/config/db.js
```

Cấu hình kết nối đang được khai báo trực tiếp bằng các thông số như:

- Host: `localhost`
- Username: `root`
- Database: `ecommerce`
- Password: theo cấu hình MySQL trên máy cài đặt.

**Quan trọng:** File `db.js` hiện chưa đọc đầy đủ cấu hình database từ biến môi trường. Nếu MySQL trên máy sử dụng tài khoản hoặc mật khẩu khác, cần cập nhật cấu hình kết nối tương ứng trước khi chạy.

Không đưa mật khẩu database thật lên GitHub.

## 6. Cài đặt Backend

Mở Terminal trong VS Code:

```powershell
cd backend
npm install
```

Lệnh này tự động cài đặt các thư viện được khai báo trong `backend/package.json`.

### Tạo file môi trường

Tạo file:

```text
backend/.env
```

Nội dung tham khảo:

```dotenv
PORT=5000
JWT_SECRET=THAY_BANG_CHUOI_BI_MAT_DU_MẠNH

GEMINI_API_KEY=
GEMINI_API_KEY_SALE=
GEMINI_API_KEY_RETURN=
GEMINI_API_KEY_VOUCHER=
```

Các API key Gemini cần được cung cấp hợp lệ nếu sử dụng các chức năng AI tương ứng.

Không chia sẻ hoặc commit file `.env` chứa khóa thật.

### Chạy Backend

```powershell
node server.js
```

Khi khởi động thành công, terminal sẽ hiển thị thông báo tương tự:

```text
Backend running on http://localhost:5000
```

Giữ nguyên cửa sổ Terminal này để backend tiếp tục hoạt động.

## 7. Cài đặt Frontend

Mở Terminal mới trong VS Code.

Từ thư mục gốc của dự án:

```powershell
cd frontend
npm install
```

Sau khi cài đặt xong, chạy:

```powershell
npm start
```

Ứng dụng React sẽ khởi động tại:

http://localhost:3000

Lưu ý: Backend phải đang chạy trên cổng `5000` để các chức năng gọi API hoạt động đúng theo cấu hình hiện tại.

## 8. Hướng dẫn sử dụng

### 8.1. Khách hàng (Customer)

Trang đăng ký:

http://localhost:3000/register

Trang đăng nhập:

http://localhost:3000/login

Sau khi đăng nhập thành công, người dùng được điều hướng đến `/home`.

Các chức năng chính:

- Xem danh sách sản phẩm.
- Tìm kiếm và lọc sản phẩm.
- Xem thông tin chi tiết sản phẩm.
- Thêm sản phẩm vào giỏ hàng.
- Đặt hàng và lựa chọn phương thức thanh toán.
- Áp dụng mã voucher.
- Xem và theo dõi đơn hàng.
- Gửi yêu cầu đổi trả hoặc bảo hành.
- Nhận thông báo.
- Chat với nhân viên hoặc Chatbot AI.
- Cập nhật thông tin cá nhân.

### 8.2. Quản trị viên (Admin)

Sau khi đăng nhập, tài khoản Admin được điều hướng tới:

http://localhost:3000/admin/dashboard

Các chức năng chính:

- Xem tổng quan hệ thống.
- Quản lý tài khoản người dùng.
- Phân quyền tài khoản.
- Quản lý trạng thái người dùng.
- Xem lịch sử hoạt động và nhật ký hệ thống.
- Thực hiện các nghiệp vụ quản trị được phân quyền.

### 8.3. Quản lý (Manager)

Sau khi đăng nhập, tài khoản Manager được điều hướng tới:

http://localhost:3000/manager/workspace

Các chức năng chính:

- Quản lý sản phẩm và kho hàng.
- Theo dõi đơn hàng.
- Quản lý nhân viên.
- Quản lý lịch làm việc.
- Theo dõi chấm công.
- Xem bảng lương nhân viên.
- Quản lý voucher.
- Xem báo cáo thống kê.
- Xử lý các yêu cầu nhân sự theo quyền được cấp.

### 8.4. Nhân viên (Staff)

Sau khi đăng nhập, tài khoản Staff được điều hướng tới:

http://localhost:3000/staff/workspace

Các chức năng chính:

- Xem tổng quan công việc.
- Chấm công vào/ra ca.
- Đăng ký lịch làm việc.
- Xử lý đơn hàng.
- Chat và hỗ trợ khách hàng.
- Xem bảng lương và hoa hồng.
- Gửi yêu cầu nghỉ phép hoặc đi muộn.

## 9. Thiết lập tài khoản Admin, Manager và Staff

Hệ thống có các vai trò:

| Vai trò | Quyền sử dụng |
|---|---|
| ADMIN | Quản trị hệ thống |
| MANAGER | Quản lý cửa hàng và nhân sự |
| STAFF | Thực hiện nghiệp vụ nhân viên |
| CUSTOMER | Mua sắm và quản lý đơn hàng cá nhân |

**Chú ý:** Quy trình tạo tài khoản Admin đầu tiên và dữ liệu tài khoản mặc định hiện chưa được xác minh đầy đủ.

Source cũng có điểm cần kiểm tra giữa dữ liệu role trong schema gốc, migration và chức năng đăng ký khách hàng.

Do đó, trước khi sử dụng, cần kiểm tra database thực tế và đảm bảo tài khoản được gán đúng vai trò.

Không có mật khẩu mẫu được công bố trong tài liệu này. Người triển khai cần thiết lập tài khoản hợp lệ và bàn giao thông tin đăng nhập riêng qua kênh an toàn.

## 10. Các chức năng nổi bật

### Quản lý bán hàng

Hỗ trợ danh mục, sản phẩm, biến thể, giỏ hàng, đơn hàng, voucher và quản lý trạng thái xử lý đơn.

### Hệ thống Chatbot AI

Tích hợp các chức năng hỗ trợ tư vấn khách hàng thông qua Google Generative AI. Những chức năng này phụ thuộc vào API key và cấu hình tương ứng.

### Chat thời gian thực

Sử dụng Socket.IO để trao đổi dữ liệu giữa khách hàng và nhân viên mà không cần tải lại trang.

### Quản lý nhân sự

Hỗ trợ ca làm, chấm công, quản lý yêu cầu nhân sự, lương và hoa hồng.

### Quản trị và thống kê

Cung cấp giao diện theo dõi hoạt động quản lý, doanh thu, tài khoản và các nghiệp vụ nội bộ.

## 11. Các lỗi thường gặp

| Lỗi | Hướng xử lý |
|---|---|
| `npm is not recognized` | Cài đặt Node.js và mở lại Terminal |
| `Cannot find module` | Chạy `npm install` đúng thư mục |
| Backend không kết nối MySQL | Kiểm tra MySQL và `backend/config/db.js` |
| Port 5000 bị chiếm | Giải phóng cổng hoặc điều chỉnh cấu hình đồng bộ |
| Port 3000 bị chiếm | Kiểm tra tiến trình sử dụng cổng |
| Frontend không gọi được API | Kiểm tra backend, proxy và địa chỉ API |
| Không đăng nhập được | Kiểm tra JWT secret, database và role |
| Chat không hoạt động | Kiểm tra Socket.IO và kết nối backend |
| AI không phản hồi | Kiểm tra Gemini API key, quota và cấu hình |
| Import SQL thất bại | Kiểm tra cấu trúc bảng, migration và lỗi SQL cụ thể |

## 12. Kiểm tra sau cài đặt

Sau khi hoàn thành, cần thử nghiệm các thao tác:

- [ ] Backend khởi động thành công.
- [ ] Frontend truy cập được tại localhost:3000.
- [ ] Backend kết nối database thành công.
- [ ] Hiển thị được sản phẩm.
- [ ] Đăng ký và đăng nhập Customer thành công.
- [ ] Đăng nhập Admin thành công.
- [ ] Đăng nhập Manager thành công.
- [ ] Đăng nhập Staff thành công.
- [ ] Đặt và xử lý đơn hàng.
- [ ] Chat giữa nhân viên và khách hàng.
- [ ] Kiểm tra chức năng AI nếu đã cấu hình API key.
- [ ] Kiểm tra phân quyền giữa các vai trò.

## 13. Lưu ý bảo mật và triển khai

- Đây là hướng dẫn chạy ứng dụng trong môi trường localhost.
- Không sử dụng trực tiếp cấu hình phát triển để triển khai production.
- Không công khai `.env`, mật khẩu database hoặc API key.
- Đổi mật khẩu các tài khoản thử nghiệm trước khi đưa vào sử dụng thực tế.
- Sao lưu database trước khi thực hiện migration.
- Kiểm tra quyền truy cập API ở backend.
- Đảm bảo dữ liệu nhạy cảm không bị gửi hoặc lưu trữ không cần thiết.

## 14. Khởi động lại hệ thống trong những lần sử dụng sau

Sau lần cài đặt đầu tiên, thông thường không cần chạy lại `npm install` nếu dependencies không thay đổi.

Mỗi lần sử dụng:

**Bước 1:** Khởi động MySQL.

**Bước 2:** Mở Terminal backend:

```powershell
cd backend
node server.js
```

**Bước 3:** Mở Terminal thứ hai tại thư mục gốc dự án:

```powershell
cd frontend
npm start
```

**Bước 4:** Truy cập:

http://localhost:3000

Để dừng server, nhấn `Ctrl + C` trong Terminal tương ứng.

---

**Tiger Shop — Hệ thống thương mại điện tử tích hợp Chatbot AI**

*Tài liệu hướng dẫn cài đặt và sử dụng trên môi trường localhost. Một số quy trình thiết lập database và tài khoản quản trị cần được xác minh trên môi trường triển khai thực tế.*
