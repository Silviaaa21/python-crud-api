
# Python CRUD API

Project praktikum CI/CD Pipeline menggunakan Jenkins, GitHub, Docker, dan ngrok.

## Deskripsi
Aplikasi REST API sederhana menggunakan Python dengan fitur pengelolaan pesan.

## Fitur
- GET /health
- GET /messages
- POST /messages
- DELETE /messages?index=N

## Teknologi
- Python 3
- Docker
- Jenkins
- GitHub
- ngrok

## Menjalankan Aplikasi
Build Docker image:

```bash
docker build -t python-crud-api:manual .
```

Jalankan container:

```bash
docker run -d --name production-api-container -p 5000:5000 -v production-api-data:/var/lib/backend_data python-crud-api:manual
```

Periksa health:

```bash
curl http://localhost:5000/health
```
