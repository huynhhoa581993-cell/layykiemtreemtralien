# ỨNG DỤNG WEB "LẤY Ý KIẾN TRẺ EM XÃ TRÀ LIÊN"
> Cơ quan quản lý: **Đoàn TNCS Hồ Chí Minh – Hội đồng Đội xã Trà Liên**

Ứng dụng web được xây dựng nhằm lắng nghe, tiếp nhận và giải quyết tâm tư, nguyện vọng và ý kiến đóng góp của trẻ em, thiếu niên nhi đồng trên địa bàn xã Trà Liên.

---

## 🌟 TÍNH NĂNG NỔI BẬT

### 1. Giao diện thiếu nhi gửi ý kiến (`/`)
* **Thân thiện & Tối ưu điện thoại:** Thiết kế nhẹ, tải cực nhanh, tông màu xanh thanh niên và trắng, nút bấm to, biểu tượng sinh động, dễ sử dụng trên smartphone.
* **Không cần đăng nhập:** Trẻ em gửi ý kiến trực tiếp, thuận tiện, không rào cản.
* **Biểu mẫu đầy đủ:** 
  - Chọn nhanh độ tuổi (hoặc tự nhập tuổi).
  - Chọn thôn/xóm trên địa bàn xã Trà Liên (Trà Liên Tây, Trà Liên Đông, Thôn 1, 2, 3, 4 hoặc tự nhập).
  - Chọn chủ đề: **Học tập, Vui chơi, Gia đình, Nhà trường, Môi trường, Bảo vệ trẻ em, Hoạt động Đoàn – Đội, Ý kiến khác**.
  - Soạn nội dung ý kiến với bộ đếm ký tự.
* **Bảo vệ thông tin & Quyền trẻ em:**
  - Mặc định chế độ **Gửi ẩn danh** tuyệt đối.
  - Cho phép tùy chọn để lại họ tên, số liên hệ nếu muốn cán bộ Đoàn phản hồi trực tiếp.
* **Thông báo thành công:** Cấp mã tiếp nhận (Ví dụ: `TL-0001`) và lời cảm ơn thân thiện từ Đoàn xã.

### 2. Trang quản trị Đoàn xã (`/admin`)
* **Đăng nhập bảo mật:** Xác thực phiên làm việc, chỉ cán bộ quản trị mới xem được dữ liệu trẻ em.
* **Bảng thống kê:** Tổng số ý kiến, Ý kiến mới tiếp nhận, Đang xử lý, Đã hoàn thành.
* **Xem, tìm kiếm & Bộ lọc nâng cao:**
  - Tìm kiếm theo từ khóa nội dung, mã số, người gửi.
  - Lọc nhanh theo từng Thôn/Xóm.
  - Lọc theo Chủ đề.
  - Lọc theo Trạng thái xử lý.
* **Cập nhật tiến độ xử lý:**
  - Chuyển trạng thái 1-chạm: *Mới tiếp nhận* ➔ *Đang xử lý* ➔ *Đã hoàn thành*.
  - Ghi chú biện pháp giải quyết hoặc phân công cán bộ Đoàn phụ trách.
* **Xuất báo cáo:**
  - **Xuất Excel (.xlsx):** Định dạng chuẩn, tự căn chỉnh độ rộng cột.
  - **Xuất CSV:** Chuẩn mã hóa UTF-8 BOM, mở trực tiếp trên Excel tiếng Việt không lỗi font.

---

## 🚀 HƯỚNG DẪN KHỞI CHẠY VÀ SỬ DỤNG

### Bước 1: Khởi động máy chủ
Mở cửa sổ dòng lệnh tại thư mục dự án và chạy lệnh:
```bash
npm start
```

Máy chủ sẽ chạy tại địa chỉ:
* **Giao diện thiếu nhi:** [http://localhost:3000](http://localhost:3000)
* **Trang quản trị Đoàn xã:** [http://localhost:3000/admin](http://localhost:3000/admin)

### Bước 2: Đăng nhập quản trị
* **Tài khoản mặc định:** `admin`
* **Mật khẩu mặc định:** `doanxatralien@2026`

*(Có thể thay đổi trong tệp cấu hình `.env`)*

---

## 📁 CẤU TRÚC DỰ ÁN

```text
vidu/
├── package.json          # Danh sách gói phụ thuộc và scripts
├── .env                  # Cấu hình biến môi trường và tài khoản admin
├── server.js             # Máy chủ Express: API tiếp nhận, xác thực, quản lý và xuất file
├── db.js                 # Cơ sở dữ liệu tệp lưu trữ bền vững (Atomic Persistence)
├── test_app.js           # Bộ kịch bản kiểm thử tự động toàn diện
├── data/
│   └── feedbacks.json    # Cơ sở dữ liệu thực tế lưu trữ ý kiến của trẻ em
└── public/
    ├── index.html        # Giao diện thiếu nhi gửi ý kiến
    ├── admin.html        # Trang quản trị của Đoàn xã
    ├── css/
    │   ├── style.css     # Giao diện thiếu nhi (xanh thanh niên, responsive di động)
    │   └── admin.css     # Giao diện bảng điều khiển quản trị
    ├── js/
    │   ├── app.js        # Logic gửi ý kiến thiếu nhi, xác thực form
    │   └── admin.js      # Logic quản trị: đăng nhập, thống kê, lọc, cập nhật, xuất file
    └── images/
        └── logo-doan.svg # Biểu trưng Đoàn TNCS Hồ Chí Minh
```

---

## 🔒 BẢO MẬT & BẢO VỆ DỮ LIỆU TRẺ EM
1. API công khai (`/api/feedback`) chỉ tiếp nhận ý kiến, **tuyệt đối không để lộ** danh sách ý kiến ra ngoài.
2. Dữ liệu quản trị được bảo vệ bởi middleware xác thực Bearer token 24 giờ.
3. Người dùng chưa đăng nhập khi truy cập API quản lý sẽ nhận mã lỗi `401 Unauthorized`.
4. Dữ liệu được lưu trữ tự động và an toàn tại `data/feedbacks.json`, có thể dễ dàng sao lưu hoặc đồng bộ lên dịch vụ đám mây (Cloud/Supabase).
