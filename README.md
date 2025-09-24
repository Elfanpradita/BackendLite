# **Panduan Instalasi Proyek Pemrograman Web (PemWeb)** 🚀

Panduan ini menjelaskan langkah-langkah untuk melakukan setup awal proyek Pemrograman Web menggunakan Docker dan Laravel Starter Kit.

---

## **1. Prasyarat**

Pastikan **Docker** dan **Docker Compose** sudah terinstal dan berjalan di sistem Anda.

---

## **2. Langkah-langkah Instalasi**

### **Langkah 1: Masuk ke Docker Container**

Buka terminal Anda dan jalankan perintah berikut untuk masuk ke dalam *shell* dari container Docker aplikasi.

```bash
docker exec -it pemweb bash
```

### **Langkah 2: Instalasi Laravel Starter Kit**

Instalasi ini menggunakan Composer. Proses ini akan mengunduh semua dependensi yang dibutuhkan.

⚠️ **Penting:** Perintah ini akan menginstall composer, tidak perlu lakukan perindah dibawahnya, skip langkah 2 dan langsung ke langkah 3.

```bash
composer install
```

⚠️ **Penting:** Jika direktori kerja Anda (`/var/www/html`) sudah berisi file, hapus terlebih dahulu dengan perintah di bawah ini. Lakukan dengan hati-hati.

```bash
# Hapus semua file yang ada (jika perlu)
rm -rf *
rm -rf .*
```

Setelah direktori bersih, jalankan perintah instalasi:

```bash
# Instalasi Laravel Starter Kit
composer create-project --prefer-dist raugadh/fila-starter .
```

### **Langkah 3: Atur Izin Akses Folder**

Sesuaikan kepemilikan dan izin akses pada folder `storage` dan `bootstrap` agar server web dapat menulis file *cache* dan *log*.

```bash
# Mengubah kepemilikan folder
chown -R www-data:www-data storage/*

#ini juga
chmod 777 -R storage/*

#ini juga
chmod 777 bootstrap/*
```

### **Langkah 4: Konfigurasi Environment (`.env`)**

Buat atau edit file `.env` di root proyek Anda. File ini berisi semua konfigurasi penting untuk aplikasi, seperti koneksi database dan URL aplikasi.

```env
APP_NAME="PemWeb"
APP_TIMEZONE='Asia/Jakarta'
APP_URL=http://localhost
ASSET_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=db_pemweb
DB_PORT=3306
DB_DATABASE=db_pemweb
DB_USERNAME=root
DB_PASSWORD=p455w0rd
```

### **Langkah 5: Inisialisasi Aplikasi**

Setelah konfigurasi `.env` selesai, jalankan perintah-perintah Artisan berikut secara berurutan untuk menyelesaikan instalasi.

```bash
# Generate kunci aplikasi
php artisan key:generate

# Jalankan migrasi untuk membuat tabel di database
php artisan migrate

# Generate role & permission default dari Filament Shield
php artisan shield:generate --all

# Jalankan seeder custom untuk inisialisasi data awal
php artisan project:init
```

---

## **3. Akses Aplikasi**

Setelah semua langkah selesai, aplikasi siap diakses melalui browser.

-   **URL**: Buka `http://localhost`
-   **Login Admin**:
    -   **Email**: `admin@admin.com`
    -   **Password**: `password`

---

## **4. Perintah Tambahan yang Berguna** 🛠️

Berikut adalah beberapa perintah Artisan yang mungkin Anda butuhkan selama pengembangan.

### **Membuat Komponen**

-   **Membuat komponen Livewire baru:**
    ```bash
    php artisan make:livewire NamaKomponen
    ```
-   **Membuat Model, Migration, dan Seeder sekaligus:**
    ```bash
    php artisan make:model NamaModel -ms
    ```
-   **Membuat Filament Resource untuk sebuah Model:**
    ```bash
    php artisan make:filament-resource NamaModel --generate
    ```

### **Manajemen Database**

-   **Reset dan jalankan ulang semua migrasi database:**
    ```bash
    php artisan migrate:fresh
    ```
-   **Jalankan semua seeder untuk mengisi data awal:**
    ```bash
    php artisan db:seed --force
    ```
