# Tech Store - Cửa Hàng Công Nghệ 🛍️

Nền tảng e-commerce hoàn chỉnh bằng **Flask** + **SQLAlchemy**. Hỗ trợ đầy đủ: mua sắm, giỏ hàng, thanh toán, quản lý đơn hàng, panel admin CRUD.

## ✨ Tính Năng Chính

- **👤 Tài khoản**: Đăng ký/đăng nhập/đăng xuất, lịch sử đơn hàng
- **🛍️ Sản phẩm**: Danh sách (12/trang, phân trang), chi tiết, thêm giỏ nhanh (JS)
- **🛒 Giỏ hàng**: Thêm/xóa/sửa số lượng, tính tổng
- **💳 Thanh toán**: Checkout → Order success, cập nhật kho tự động
- **📦 Đơn hàng**: Lịch sử + trạng thái (pending/paid/shipped/delivered)
- **👨‍💼 Admin**: CRUD sản phẩm (add/update/delete/adjust inventory), quản lý đơn hàng/người dùng, AJAX APIs

**Admin mặc định**: `admin` / `admin123` (tự tạo DB init)

## 🚀 Cài Đặt & Chạy

### Local (SQLite dev)
```bash
pip install -r requirements.txt
python app.py
```
→ **http://localhost:5000** (auto tạo DB + 8 sản phẩm mẫu)

### Docker
```bash
docker build -t techstore .
docker run -p 5000:5000 techstore
```

### Render (từ render.yaml + PostgreSQL)
Push Git → Render auto-deploy (env: SECRET_KEY auto-gen, DATABASE_URL từ service)

## 🔐 Tài Khoản Test

| Role | Username | Password |
|------|----------|----------|
| Admin | admin | admin123 |

## 📁 Cấu Trúc Dự Án (Đầy Đủ)

```
web_v1/                          # Current dir
├── .gitignore
├── app.py                      # Flask app + models + routes + DB init
├── requirements.txt            # Flask/SQLAlchemy/Werkzeug/psycopg2/gunicorn
├── Dockerfile                  # Docker build
├── render.yaml                 # Render deploy (Docker + Postgres Singapore)
├── README.md                   # This file
├── static/
│   └── style.css               # Responsive CSS
└── templates/                  # Jinja2 HTML
    ├── layout.html             # Base layout
    ├── index.html              # Home/products grid + pagination + quick cart
    ├── product_detail.html     # Product view
    ├── cart.html               # Cart management
    ├── checkout.html           # Payment form
    ├── order_success.html      # Order confirmation
    ├── orders.html             # User orders history
    ├── admin.html              # Admin dashboard (tabs: products/orders/users)
    ├── login.html              # Auth
    └── register.html           # Signup
```

## 🔗 Chính Routes/Endpoints (từ app.py)

**User**:
- `/` (GET): Products paginated (12/page)
- `/product/<id>`: Detail
- `/register`, `/login`, `/logout`
- `/cart`, `/add-to-cart/<id>` (POST qty), `/remove-from-cart/<id>`
- `/checkout` (POST → order), `/order-success/<id>`, `/orders`

**Admin** (is_admin only):
- `/admin` (GET): Dashboard
- `/admin/add-product` (POST form)
- `/admin/update-product/<id>`, `/admin/delete-product/<id>` (POST/AJAX)
- `/admin/adjust-inventory` (POST), `/admin/update-order-status/<id>`
- `/admin/product/<id>`, `/admin/order/<id>` (JSON APIs)

**Errors**: 404/500 handlers

## 🗄️ Database Models (SQLAlchemy)

| Model | Fields | Relations |
|-------|--------|-----------|
| **User** | id, username*, email*, password*, is_admin, created_at | orders |
| **Product** | id, name*, desc, price*, qty, image_url, created_at | order_items, cart_items |
| **Order** | id, user_id*, total_price*, status*, created_at | items (OrderItem) |
| **OrderItem** | id, order_id*, product_id*, qty*, price* | order, product |
| **CartItem** | id, user_id, product_id*, qty | product |

*required; Auto-init: admin + 8 tech products (iPhone15, MacBook M2, etc.)

## 🎨 Tính Năng Giao Diện

- ✅ **Responsive Design**: Hỗ trợ Mobile, Tablet, Desktop
- ✅ **Modern UI**: Gradient backgrounds, smooth animations
- ✅ **Dark-Light Support**: Tối ưu một cho cả mode sáng
- ✅ **Form Validation**: Server-side & Client-side
- ✅ **Error Handling**: 404, 500 pages
- ✅ **Flash Messages**: Thông báo thành công/lỗi

## 🔧 Biến Môi Trường

```bash
# Tùy chọn (sẽ sử dụng mặc định nếu không thiết lập)
SECRET_KEY=your-secret-key         # Flask session key
DATABASE_URL=sqlite:///shop.db      # Database connection
FLASK_ENV=development               # development hoặc production
PORT=5000                           # Port để chạy server
```

## 📚 Công Nghệ Sử Dụng

- **Backend**: Flask 2.3.2, SQLAlchemy 3.0.5
- **Database**: SQLite (development) / PostgreSQL (production)
- **Frontend**: HTML5, CSS3, JavaScript (vanilla)
- **Security**: Werkzeug password hashing
- **Deployment**: Docker, Render, Gunicorn


## 🌐 Deploy

### Deploy lên Render
```bash
git push # Render sẽ tự động build từ render.yaml
```

### Deploy lên Docker
```bash
docker build -t techstore .
docker run -p 5000:5000 techstore
```

## 📝 License
MIT License - Tự do sử dụng cho mục đích cá nhân & thương mại

## 👥 Hỗ Trợ

### Bước 3: Cài Đặt Dependencies
```bash
pip install -r requirements.txt
```

### Bước 4: Chạy Ứng Dụng
```bash
python app.py
```

Truy cập ứng dụng tại: **http://localhost:5000**

## 📝 Tài Khoản Admin Mặc Định
- **Tên Đăng Nhập**: admin
- **Mật Khẩu**: admin123

## 📁 Cấu Trúc Dự Án
```
web_v1/
├── app.py                 # Ứng dụng chính
├── requirements.txt       # Dependencies
├── Dockerfile            # Docker configuration
├── .env                  # Biến môi trường
├── templates/            # HTML templates
│   ├── layout.html      # Giao diện chung
│   ├── index.html       # Trang chủ
│   ├── login.html       # Đăng nhập
│   ├── register.html    # Đăng ký
│   ├── product_detail.html  # Chi tiết sản phẩm
│   ├── cart.html        # Giỏ hàng
│   ├── checkout.html    # Thanh toán
│   ├── order_success.html   # Đơn hàng thành công
│   ├── orders.html      # Lịch sử đơn hàng
│   └── admin.html       # Trang quản trị
└── static/              # Tài nguyên tĩnh (CSS, JS, ảnh)
```

## 🗄️ Cơ Sở Dữ Liệu

### Models
1. **User** - Người dùng
2. **Product** - Sản phẩm
3. **Order** - Đơn hàng
4. **OrderItem** - Chi tiết đơn hàng
5. **CartItem** - Giỏ hàng

## 🐳 Docker

Để chạy ứng dụng trong Docker:

```bash
docker build -t tech-store .
docker run -p 5000:5000 tech-store
```



---
**Phiên Bản**: 1.0.0  
**Ngày Cập Nhật**: Tháng 2, 2026
