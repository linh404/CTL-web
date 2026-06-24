# 🛍️ CTL Store - Ứng Dụng Thương Mại Điện Tử Thời Trang

**CTL Web** là một ứng dụng thương mại điện tử (e-commerce) mã nguồn mở được xây dựng bằng **PHP thuần**, kết hợp với **MySQL**, **Bootstrap 5** và **JavaScript**. Ứng dụng cung cấp nền tảng mua sắm thời trang trực tuyến với đầy đủ chức năng từ duyệt sản phẩm, quản lý giỏ hàng, thanh toán đến hệ thống quản trị (Admin Dashboard).

> 🌐 **Demo:** [https://ctl-store.kesug.com](https://ctl-store.kesug.com)

---

## 📋 Mục Lục

- [Tổng Quan](#-tổng-quan)
- [Tính Năng Chính](#-tính-năng-chính)
- [Cấu Trúc Dự Án](#-cấu-trúc-dự-án)
- [Công Nghệ Sử Dụng](#-công-nghệ-sử-dụng)
- [Cơ Sở Dữ Liệu](#-cơ-sở-dữ-liệu)
- [Hướng Dẫn Cài Đặt](#-hướng-dẫn-cài-đặt)
- [Hướng Dẫn Sử Dụng](#-hướng-dẫn-sử-dụng)
- [API & PHP Endpoints](#-api--php-endpoints)
- [Bảo Mật](#-bảo-mật)
- [Triển Khai (Deployment)](#-triển-khai-deployment)
- [Kế Hoạch Phát Triển](#-kế-hoạch-phát-triển)
- [Giấy Phép](#-giấy-phép)

---

## 📌 Tổng Quan

CTL Store là một hệ thống bán giày dép & thời trang trực tuyến hoàn chỉnh, bao gồm:

- **Giao diện người dùng (Front-end):** Trang chủ, danh sách sản phẩm, chi tiết sản phẩm, tìm kiếm, giỏ hàng, thanh toán, đơn hàng, trang cá nhân.
- **Hệ thống xác thực:** Đăng ký, đăng nhập, đăng xuất, khôi phục mật khẩu.
- **Bảng điều khiển quản trị (Admin):** Dashboard thống kê, quản lý sản phẩm (thêm/sửa/xóa), quản lý danh mục.
- **Quản lý phiên & giỏ hàng:** Sử dụng PHP Session để lưu trữ trạng thái người dùng và giỏ hàng.

---

## ✨ Tính Năng Chính

### 🧑‍💻 Người Dùng (Frontend)

| Tính năng | Mô tả |
|-----------|-------|
| **Trang chủ** | Banner quảng cáo, danh mục nổi bật, sản phẩm bán chạy, đánh giá khách hàng, form đăng ký nhận tin |
| **Duyệt sản phẩm** | Xem tất cả sản phẩm với chế độ hiển thị lưới/danh sách |
| **Chi tiết sản phẩm** | Hình ảnh, mô tả, giá, biến thể (size/màu sắc), số lượng |
| **Tìm kiếm** | Tìm kiếm sản phẩm theo từ khóa |
| **Lọc theo danh mục** | Xem sản phẩm theo danh mục, lọc theo thuộc tính (size, màu sắc, thương hiệu) |
| **Giỏ hàng** | Thêm, sửa số lượng, xóa sản phẩm; hiển thị badge số lượng trên navbar |
| **Thanh toán (Checkout)** | Form nhập thông tin giao hàng, tổng quan đơn hàng, đặt hàng |
| **Đơn hàng** | Xem lịch sử đơn hàng, trạng thái, chi tiết từng đơn |
| **Hồ sơ cá nhân** | Cập nhật thông tin cá nhân (tên, email, số điện thoại, địa chỉ) |
| **Xác thực** | Đăng ký, đăng nhập, đăng xuất |
| **Kiểm tra email** | API kiểm tra email đã tồn tại khi đăng ký (AJAX) |
| **Responsive** | Giao diện thích ứng mọi thiết bị (mobile, tablet, desktop) |
| **Animation** | Hiệu ứng AOS (Animate on Scroll) mượt mà |
| **Scroll to top** | Nút cuộn lên đầu trang |

### 🔐 Quản Trị Viên (Admin Panel)

| Tính năng | Mô tả |
|-----------|-------|
| **Dashboard** | Thống kê tổng sản phẩm, đơn hàng, doanh thu; danh sách đơn hàng gần đây |
| **Quản lý danh mục** | Xem, thêm, sửa, xóa danh mục sản phẩm |
| **Quản lý sản phẩm** | Xem danh sách, thêm sản phẩm mới (có form chi tiết), sửa, xóa sản phẩm |

---

## 📁 Cấu Trúc Dự Án

```
CTL-Web/
│
├── index.php                 # Trang chủ - banner, danh mục, sản phẩm nổi bật
├── products.php              # Danh sách tất cả sản phẩm
├── product.php               # Chi tiết sản phẩm theo ID
├── categories.php            # Sản phẩm theo danh mục + bộ lọc thuộc tính
├── search.php                # Kết quả tìm kiếm sản phẩm
├── cart.php                  # Giỏ hàng (quản lý session)
├── cart_actions.php          # Xử lý AJAX thêm/xóa/cập nhật giỏ hàng
├── checkout.php              # Trang thanh toán
├── orders.php                # Lịch sử đơn hàng của người dùng
├── profile.php               # Hồ sơ & cập nhật thông tin cá nhân
├── login.php                 # Đăng nhập
├── register.php              # Đăng ký tài khoản
├── logout.php                # Đăng xuất
├── check_email.php           # AJAX endpoint: kiểm tra email tồn tại
├── get_category_attributes.php # AJAX: lấy thuộc tính lọc theo danh mục
├── debug.php                 # Debug/thông tin hệ thống
│
├── admin/                    # 🛠️ Bảng điều khiển quản trị
│   ├── index.php             # Dashboard quản trị
│   ├── categories.php        # Quản lý danh mục (CRUD)
│   ├── auth/                 # Xác thực admin
│   ├── includes/             # Header, footer, sidebar layout admin
│   └── products/             # Quản lý sản phẩm (CRUD)
│       ├── index.php         # Danh sách sản phẩm
│       ├── add.php           # Thêm sản phẩm
│       ├── edit.php          # Sửa sản phẩm
│       └── delete.php        # Xóa sản phẩm
│
├── includes/                 # 📦 Thành phần dùng chung
│   ├── config.php            # Cấu hình DB, kết nối MySQL
│   ├── config_local.php      # Cấu hình DB cho môi trường local
│   ├── session_config.php    # Cấu hình session (thời gian, cookie)
│   ├── functions.php         # Hàm tiện ích (isLoggedIn, cart helpers, etc.)
│   ├── header.php            # Header toàn trang (navbar, cart badge, auth)
│   ├── footer.php            # Footer toàn trang + script assets
│   ├── category_functions.php # Hàm xử lý danh mục & attributes
│   └── category_components.php # Component hiển thị danh mục (UI)
│
├── css/
│   └── style.css             # 📝 Stylesheet tùy chỉnh
│
├── js/
│   ├── script.js             # JavaScript chính (cart, search, interactions)
│   └── profile-validation.js # Validate form hồ sơ (phía client)
│
├── images/                   # 🖼️ Tài nguyên hình ảnh
│   ├── logo.png              # Logo CTL Store
│   ├── hero-image.png        # Ảnh banner trang chủ
│   └── newsletter-image.png  # Ảnh form đăng ký nhận tin
│
├── .htaccess                 # Cấu hình Apache (URL rewriting, bảo mật)
├── .htaccess_local           # Cấu hình Apache cho môi trường local
├── .htaccess.production      # Cấu hình Apache cho production
├── shoe_store.sql            # 📊 Database dump
│
├── 403.php                   # Trang lỗi 403 (Forbidden)
└── 404.php                   # Trang lỗi 404 (Not Found)
```

---

## 🛠 Công Nghệ Sử Dụng

### Backend
| Công nghệ | Mục đích |
|-----------|----------|
| **PHP 8.x** | Ngôn ngữ lập trình backend chính (thuần, không framework) |
| **MySQL** | Cơ sở dữ liệu quan hệ |
| **MySQLi** | Extension kết nối PHP - MySQL (persistent connection) |
| **PHP Sessions** | Quản lý phiên đăng nhập & giỏ hàng |

### Frontend
| Công nghệ | Mục đích |
|-----------|----------|
| **HTML5** | Cấu trúc trang |
| **CSS3** | Định dạng giao diện |
| **Bootstrap 5.3** | Framework CSS (grid, components, utilities) |
| **Bootstrap Icons** | Thư viện icon |
| **Google Fonts (Poppins)** | Font chữ hiện đại |
| **AOS 2.3** (Animate on Scroll) | Hiệu ứng xuất hiện khi cuộn trang |
| **JavaScript (Vanilla)** | Xử lý phía client (AJAX, DOM manipulation) |
| **jQuery** | Hỗ trợ AJAX & thao tác DOM |

### Server
| Công nghệ | Mục đích |
|-----------|----------|
| **Apache** | Web server (cấu hình qua .htaccess) |
| **InfinityFree** | Hosting miễn phí (deploy hiện tại) |

---

## 🗄 Cơ Sở Dữ Liệu

CSDL `shoe_store` gồm các bảng chính:

| Bảng | Mô tả | Các cột chính |
|------|-------|---------------|
| `categories` | Danh mục sản phẩm | id, name, description, parent_id, slug, image, is_featured |
| `products` | Sản phẩm | id, category_id, name, slug, description, price, sale_price, image, sizes (JSON), colors (JSON), stock, is_featured, created_at |
| `users` | Người dùng | id, full_name, email, password (hashed), phone, address, role, created_at |
| `orders` | Đơn hàng | id, user_id, customer_name, email, phone, address, total_amount, status, order_date |
| `order_items` | Chi tiết đơn hàng | id, order_id, product_id, product_name, price, quantity |
| `cart` | Giỏ hàng (persistent) | id, user_id, product_id, quantity, created_at |

> **Lưu ý:** File dump CSDL tại `shoe_store.sql`.

---

## 🚀 Hướng Dẫn Cài Đặt

### Yêu cầu hệ thống
- PHP 8.0 trở lên
- MySQL 5.7+ hoặc MariaDB 10.3+
- Apache với mod_rewrite (hoặc Nginx)
- Extension PHP: `mysqli`, `session`, `json`, `mbstring`

### Các bước cài đặt

#### 1. Clone repository
```bash
git clone https://github.com/linh404/CTL-web.git
cd CTL-Web
```

#### 2. Import cơ sở dữ liệu

- Tạo database mới (ví dụ: `shoe_store`)
- Import file `shoe_store.sql`:
```bash
mysql -u username -p shoe_store < shoe_store.sql
```

#### 3. Cấu hình kết nối database

Tạo/Cập nhật file `includes/config_local.php`:

```php
<?php
define('DB_SERVER', 'localhost');
define('DB_USERNAME', 'your_username');
define('DB_PASSWORD', 'your_password');
define('DB_NAME', 'shoe_store');
```

> **Mẹo:** Đổi `require_once` trong file `includes/config.php` thành `config_local.php` khi chạy local.

#### 4. Cấu hình Apache (nếu cần)

- Đảm bảo `mod_rewrite` được bật
- File `.htaccess_local` chứa cấu hình cho môi trường local

#### 5. Khởi chạy

**Sử dụng PHP Built-in Server:**
```bash
php -S localhost:8000
```
Truy cập: `http://localhost:8000`

**Sử dụng XAMPP/WAMP/Laragon:**
- Đặt thư mục dự án vào `htdocs` (XAMPP) hoặc `www` (WAMP)
- Truy cập: `http://localhost/CTL-Web`

---

## 📖 Hướng Dẫn Sử Dụng

### 🌐 Người Dùng

1. **Trang chủ** (`index.php`) - Xem banner, danh mục, sản phẩm nổi bật
2. **Đăng ký** (`register.php`) - Tạo tài khoản mới
3. **Đăng nhập** (`login.php`) - Đăng nhập vào hệ thống
4. **Duyệt sản phẩm** (`products.php` hoặc `categories.php?category=ID`) - Khám phá sản phẩm
5. **Tìm kiếm** - Sử dụng ô tìm kiếm trên navbar
6. **Chi tiết sản phẩm** - Click vào sản phẩm để xem chi tiết & thêm vào giỏ
7. **Giỏ hàng** (`cart.php`) - Xem & chỉnh sửa giỏ hàng
8. **Thanh toán** (`checkout.php`) - Nhập thông tin & đặt hàng
9. **Đơn hàng** (`orders.php`) - Theo dõi đơn hàng đã đặt
10. **Hồ sơ** (`profile.php`) - Cập nhật thông tin cá nhân

### 🔧 Quản Trị Viên

1. **Dashboard** - Truy cập `admin/index.php`
2. **Quản lý sản phẩm** - `admin/products/index.php`
   - Thêm sản phẩm: `admin/products/add.php`
   - Sửa sản phẩm: Click "Sửa" trên danh sách
   - Xóa sản phẩm: Click "Xóa" trên danh sách
3. **Quản lý danh mục** - `admin/categories.php`

> **Tài khoản admin mặc định:** Cần tạo tài khoản có `role = 'admin'` trong bảng `users`.

---

## 🔌 API & PHP Endpoints

### Public Pages
| Endpoint | Phương thức | Mô tả |
|----------|-------------|-------|
| `/index.php` | GET | Trang chủ |
| `/products.php` | GET | Danh sách sản phẩm |
| `/product.php?id=N` | GET | Chi tiết sản phẩm |
| `/categories.php?category=ID` | GET | Sản phẩm theo danh mục |
| `/search.php?q=keyword` | GET | Tìm kiếm sản phẩm |
| `/cart.php` | GET | Giỏ hàng |
| `/checkout.php` | GET/POST | Thanh toán |
| `/orders.php` | GET | Đơn hàng của tôi |
| `/profile.php` | GET/POST | Cập nhật hồ sơ |
| `/login.php` | GET/POST | Đăng nhập |
| `/register.php` | GET/POST | Đăng ký |
| `/logout.php` | GET | Đăng xuất |

### AJAX Endpoints
| Endpoint | Mô tả |
|----------|-------|
| `POST /cart_actions.php` | Xử lý thêm/sửa/xóa sản phẩm trong giỏ hàng (AJAX) |
| `GET /cart_actions.php?action=get_count` | Lấy số lượng sản phẩm trong giỏ (AJAX) |
| `POST /check_email.php` | Kiểm tra email đã tồn tại |
| `GET /get_category_attributes.php?category_id=ID` | Lấy thuộc tính lọc theo danh mục |

---

## 🔒 Bảo Mật

- **Mật khẩu:** Được băm bằng `password_hash()` (bcrypt)
- **SQL Injection:** Sử dụng MySQLi prepared statements
- **XSS:** Dùng `htmlspecialchars()` khi output dữ liệu người dùng
- **Session:** Cấu hình bảo mật session qua `session_config.php`:
  - `httponly` & `samesite=Lax` cho cookie session
  - Thời gian timeout có cấu hình
- **File .htaccess:** Chặn truy cập thư mục nhạy cảm (includes, admin/auth)

---

## 🌍 Triển Khai (Deployment)

Hiện tại dự án được triển khai trên **InfinityFree** (hosting miễn phí).

### Hướng dẫn deploy lên hosting:

1. Upload toàn bộ source code lên thư mục `htdocs` (hoặc tương đương)
2. Import file `shoe_store.sql` vào database trên hosting
3. Cập nhật thông tin database trong `includes/config.php`
4. Cấu hình `.htaccess` cho production
5. Đảm bảo PHP version ≥ 8.0

### Biến môi trường & cấu hình
- **Development:** Sử dụng `config_local.php`
- **Production:** Sử dụng `config.php` với thông tin hosting

---

## 📈 Kế Hoạch Phát Triển

- [ ] **API RESTful** - Xây dựng API cho mobile app
- [ ] **Thanh toán online** - Tích hợp VNPay, MoMo
- [ ] **Quản lý kho** - Theo dõi tồn kho tự động
- [ ] **Đánh giá sản phẩm** - Người dùng có thể đánh giá & comment
- [ ] **Yêu thích (Wishlist)** - Danh sách sản phẩm yêu thích
- [ ] **Coupon/Giảm giá** - Mã giảm giá & khuyến mãi
- [ ] **Thông báo email** - Xác nhận đơn hàng qua email
- [ ] **Quản lý người dùng (Admin)** - CRUD người dùng từ admin
- [ ] **Export báo cáo** - Xuất Excel/PDF thống kê
- [ ] **Tối ưu SEO** - Meta tags, sitemap, structured data
- [ ] **PWA** - Progressive Web App support
- [ ] **Đa ngôn ngữ** - Hỗ trợ tiếng Việt & tiếng Anh

---

## 🤝 Đóng Góp

Mọi đóng góp đều được hoan nghênh! Vui lòng:

1. Fork dự án
2. Tạo branch feature (`git checkout -b feature/AmazingFeature`)
3. Commit thay đổi (`git commit -m 'Add some AmazingFeature'`)
4. Push lên branch (`git push origin feature/AmazingFeature`)
5. Mở Pull Request

---

## 📄 Giấy Phép

Dự án được phân phối dưới giấy phép **MIT**. Xem file `LICENSE` để biết thêm chi tiết.

---

## 📬 Liên Hệ

- **Website:** [ctl-store.kesug.com](https://ctl-store.kesug.com)
- **Email:** contact@ctl.com
- **Địa chỉ:** Số 141 Đường Chiến Thắng, Tân Triều, Thanh Trì, Hà Nội
- **GitHub:** [github.com/linh404/CTL-web](https://github.com/linh404/CTL-web)

---

<p align="center">
  <strong>⭐ Đừng quên để lại star nếu bạn thấy dự án hữu ích! ⭐</strong>
</p>