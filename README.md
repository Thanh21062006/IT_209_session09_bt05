# Báo cáo Bài 5: Khởi chạy dịch vụ đơn giản với Docker Compose

## 1. Mục tiêu
- Làm quen với cú pháp và cách cấu hình công cụ quản lý multi-container bằng Docker Compose (CLI v2).
- Viết tệp cấu hình khai báo `docker-compose.yml` tối giản để triển khai một dịch vụ Web Nginx.
- Quản lý vòng đời dịch vụ bằng các lệnh: `docker compose up -d`, `docker compose ps`, `docker compose down`.

## 2. Cấu trúc mã nguồn

Thư mục bài làm bao gồm:
```text
.
├── docker-compose.yml
└── README.md
```

### Nội dung `docker-compose.yml`:
```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8082:80"
```

---

## 3. Các bước thực hiện và lệnh đã sử dụng

### Bước 1: Khởi chạy dịch vụ ở chế độ chạy ngầm
```bash
docker compose up -d
```

### Bước 2: Kiểm tra trạng thái dịch vụ
```bash
docker compose ps
```

### Bước 3: Gửi truy vấn HTTP kiểm tra trang web
```bash
curl http://localhost:8082
```

### Bước 4: Hạ dịch vụ và dọn dẹp tài nguyên
```bash
docker compose down
```

---

## 4. Nhật ký kết quả đầu ra thực tế từ Terminal

### 4.1. Khởi chạy và kiểm tra dịch vụ (`docker compose up -d` & `ps`)
```text
 Network ss09_hw05_daotrongtri_ptit062_default Creating 
 Network ss09_hw05_daotrongtri_ptit062_default Created 
 Container ss09_hw05_daotrongtri_ptit062-web-1 Creating 
 Container ss09_hw05_daotrongtri_ptit062-web-1 Created 
 Container ss09_hw05_daotrongtri_ptit062-web-1 Starting 
 Container ss09_hw05_daotrongtri_ptit062-web-1 Started 

NAME                                        IMAGE          COMMAND                  SERVICE   CREATED         STATUS        PORTS
ss09_hw05_daotrongtri_ptit062-web-1         nginx:alpine   "/docker-entrypoint.…"   web       2 seconds ago   Up 1 second   0.0.0.0:8082->80/tcp, [::]:8082->80/tcp
```

### 4.2. Kiểm tra phản hồi bằng `curl http://localhost:8082`
```text
HTTP/1.1 200 OK
Server: nginx/1.31.6
Date: Mon, 12 Oct 2026 12:58:48 GMT
Content-Type: text/html
Content-Length: 896
Last-Modified: Tue, 15 Sep 2026 14:18:52 GMT
Connection: keep-alive
ETag: "6aa953cc-380"
Accept-Ranges: bytes

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, nginx is successfully installed and working.
Further configuration is required for the web server, reverse proxy, 
API gateway, load balancer, content cache, or other features.</p>

<p>For online documentation and support please refer to
<a href="https://nginx.org/">nginx.org</a>.<br/>
To engage with the community please visit
<a href="https://community.nginx.org/">community.nginx.org</a>.<br/>
For enterprise grade support, professional services, additional 
security features and capabilities please refer to
<a href="https://f5.com/nginx">f5.com/nginx</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

### 4.3. Hạ dịch vụ (`docker compose down`)
```text
 Container ss09_hw05_daotrongtri_ptit062-web-1 Stopping 
 Container ss09_hw05_daotrongtri_ptit062-web-1 Stopped 
 Container ss09_hw05_daotrongtri_ptit062-web-1 Removing 
 Container ss09_hw05_daotrongtri_ptit062-web-1 Removed 
 Network ss09_hw05_daotrongtri_ptit062_default Removing 
 Network ss09_hw05_daotrongtri_ptit062_default Removed 
```

---

## 5. So sánh Docker CLI và Docker Compose

| Đặc điểm | Docker CLI (`docker run`) | Docker Compose (`docker compose`) |
| :--- | :--- | :--- |
| **Cách tiếp cận** | Lệnh mệnh lệnh (Imperative): Phải nhớ và gõ nhiều cờ tham số (`-d`, `-p`, `--name`, v.v.). | Khai báo (Declarative): Mọi cấu hình dịch vụ, mạng, cổng được định nghĩa tập trung trong tệp YAML (`docker-compose.yml`). |
| **Quản lý đa container** | Phức tạp, phải chạy từng câu lệnh riêng lẻ cho từng dịch vụ và kết nối mạng thủ công. | Dễ dàng quản lý đồng thời toàn bộ stack ứng dụng chỉ với một lệnh duy nhất (`docker compose up / down`). |
| **Tính tái lập & Chia sẻ** | Dễ nhầm lẫn khi chuyển đổi giữa các môi trường nếu không ghi chép lại lệnh. | File cấu hình có thể version control qua Git, dễ dàng chia sẻ và tái lập môi trường đồng nhất. |

---

## 6. Hướng dẫn chụp ảnh minh chứng & Placeholder
1. Chạy tuần tự các lệnh:
   ```bash
   docker compose up -d
   docker compose ps
   curl http://localhost:8082
   ```
2. Chụp ảnh màn hình hiển thị service `web` đang chạy cổng 8082 trong bảng `docker compose ps` và kết quả trả về của lệnh `curl`.
3. Dán ảnh vào vị trí placeholder bên dưới:

`ImgEx`
