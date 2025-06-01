# Docker Compose Mashqlar

## Mashq 1: Oddiy Web Server

**Maqsad:** Nginx web server bilan tanishish va static website yaratish

### Vazifa:

1. `nginx` image'dan foydalanib web server yarating
2. Port 8080'da ishlasin
3. Öz HTML sahifangizni yarating va serve qiling

### Qadamlar:

1. Yangi papka yarating: `mkdir web-server && cd web-server`
2. `index.html` file yarating:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mening Birinchi Docker Web Saytim</title>
  </head>
  <body>
    <h1>Salom Docker!</h1>
    <p>Bu mening birinchi Docker bilan yaratgan web saytim.</p>
  </body>
</html>
```

3. `docker-compose.yml` file yarating
4. Browser'da `http://localhost:8080` ga kirib natijani tekshiring

### Kutilayotgan natija:

- Web sayt 8080 portda ochilishi
- Sizning HTML sahifangiz ko'rinishi

---

## Mashq 2: Node.js API + PostgreSQL

**Maqsad:** Backend va Database service'larini birlashtirish

### Vazifa:

1. Node.js backend yarating
2. PostgreSQL database ulang
3. Health check endpoint yarating

### Qadamlar:

1. Yangi papka: `mkdir api-db && cd api-db`
2. `package.json` yarating:

```json
{
  "name": "simple-api",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.0",
    "pg": "^8.8.0"
  }
}
```

3. `server.js` yarating (oddiy Express server)
4. `Dockerfile` yarating
5. `docker-compose.yml` da 2ta service qo'shing:
   - `api` (sizning Node.js app)
   - `postgres` (PostgreSQL database)

### Kutilayotgan natija:

- API 3000 portda ishlashi
- PostgreSQL 5432 portda ishlashi
- API database'ga ulanishi

---

## Mashq 3: Multi-service Blog Platform

**Maqsad:** Ko'p service'li ilovani boshqarish

### Vazifa:

1. 3ta service yarating:
   - Frontend (Nginx)
   - Backend (Node.js yoki Python)
   - Database (PostgreSQL)
2. Volume'lar bilan persistent data
3. Environment variable'lar

### Qadamlar:

1. Yangi papka: `mkdir blog-platform && cd blog-platform`
2. Har bir service uchun alohida papka:
   - `frontend/`
   - `backend/`
   - `database/`
3. `docker-compose.yml` da:
   - Barcha service'larni define qiling
   - Volume'lar qo'shing
   - Environment variable'lar o'rnating
   - Service'lar o'rtasida dependency o'rnating

### Kutilayotgan natija:

- Frontend: 80 port
- Backend: 5000 port
- Database: 5432 port
- Ma'lumotlar volume'da saqlanishi

---

## Mashq 4: Development vs Production

**Maqsad:** Turli environment'lar uchun configuration

### Vazifa:

1. Bitta loyiha uchun 2ta compose file:
   - `docker-compose.yml` (development)
   - `docker-compose.prod.yml` (production)
2. Development'da hot reload
3. Production'da optimized image

### Qadamlar:

1. Oldingi mashqlardan birini tanlang
2. `docker-compose.yml` - development uchun:
   - Volume mount qiling (kod o'zgarishini ko'rish uchun)
   - Development environment variable'lar
3. `docker-compose.prod.yml` - production uchun:
   - Optimized image
   - Production environment variable'lar
   - Resource limits

### Test qilish:

```bash
# Development
docker-compose up

# Production
docker-compose -f docker-compose.prod.yml up
```

### Kutilayotgan natija:

- Development'da kod o'zgarishi darhol ko'rinishi
- Production'da optimized va secure bo'lishi

---

### Debugging uchun:

```bash
# Service'lar holatini ko'rish
docker-compose ps

# Loglarni ko'rish
docker-compose logs service_name

# Container ichiga kirish
docker-compose exec service_name sh

# Service'ni qayta ishga tushirish
docker-compose restart service_name
```

### Tozalash:

```bash
# Container'lar va network'larni o'chirish
docker-compose down

# Volume'lar bilan birga o'chirish
docker-compose down -v

# Image'larni ham o'chirish
docker-compose down --rmi all
```

### Yaxshi practice'lar:

- Har doim `.gitignore` da `.env` file'ni ignore qiling
- Volume'lar uchun meaningful nomlar bering
- Health check'lar qo'shing
- Resource limits belgilang production'da

---
