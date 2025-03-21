# Proyek WordPress dengan Docker

## Deskripsi
Proyek ini merupakan setup WordPress menggunakan Docker yang terdiri dari tiga layanan utama:
- PHP & WordPress
- MySQL Database
- Redis Server

## Prasyarat
Sebelum memulai, pastikan sistem Anda telah memiliki:
- Docker
- Docker Compose
- Git (opsional)

## Struktur Proyek 
.
├── docker-compose.yml
├── Dockerfile
├── src/
│ └── wp-config.php
└── mysql_data/
├── src/
│ └── wp-config.php
└── mysql_data/

## Konfigurasi
### Detail Layanan

1. **PHP & WordPress**
   - Port: 8080
   - Volume: `./src:/var/www/html`

2. **MySQL**
   - Database: wordpress_db
   - Username: wordpress_user
   - Password: sandi_wordpress
   - Volume: `./mysql_data:/var/lib/mysql`

3. **Redis**
   - Menggunakan image Redis terbaru
   - Berjalan sebagai cache server

## Cara Penggunaan

### 1. Menjalankan Proyek
```bash
# Clone repositori (jika menggunakan git)
git clone https://www.github.com/javierfadel/wordpress-docker-practice.git

# Masuk ke direktori proyek
cd wordpress-docker-practice

# Menjalankan container
docker-compose up -d
```

### 2. Mengakses WordPress
- Buka browser dan kunjungi: `http://localhost:8080`
- Ikuti langkah-langkah instalasi WordPress

### 3. Mengakses Database
Anda dapat mengakses database menggunakan:

**Melalui Command Line:**
```bash
docker exec -it mysql_server mysql -u wordpress_user -p
```

**Melalui MySQL Client (seperti MySQL Workbench):**
- Host: 127.0.0.1
- Port: 3306
- Username: wordpress_user
- Password: sandi_wordpress
- Database: wordpress_db

### 4. Menghentikan Proyek
```bash
docker-compose down
```

## Perintah Docker yang Berguna

```bash
# Melihat status container
docker-compose ps

# Melihat log
docker-compose logs

# Menghapus semua container dan volume
docker-compose down -v

# Membangun ulang image
docker-compose build
```

## Backup dan Restore

### Backup Database
```bash
docker exec mysql_server mysqldump -u wordpress_user -p wordpress_db > backup.sql
```

### Restore Database
```bash
docker exec -i mysql_server mysql -u wordpress_user -p wordpress_db < backup.sql
```

## Troubleshooting

1. **Jika tidak bisa mengakses WordPress:**
   - Pastikan semua container berjalan: `docker-compose ps`
   - Periksa log: `docker-compose logs php`

2. **Jika database tidak tersambung:**
   - Pastikan konfigurasi di `wp-config.php` sesuai
   - Periksa log MySQL: `docker-compose logs mysql`

## Keamanan
- Ganti password default yang ada di `docker-compose.yml`
- Update `wp-config.php` dengan salt keys yang unik
- Aktifkan WP_DEBUG hanya saat development

## Kontribusi
Silakan berkontribusi dengan membuat pull request atau melaporkan issues.