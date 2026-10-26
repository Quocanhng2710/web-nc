# Tiger Shop — Hướng dẫn cài đặt và sử dụng trên máy cá nhân

> Tài liệu dành cho khách nhận source code. Căn cứ: báo cáo audit từ mã nguồn do bên phát triển cung cấp. Các bước import migration, tạo tài khoản quản trị và kiểm thử end-to-end chưa được xác minh trên máy sạch.

## 1. Chuẩn bị

- Máy Windows, Git (hoặc tải ZIP trên GitHub), Node.js và npm, MySQL/MariaDB (có thể dùng Laragon hoặc XAMPP), trình duyệt, VS Code tùy chọn.
- Node.js v22.20.0 đã xuất hiện trong môi trường audit; dự án **chưa khai báo phiên bản Node tối thiểu**.
- Cần quyền truy cập các tệp cấu hình cục bộ và file SQL được phép bàn giao. Không chia sẻ khóa bí mật trong repo công khai.

## 2. Lấy mã nguồn

Truy cập <https://github.com/Quocanhng2710/web-nc> → **Code → Download ZIP** và giải nén, hoặc trong PowerShell:

```powershell
git clone https://github.com/Quocanhng2710/web-nc.git
cd web-nc
```

## 3. Chuẩn bị MySQL

1. Bật dịch vụ MySQL trong Laragon/XAMPP hoặc MySQL Server.
2. Mở phpMyAdmin / MySQL Workbench; kiểm tra port, user và mật khẩu thực tế.
3. Xem nội dung `database/ecommerce.sql` trước khi chạy. Nếu script chưa tự tạo database, có thể tạo cơ sở dữ liệu trước:

```sql
CREATE DATABASE IF NOT EXISTS ecommerce
CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

4. Import `database/ecommerce.sql` **vào database mới/trống** sau khi đã kiểm tra nội dung; sao lưu trước khi chạy trên database đang có dữ liệu.
5. Thư mục `database/migrations/` chứa các tệp `001`–`014` nhưng **chưa có migration runner và thứ tự áp dụng thực tế được nghiệm thu**. Không chạy hàng loạt khi chưa xác minh các lệnh `ALTER`, `UPDATE`, `DELETE`, `INSERT`, quan hệ phụ thuộc và tình trạng dữ liệu.
6. Mâu thuẫn dữ liệu vai trò: mã đăng ký gán Customer `role_id = 5` nhưng một migration cung cấp các ID 1–4. Cần kiểm tra/đồng bộ ở database trước khi nghiệm thu chức năng tài khoản.

## 4. Cấu hình backend

Vào `backend/config/db.js`: phiên bản được audit **đang hard-code** `localhost`, `root`, mật khẩu rỗng và database `ecommerce`. Phải đối chiếu/cấu hình lại an toàn cho MySQL trên máy khách; các biến `DB_*` trong `.env` **chưa được file này sử dụng**.

Tạo `backend/.env` ở máy khách (không commit):

```dotenv
PORT=5000
JWT_SECRET=THAY_BANG_CHUOI_NGAU_NHIEN_DU_DAI
# Chỉ cấu hình nếu dùng các tính năng AI tương ứng
GEMINI_API_KEY=
GEMINI_API_KEY_SALE=
GEMINI_API_KEY_RETURN=
GEMINI_API_KEY_VOUCHER=
```

Không sử dụng ví dụ `JWT_SECRET` như khóa thật; dùng giá trị mạnh riêng của khách.

Mở Terminal 1 trong thư mục dự án:

```powershell
cd backend
npm install
node server.js
```

**Lưu ý:** audit cho thấy `backend/package.json` không có `npm start`; dùng `node server.js`. Nếu khởi động thành công, server thông báo URL `http://localhost:5000`. Giữ terminal này mở.

## 5. Cài frontend và chạy website

Mở **Terminal thứ hai**, trở về thư mục gốc của dự án và chạy:

```powershell
cd frontend
npm install
npm start
```

Truy cập <http://localhost:3000>. Frontend dùng Create React App (`react-scripts`) và có proxy đến `http://localhost:5000`, đồng thời một số component gọi trực tiếp URL này. Nếu bạn đổi cổng backend thì phải kiểm tra và cập nhật các URL frontend phù hợp.

Có thể build frontend để thử:

```powershell
cd frontend
npm run build
```

## 6. Đăng nhập và cách sử dụng

- Trang đăng nhập: <http://localhost:3000/login>
- Đăng ký khách hàng: <http://localhost:3000/register>
- Customer → `/home`: xem/tìm sản phẩm, giỏ hàng, đặt hàng, mã giảm giá, theo dõi đơn, chat.
- Admin → `/admin/dashboard`: quản lý tài khoản/phân quyền, xem nhật ký hệ thống.
- Manager → `/manager/workspace`: quản lý kho/sản phẩm, nhân viên, ca làm, lương, đơn và voucher.
- Staff → `/staff/workspace`: tiếp nhận và xử lý đơn, chấm công, ca làm, chat khách.

**Tài khoản quản trị đầu tiên và tài khoản Staff/Manager mẫu: CHƯA XÁC MINH.** Nhà phát triển cần cung cấp quy trình khởi tạo an toàn và kiểm tra role thực tế. Tuyệt đối không đăng mật khẩu demo hoặc mật khẩu của khách lên GitHub công khai.

## 7. Kiểm tra nghiệm thu sau cài đặt

- [ ] MySQL khởi động và database đúng schema
- [ ] Backend khởi động được tại cổng 5000
- [ ] Frontend truy cập được tại cổng 3000
- [ ] Đăng ký Customer, đăng nhập/đăng xuất và phân quyền đúng
- [ ] Tạo/đăng nhập Admin, Manager, Staff bằng cơ chế đã được xác minh
- [ ] Thử xem sản phẩm, thêm giỏ, đặt đơn và xử lý đơn
- [ ] Thử Socket.IO/chat và AI nếu đã cung cấp API key
- [ ] Không lộ `.env`, mật khẩu, dữ liệu khách hàng trên repository công khai

## 8. Khắc phục lỗi phổ biến

| Hiện tượng | Kiểm tra |
|---|---|
| Backend không chạy | Đã `npm install` trong `backend/`? `node server.js` có log lỗi nào? |
| Không kết nối MySQL | Dịch vụ MySQL, host/port, tài khoản, mật khẩu, database và cấu hình hard-code `db.js` |
| Lỗi JWT | `backend/.env` có `JWT_SECRET` hợp lệ? |
| Frontend không gọi được API | Backend cổng 5000, proxy `frontend/package.json`, URL hard-code, CORS |
| Lỗi role/không đăng nhập | Đối chiếu `roles` thực tế, migration 003 và `role_id` khi đăng ký |
| Lỗi SQL khi import | Kiểm tra bảng/cột đã tồn tại; không chạy lại migration mù quáng |
| AI không phản hồi | Cấu hình API key Gemini phù hợp, kết nối Internet, log backend |

## 9. Bàn giao dữ liệu và giới hạn localhost

Nếu cần dữ liệu demo có sẵn, xuất SQL từ database được phép bàn giao **sau khi ẩn danh và loại bỏ dữ liệu riêng tư/khóa bí mật**. Không tự động import cả dump đầy đủ lẫn chạy lại tất cả migration. `localhost` chỉ sử dụng được trên máy đang chạy; muốn công khai Internet cần triển khai riêng.

## 10. Tình trạng xác minh

Phần hướng dẫn dựa trên kết quả kiểm tra file và nhật ký chạy backend do bên phát triển cung cấp. Chưa có bằng chứng thử nghiệm trọn vẹn trên một máy khách mới cài Windows và database trống. Các bước chưa xác minh phải được kiểm tra trước khi coi là nghiệm thu hoàn tất.
