# Docker Evidence - Lab 04

Generated on: 2026-06-07

## Team

- Team name: `team-iot`
- Service: `iot-ingestion`
- Image tags:
  - `fit4110/iot-ingestion:lab04`
  - `fit4110/iot-ingestion:v0.1.0-team-iot`

## 1. Build Evidence

Command:

```bash
docker build -t fit4110/iot-ingestion:lab04 .
docker tag fit4110/iot-ingestion:lab04 fit4110/iot-ingestion:v0.1.0-team-iot
```

Result:

```text
fit4110/iot-ingestion:lab04             b8e310db7726   268MB
fit4110/iot-ingestion:v0.1.0-team-iot   b8e310db7726   268MB
```

Image metadata verified:

```text
User: appuser
Healthcheck: GET http://127.0.0.1:8000/health
Exposed port: 8000/tcp
```

## 2. Run Evidence

Command:

```bash
cp .env.example .env
docker run -d --rm --name fit4110-iot-lab04 -p 8000:8000 --env-file .env fit4110/iot-ingestion:lab04
```

Container status:

```text
fit4110-iot-lab04   Up   healthy   0.0.0.0:8000->8000/tcp
```

## 3. Healthcheck Evidence

Command:

```bash
curl http://localhost:8000/health
```

Result:

```json
{"status":"ok","service":"iot-ingestion","version":"0.4.0"}
```

## 4. Newman Evidence

Command:

```bash
npm run test:local
```

Summary:

```text
iterations: 1 executed, 0 failed
requests: 11 executed, 0 failed
test-scripts: 11 executed, 0 failed
assertions: 19 executed, 0 failed
average response time: 7ms
```

Generated reports:

```text
reports/newman-lab04-local.xml
reports/newman-lab04-local.html
```

## 5. Registry Note

Local image tagging is complete. Registry push was not performed because it requires a real registry owner and credentials. If required, push with:

```bash
docker tag fit4110/iot-ingestion:lab04 ghcr.io/<owner>/team-iot:v0.1.0-team-iot
docker push ghcr.io/<owner>/team-iot:v0.1.0-team-iot
```
