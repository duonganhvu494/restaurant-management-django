# 🍽️ Hệ Thống Quản Lý Nhà Hàng

Một hệ thống quản lý nhà hàng được xây dựng bằng Django, xây dựng bằng mô hình truyền thống MVC, cung cấp giải pháp toàn diện cho việc quản lý hoạt động của nhà hàng.

## ✨ Tính năng chính

### 👥 Quản lý Nhân viên
- Hệ thống phân quyền với 4 vai trò: Admin, Quản lý, Bếp, Phục vụ
- Quản lý ca làm việc và chấm công
- Theo dõi nhân viên đang trong ca

### 🍽️ Quản lý Menu
- Thêm, sửa, xóa món ăn
- Phân loại món: Khai vị, Món chính, Tráng miệng
- Tính toán lợi nhuận từ giá bán và chi phí
- Tìm kiếm món ăn

### 🪑 Quản lý Bàn
- Quản lý trạng thái bàn (trống/có khách)
- Tự động tạo QR code cho mỗi bàn
- Khách hàng có thể quét QR để gọi món

### 📝 Quản lý Đơn hàng
- Tạo đơn hàng cho từng bàn
- Theo dõi trạng thái món ăn: Chưa lên món → Đã lên món → Đã nhận món
- Áp dụng mã khuyến mãi
- Thanh toán và tính lợi nhuận

### 🎁 Hệ thống Khuyến mãi
- Tạo và quản lý mã khuyến mãi
- Áp dụng giảm giá theo phần trăm

### 📊 Báo cáo Doanh thu
- Xem chi tiết các đơn hàng đã thanh toán
- Thống kê lợi nhuận
- Tìm kiếm đơn hàng theo nhiều tiêu chí

## 🛠️ Công nghệ sử dụng

- **Backend**: Django 5.1.4
- **Database**: MySQL
- **Frontend**: HTML, CSS, Bootstrap 5.3.0
- **QR Code**: qrcode library
- **Environment Management**: python-dotenv

## 📋 Yêu cầu hệ thống

- Python 3.8+
- MySQL 5.7+
- pip

## 🚀 Hướng dẫn cài đặt

### 1. Clone repository
```bash
git clone <repository-url>
cd restaurant-management
```

### 2. Tạo virtual environment
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate
```

### 3. Cài đặt dependencies
```bash
pip install -r requirements.txt
```

### 4. Cấu hình database
- Tạo database MySQL
- Sao chép file `.env.example` thành `.env`
- Cập nhật thông tin database trong file `.env`

### 5. Chạy migrations
```bash
cd quanlynhahang
python manage.py makemigrations
python manage.py migrate
```

### 6. Tạo superuser
```bash
python manage.py createsuperuser
```

### 7. Chạy server
```bash
python manage.py runserver
```

Truy cập http://127.0.0.1:8000 để sử dụng ứng dụng.

## 📁 Cấu trúc thư mục

```
restaurant-management/
├── quanlynhahang/              # Django project root
│   ├── manage.py              # Django management script
│   ├── .env.example              # Environment variables template
│   ├── quanlynhahang/         # Project settings
│   │   ├── settings.py        # Django settings
│   │   ├── urls.py           # Main URL configuration
│   │   └── ...
│   ├── rm/                    # Main application
│   │   ├── models.py         # Database models
│   │   ├── views.py          # Business logic
│   │   ├── urls.py           # URL routing
│   │   ├── forms.py          # Django forms
│   │   ├── admin.py          # Admin interface
│   │   ├── templates/        # HTML templates
│   │   ├── static/           # CSS, JS, images
│   │   └── migrations/       # Database migrations
│   └── media/                 # User uploaded files
│       └── qrcodes/          # Generated QR codes
├── requirements.txt           # Python dependencies
└── README.md                 # This file
```

## 👤 Hệ thống phân quyền

### Admin
- Toàn quyền truy cập tất cả tính năng
- Quản lý nhân viên
- Quản lý menu

### Quản lý (Manager)
- Xem doanh thu và báo cáo
- Quản lý đơn hàng
- Quản lý bàn

### Bếp (Kitchen)
- Xem đơn hàng
- Cập nhật trạng thái món ăn (Chưa lên → Đã lên món)

### Phục vụ (Waiter)
- Tạo đơn hàng
- Cập nhật trạng thái món ăn (Đã lên → Đã nhận món)
- Thanh toán

## 🔧 Cấu hình

### Environment Variables
Tham khảo file `.env.example` để biết các biến môi trường cần thiết:

- `DJANGO_SECRET_KEY`: Secret key cho Django
- `DJANGO_DEBUG`: Chế độ debug (True/False)
- `DB_NAME`: Tên database
- `DB_USER`: Username database
- `DB_PASSWORD`: Password database
- `DB_HOST`: Host database
- `DB_PORT`: Port database
- `SITE_URL`: URL của website (để tạo QR code)

### Database
Project sử dụng MySQL làm database chính. Cấu hình trong `settings.py`:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': os.getenv("DB_NAME"),
        'USER': os.getenv("DB_USER"),
        'PASSWORD': os.getenv("DB_PASSWORD"),
        'HOST': os.getenv("DB_HOST", "localhost"),
        'PORT': os.getenv("DB_PORT", "3306"),
    }
}
```

## 📱 Tính năng QR Code

Mỗi bàn được tự động tạo QR code khi thêm vào hệ thống. Khách hàng có thể:
1. Quét QR code trên bàn
2. Xem menu và gọi món trực tiếp
3. Theo dõi trạng thái đơn hàng

## 🔄 Workflow hoạt động

1. **Nhân viên phục vụ** tạo đơn hàng cho bàn
2. **Khách hàng** có thể quét QR để gọi thêm món
3. **Bếp** xem đơn hàng và cập nhật trạng thái "Đã lên món"
4. **Phục vụ** mang món và cập nhật "Đã nhận món"
5. **Phục vụ/Quản lý** thực hiện thanh toán
6. Hệ thống tự động tính lợi nhuận và cập nhật trạng thái bàn



⭐ Nếu project này hữu ích, hãy cho một star nhé!
