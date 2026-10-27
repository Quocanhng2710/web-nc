# TIGER SHOP — Hệ thống thương mại điện tử tích hợp Chatbot AI

> Website bán hàng đa ngành, quản lý đơn hàng, sản phẩm, nhân sự và chăm sóc khách hàng bằng trò chuyện trực tuyến và trợ lý AI.

**Công nghệ:** ReactJS (Create React App) · Node.js · ExpressJS · MySQL · JWT · Socket.IO · Gemini API.

**Mã nguồn:** https://github.com/Quocanhng2710/web-nc

## Mục lục

- [Giới thiệu và hình ảnh](#1-giới-thiệu-và-hình-ảnh)
- [Các chức năng theo vai trò](#2-các-chức-năng-theo-vai-trò)
- [Yêu cầu cài đặt](#3-yêu-cầu-cài-đặt)
- [Tải và cài đặt dự án](#4-tải-và-cài-đặt-dự-án)
- [Cấu hình cơ sở dữ liệu](#5-cấu-hình-cơ-sở-dữ-liệu)
- [Cấu hình Backend](#6-cấu-hình-backend)
- [Khởi động website](#7-khởi-động-website)
- [Đăng nhập và sử dụng](#8-đăng-nhập-và-sử-dụng)
- [Lỗi thường gặp](#9-lỗi-thường-gặp)
- [Lưu ý bàn giao](#10-lưu-ý-bàn-giao)

## 1. Giới thiệu và hình ảnh

Các ảnh dưới đây được trích từ **Chương 5 – Cài đặt và kết quả thử nghiệm** của báo cáo dự án. Ảnh có tính chất minh họa giao diện tại thời điểm chụp; giao diện thực tế có thể thay đổi theo phiên bản source.

### Giao diện dành cho khách hàng

**Trang chủ**

![Trang chủ Tiger Shop](docs/images/trang-chu.jpg)

**Danh sách, tìm kiếm và lọc sản phẩm**

![Danh sách sản phẩm](docs/images/danh-sach-san-pham.jpg)

**Thông tin chi tiết sản phẩm**

![Chi tiết sản phẩm](docs/images/chi-tiet-san-pham.jpg)

**Giỏ hàng**

![Giỏ hàng](docs/images/gio-hang.jpg)

**Thanh toán**

![Thanh toán](docs/images/thanh-toan.jpg)

**Trợ lý AI tư vấn**

![Chatbot AI](docs/images/chatbot-ai.jpg)

**Chat trực tuyến**

![Chat khách hàng](docs/images/chat-khach-hang.jpg)

### Giao diện Admin

**Tổng quan quản trị**

![Dashboard Admin](docs/images/admin-dashboard.jpg)

**Báo cáo doanh thu**

![Doanh thu](docs/images/admin-doanh-thu.jpg)

**Quản lý tài khoản người dùng**

![Người dùng](docs/images/admin-nguoi-dung.jpg)

**Nhật ký hệ thống**

![Nhật ký hệ thống](docs/images/admin-nhat-ky.jpg)

### Giao diện Manager

**Tổng quan quản lý**

![Dashboard Manager](docs/images/manager-dashboard.jpg)

**Quản lý sản phẩm / kho**

![Quản lý sản phẩm](docs/images/manager-san-pham.jpg)

**Quản lý nhân sự**

![Quản lý nhân sự](docs/images/manager-nhan-su.jpg)

**Quản lý voucher**

![Voucher](docs/images/manager-voucher.jpg)

### Giao diện Staff

**Chấm công**

![Chấm công nhân viên](docs/images/staff-cham-cong.jpg)

**Tổng quan công việc**

![Tổng quan nhân viên](docs/images/staff-tong-quan.jpg)

**Xử lý đơn hàng**

![Xử lý đơn hàng](docs/images/staff-don-hang.jpg)

**Chat với khách hàng**

![Nhân viên chat](docs/images/staff-chat.jpg)

## 2. Các chức năng theo vai trò

| Vai trò | Nhóm chức năng theo báo cáo |
|---|---|
| **Customer** | Đăng ký/đăng nhập; tìm kiếm, xem sản phẩm; giỏ hàng; đặt và theo dõi đơn; voucher; chat AI và nhân viên; yêu cầu đổi/trả |
| **Admin** | Quản trị người dùng và phân quyền; kiểm tra nhật ký; theo dõi báo cáo quản trị |
| **Manager** | Quản lý sản phẩm/kho; nhân sự; ca làm, lương; voucher; thống kê và yêu cầu đổi/trả |
| **Staff** | Chấm công, đăng ký ca; xem lương; xử lý đơn hàng; tư vấn khách hàng qua chat |

> Danh sách dựa trên tài liệu phân tích và ảnh báo cáo. Cần kiểm thử trên database của máy cài đặt để xác nhận hoạt động end-to-end của từng chức năng.

## 3. Yêu cầu cài đặt

- Windows 10 hoặc 11.
- Node.js và npm (Node v22.20.0 từng được dùng để kiểm tra source; **phiên bản tối thiểu chưa xác minh**).
- MySQL / MariaDB (có thể cài qua Laragon hoặc dùng MySQL Server riêng).
- VS Code hoặc Terminal PowerShell.
- Kết nối Internet để tải thư viện npm.

Kiểm tra môi trường:

```powershell
node -v
npm -v
```

## 4. Tải và cài đặt dự án

**Tải ZIP:** tại trang repository chọn **Code → Download ZIP**, giải nén, mở thư mục `web-nc`.

**Hoặc clone bằng Git:**

```powershell
git clone https://github.com/Quocanhng2710/web-nc.git
cd web-nc
```

Cấu trúc cần có:

```text
web-nc/
├── backend/       # Express API, Socket.IO
├── frontend/      # React UI
├── database/      # ecommerce.sql, migrations
├── docs/images/   # Hình ảnh giao diện trong README
└── README.md
```

Không cần copy `node_modules` từ máy phát triển. Mỗi máy cần tự cài dependencies qua `npm install`.

## 5. Cấu hình cơ sở dữ liệu

1. Mở Laragon và khởi động **MySQL**, hoặc khởi động dịch vụ MySQL trên máy.
2. Mở phpMyAdmin/MySQL Workbench và tạo database:

```sql
CREATE DATABASE IF NOT EXISTS ecommerce
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;
```

3. Import file `database/ecommerce.sql` vào database `ecommerce`.
4. Kiểm tra cấu trúc và dữ liệu của các bảng trước khi chạy ứng dụng.
5. Kiểm tra `backend/config/db.js`: trong source được audit, cấu hình kết nối MySQL viết trực tiếp trong file (host `localhost`, user `root`, database `ecommerce`, mật khẩu rỗng). **Phải chỉnh đúng theo máy cài đặt**, không giả định tất cả máy có tài khoản root không mật khẩu.

**Quan trọng:** Thư mục `database/migrations/` có nhiều file SQL, nhưng chưa có bằng chứng về một trình chạy migration tự động. Không chạy tất cả script trên database có dữ liệu khi chưa sao lưu và kiểm tra vì một số script thay đổi cấu trúc/dữ liệu. Nếu cần các chức năng mới, phải xác minh migration nào đã nằm trong `ecommerce.sql` và migration nào còn thiếu.

## 6. Cấu hình Backend

Mở Terminal trong thư mục gốc dự án:

```powershell
cd backend
npm install
```

Tạo file `backend/.env` nếu chưa tồn tại, ví dụ:

```dotenv
PORT=5000
JWT_SECRET=THAY_BANG_CHUOI_BI_MAT_DAI_NGAU_NHIEN
GEMINI_API_KEY=
GEMINI_API_KEY_SALE=
GEMINI_API_KEY_RETURN=
GEMINI_API_KEY_VOUCHER=
```

- `JWT_SECRET` cần giá trị bí mật mạnh để hỗ trợ xác thực.
- Các key Gemini dùng cho tính năng AI tương ứng; không có key có thể khiến chức năng AI không dùng được.
- **Không đăng `.env` hay key thật lên GitHub.**
- Database vẫn cần cấu hình qua `backend/config/db.js` nếu source chưa được chỉnh để đọc `DB_*` từ `.env`.

Chạy backend:

```powershell
node server.js
```

Kết quả mong đợi: backend lắng nghe tại `http://localhost:5000`. Giữ Terminal mở.

## 7. Khởi động website

Mở **Terminal PowerShell thứ hai** từ thư mục gốc `web-nc`:

```powershell
cd frontend
npm install
npm start
```

Truy cập website: **http://localhost:3000**.

- Frontend là ứng dụng Create React App, khai báo proxy backend tới `http://localhost:5000`.
- Một số component dùng URL API trực tiếp, nên **backend cần chạy đúng cổng 5000** nếu chưa sửa đồng bộ các địa chỉ API.
- Mỗi lần khởi động lại máy: bật MySQL → `node server.js` trong `backend` → `npm start` trong `frontend`.
- Dừng server bằng `Ctrl + C` trong Terminal tương ứng.

## 8. Đăng nhập và sử dụng

Trang đăng nhập chung: **http://localhost:3000/login**. Đăng ký khách hàng: **http://localhost:3000/register**.

| Vai trò | Đường dẫn sau đăng nhập |
|---|---|
| Customer | `/home` |
| Admin | `/admin/dashboard` |
| Manager | `/manager/workspace` |
| Staff | `/staff/workspace` |

**Thiết lập tài khoản ban đầu:** Dự án chưa xác minh được quy trình khởi tạo Admin đầu tiên và mật khẩu mặc định an toàn. Có mâu thuẫn cần kiểm tra giữa role ID trong schema, migration và controller đăng ký. Người triển khai phải xác minh dữ liệu bảng `roles`, cách cấp quyền và tạo tài khoản hợp lệ trước khi đưa cho người sử dụng. Không công bố mật khẩu thật trong README.

## 9. Lỗi thường gặp

| Triệu chứng | Cách kiểm tra |
|---|---|
| `npm` không nhận diện | Cài Node.js rồi mở Terminal mới |
| `Cannot find module` | Chạy `npm install` trong đúng `backend` hoặc `frontend` |
| Không kết nối MySQL | MySQL đã bật chưa? Database `ecommerce` có tồn tại? Thông số trong `backend/config/db.js` có đúng? |
| Không đăng nhập được | Kiểm tra database, `JWT_SECRET`, role ID và tài khoản khởi tạo |
| Frontend không gọi được API | Kiểm tra backend cổng 5000 và proxy/API URL |
| Socket.IO lỗi | Kiểm tra backend và URL kết nối WebSocket |
| AI không phản hồi | Kiểm tra key Gemini, quyền truy cập/quota và log backend |
| SQL báo trùng bảng/cột | Không chạy lại migration khi chưa kiểm tra phiên bản schema và sao lưu |

## 10. Lưu ý bàn giao

- Đây là hướng dẫn chạy **local**, chưa phải hướng dẫn triển khai production.
- Source code và schema SQL **không nhất thiết bao gồm dữ liệu thực tế** (sản phẩm, tài khoản demo, đơn hàng). Nếu muốn khách xem đúng nội dung demo, cần bàn giao bản dữ liệu mẫu đã được kiểm tra và loại bỏ dữ liệu nhạy cảm.
- Không công khai `.env`, password, JWT secret, API key, thông tin khách hàng hoặc tài khoản thực.
- Chưa thể xác nhận toàn bộ tính năng chạy được trên máy sạch nếu chưa nghiệm thu việc import database, đồng bộ role và tạo Admin đầu tiên.
- Các ảnh được trích từ báo cáo để minh họa, không phải kết quả kiểm thử runtime hiện tại.

---

**Tiger Shop — Website thương mại điện tử tích hợp Chatbot AI**
