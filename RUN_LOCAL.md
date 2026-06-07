# RUN_LOCAL.md – Hướng dẫn chạy Lab 04

Tài liệu này giúp người khác clone repo sạch và chạy lại service trong Docker.

---

## 1. Clone repo

```bash
git clone <repo-url>
cd FIT4110_lab04_docker_packaging
```

---

## 2. Cài dependencies cho Newman/Prism/Spectral

```bash
npm install
```

---

## 3. Tạo file cấu hình runtime

```bash
cp .env.example .env
```

Trên PowerShell:

```powershell
Copy-Item .env.example .env
```

---

## 4. Build Docker image

```bash
docker build -t fit4110/iot-ingestion:lab04 .
```

---

## 5. Run container

```bash
docker run --rm \
  --name fit4110-iot-lab04 \
  -p 8000:8000 \
  --env-file .env \
  fit4110/iot-ingestion:lab04
```

Mở terminal khác, kiểm tra:

```bash
curl http://localhost:8000/health
```

Kết quả mong đợi:

```json
{
  "status": "ok",
  "service": "iot-ingestion",
  "version": "0.4.0"
}
```

---

## 6. Chạy Newman test trên container

```bash
npm run test:local
```

Report sinh tại:

```text
reports/newman-lab04-local.xml
reports/newman-lab04-local.html
```

---

## 7. Dừng container

Nếu không dùng `--rm` hoặc container còn chạy:

```bash
docker stop fit4110-iot-lab04
```

---

## 8. Lệnh nhanh

```bash
make build
make run
make test-docker
make stop
```
