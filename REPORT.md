# REPORT - Session 09 Bài 2: Nginx Container & Port Mapping

**Họ tên:** Nguyễn Thế Kiên | **Lớp:** K24 - DevOps PTIT

## Mục tiêu
Chạy Nginx container ở chế độ ngầm (-d), ánh xạ cổng 8080:80, kiểm tra bằng curl rồi dọn dẹp.

---

## 1. Khởi chạy container
```bash
docker run -d -p 8080:80 --name my-web nginx:alpine
```
```
Unable to find image 'nginx:alpine' locally
alpine: Pulling from library/nginx
766d3311d5df: Pull complete 
1efec2485f45: Pull complete 
ccea4a153c59: Pull complete 
943c389642fa: Pull complete 
bc862a9910f5: Pull complete 
d766d06974fa: Pull complete 
858f76146c12: Pull complete 
6c2852a60c45: Download complete 
dffc70821449: Download complete 
Digest: sha256:df221db836e1754089190208cee7eeda94f233197056426eda74a43ab1abeac2
Status: Downloaded newer image for nginx:alpine
6efa808daf78ca766f7bd3daedc7502225a975810a1254597361fbd8f4c560a7```

## 2. Kiểm tra container đang chạy
```bash
docker ps
```
```
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS                   PORTS                                         NAMES
6efa808daf78   nginx:alpine          "/docker-entrypoint.…"   20 seconds ago   Up 20 seconds            0.0.0.0:8080->80/tcp, [::]:8080->80/tcp       my-web
2bf9cb40c995   langfuse/langfuse:2   "dumb-init -- ./web/…"   12 days ago      Up 8 minutes             0.0.0.0:3000->3000/tcp, [::]:3000->3000/tcp   ptit_final_ai_integrated_007-langfuse-server-1
e0a7fd682b64   postgres:16-alpine    "docker-entrypoint.s…"   12 days ago      Up 8 minutes (healthy)   0.0.0.0:5433->5432/tcp, [::]:5433->5432/tcp   ptit_final_ai_integrated_007-langfuse-db-1```

## 3. Truy vấn web bằng curl
```bash
curl http://localhost:8080
```
```
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
</html>```

## 4. Dọn dẹp
```bash
docker stop my-web && docker rm my-web
```
```
nguyenthekien@MacBookAir homework_session_09_ex2 % docker stop my-web && docker rm my-web

my-web
my-web```

---

## Giải thích tham số
- `-d` : detached — chạy ngầm, trả về terminal ngay.
- `-p 8080:80` : ánh xạ cổng 8080 (máy host) → 80 (bên trong container Nginx).
- `--name my-web` : đặt tên container cho dễ quản lý.
- `nginx:alpine` : image Nginx bản Alpine siêu nhẹ.

## Kết quả
Lệnh `curl http://localhost:8080` trả về HTML chứa:
> Welcome to nginx!
