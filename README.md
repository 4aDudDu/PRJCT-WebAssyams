# 🏫 Pondok As-Syams - SPMB Registration System

[![Laravel Version](https://img.shields.io/badge/Laravel-12.0-FF2D20?style=flat-square&logo=laravel)](https://laravel.com)
[![PHP Version](https://img.shields.io/badge/PHP-8.2+-777BB4?style=flat-square&logo=php)](https://php.net)
[![Filament](https://img.shields.io/badge/Filament-3.3-0F766E?style=flat-square)](https://filamentphp.com)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

Sistem pendaftaran SPMB (Seleksi Penerimaan Mahasiswa Baru) terintegrasi dengan admin panel modern menggunakan Laravel 12 & Filament, dilengkapi countdown deadline otomatis, dashboard interaktif, dan payment gateway Midtrans.

---

## ✨ Fitur Utama

### 📋 Untuk Calon Mahasiswa
- ✅ **Formulir SPMB** - Pendaftaran online yang user-friendly
- ⏱️ **Countdown Deadline** - Timer real-time sampai tutup pendaftaran
- 💳 **Payment Gateway** - Integrasi Midtrans untuk bayar registrasi
- 📊 **Status Tracking** - Lacak status pendaftaran calon
- 🎯 **Validasi Form** - Input validation real-time

### 🔧 Untuk Admin (Filament)
- 👥 **Dashboard Admin** - Statistik pendaftar, payment, dll
- ⚙️ **Pengaturan SPMB** - Menu untuk atur deadline countdown
- 📅 **Manajemen Deadline** - DateTimePicker user-friendly untuk set closing time
- 📨 **Data Pendaftar** - CRUD data calon mahasiswa
- 💰 **Payment Management** - Verifikasi & track pembayaran
- 📑 **Report & Export** - Generate laporan, export ke PDF/Excel
- 🔐 **User Management** - Kelola admin & permission

### 🎨 User Interface
- 🌙 **Dark & Light Mode** - Theme toggle
- 📱 **Responsive Design** - Mobile, tablet, desktop optimized
- ⚡ **Real-time Updates** - AlpineJS untuk countdown & live data
- 🎭 **Modern UI** - Tailwind CSS + Filament components

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Framework** | Laravel 12.0 |
| **Admin Panel** | Filament 3.3 |
| **Frontend** | HTML5, Tailwind CSS, AlpineJS, Vite |
| **Database** | MySQL / MariaDB |
| **Payment** | Midtrans API |
| **PDF Export** | DOMPDF |
| **PHP Version** | 8.2+ |

---

## 📋 Prerequisites

| Requirement | Versi | Keterangan |
|------------|-------|-----------|
| PHP | 8.2+ | Dengan ext: curl, mbstring, pdo_mysql, openssl |
| Composer | ^2.0 | PHP package manager |
| Node.js | 18+ | NPM untuk build frontend |
| MySQL | 5.7+ | Database engine |
| Git | Latest | Version control |

---

## 🚀 Quick Start

### 1. Clone Repository
```bash
git clone https://github.com/4aDudDu/PRJCT-WebAssyams.git
cd PRJCT-WebAssyams
```

### 2. Setup Environment
```bash
# Copy .env.example ke .env
cp .env.example .env

# Edit .env untuk:
# - DB_HOST, DB_DATABASE, DB_USERNAME, DB_PASSWORD
# - MIDTRANS_MERCHANT_ID, MIDTRANS_CLIENT_KEY, MIDTRANS_SERVER_KEY
# - APP_URL
```

### 3. Install Dependencies
```bash
# PHP dependencies
composer install

# JavaScript dependencies
npm install
```

### 4. Generate Key & Setup Database
```bash
# Generate app key
php artisan key:generate

# Run migrations & seeders
php artisan migrate --seed

# Build frontend assets
npm run build
```

### 5. Create Admin User
```bash
# Buat akun superadmin
php artisan tinker
>>> App\Models\User::create(['name' => 'Admin', 'email' => 'admin@example.com', 'password' => bcrypt('password'), 'is_admin' => true]);
>>> exit
```

### 6. Jalankan Server
```bash
# Terminal 1: PHP Server
php artisan serve

# Terminal 2: Queue (untuk email, etc)
php artisan queue:listen

# Terminal 3: Vite Dev Server (hot reload)
npm run dev
```

Buka browser: `http://localhost:8000`

---

## 📁 Struktur Folder

```
PRJCT-WebAssyams/
├── app/
│   ├── Filament/                    # Admin Panel (Filament)
│   │   ├── Resources/
│   │   │   ├── SiteSettingResource.php      # Pengaturan website
│   │   │   ├── PendaftarResource.php        # Manage calon mahasiswa
│   │   │   └── PaymentResource.php          # Manage pembayaran
│   │   └── Pages/                   # Custom pages
│   │       └── Dashboard.php        # Admin dashboard
│   ├── Models/
│   │   ├── Pendaftar.php           # Calon mahasiswa model
│   │   ├── Payment.php             # Transaksi pembayaran
│   │   ├── User.php                # Admin user
│   │   └── SiteSetting.php         # Konfigurasi website
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── HomeController.php           # Homepage
│   │   │   ├── PendaftaranController.php    # Form pendaftaran
│   │   │   └── PaymentController.php        # Payment callback
│   │   └── Middleware/
│   ├── Services/
│   │   └── MidtransService.php     # Payment gateway integration
│   └── Events/ & Jobs/
│
├── config/
│   ├── app.php                      # App config
│   ├── database.php                 # Database config
│   ├── midtrans.php                 # Payment gateway config
│   └── filament.php                 # Filament config
│
├── database/
│   ├── migrations/                  # Database schemas
│   │   ├── 2025_11_24_users_table.php
│   │   ├── 2025_11_24_pendaftars_table.php
│   │   ├── 2025_11_24_payments_table.php
│   │   └── 2025_11_24_site_settings_table.php
│   └── seeders/                     # Initial data
│
├── resources/
│   ├── views/
│   │   ├── layouts/                 # Main layout
│   │   ├── pages/
│   │   │   ├── home.blade.php       # Homepage (dengan countdown)
│   │   │   ├── daftar.blade.php     # Form pendaftaran
│   │   │   └── pembayaran.blade.php # Payment status
│   │   └── filament/                # Filament custom views
│   ├── css/
│   │   └── app.css                  # Main stylesheet
│   └── js/
│       ├── app.js                   # Main JS
│       └── countdown.js             # Timer countdown logic
│
├── routes/
│   ├── web.php                      # Web routes (public)
│   └── api.php                      # API routes (opsional)
│
├── storage/
│   ├── app/                         # File storage
│   └── logs/                        # Application logs
│
├── tests/                           # Unit & Feature tests
│
├── .env.example                     # Environment template
├── composer.json                    # PHP dependencies
├── package.json                     # Node dependencies
├── tailwind.config.js               # Tailwind configuration
├── vite.config.js                   # Vite configuration
├── artisan                          # Laravel CLI
│
└── PUBLIC DOCS/
    ├── START_HERE.txt               # Overview & getting started
    ├── QUICK_START_SPMB.md          # Admin quick guide (60 sec)
    ├── FINAL_REPORT.txt             # Complete technical report
    ├── PREVIEW_MENU_SPMB.html       # UI mockup preview
    └── quran_qb.sql                 # Sample database data
```

---

## 🔑 Environment Variables

Copy `.env.example` ke `.env` dan sesuaikan:

```bash
# App Configuration
APP_NAME="Pondok As-Syams SPMB"
APP_URL=http://localhost:8000
APP_ENV=local
APP_DEBUG=true

# Database
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=spmb_asyams
DB_USERNAME=root
DB_PASSWORD=

# Midtrans Payment Gateway
MIDTRANS_MERCHANT_ID=your_merchant_id
MIDTRANS_CLIENT_KEY=your_client_key
MIDTRANS_SERVER_KEY=your_server_key
MIDTRANS_IS_PRODUCTION=false

# Mail Configuration (optional)
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=587
MAIL_USERNAME=your_username
MAIL_PASSWORD=your_password
```

---

## 📊 Database Schema

### Tabel Utama

#### `users` - Admin & Staff
```sql
- id
- name, email, password
- is_admin, role (superadmin, admin, staff)
- created_at, updated_at
```

#### `pendaftars` - Calon Mahasiswa
```sql
- id
- nama, email, telepon, no_identitas
- alamat, kota, provinsi
- tahun_lulus
- pilihan_program (1st choice, 2nd choice)
- status (draft, submitted, verified, approved, rejected)
- payment_status (unpaid, pending, paid)
- created_at, updated_at
```

#### `payments` - Transaksi Pembayaran
```sql
- id
- pendaftar_id (FK)
- amount, payment_method
- transaction_id (dari Midtrans)
- status (pending, success, failed)
- paid_at
- created_at, updated_at
```

#### `site_settings` - Konfigurasi Website
```sql
- id
- key (unique) - 'spmb_deadline', 'spmb_open', etc
- value - format: Y-m-d H:i:s
- created_at, updated_at
```

---

## 🔧 Fitur Countdown SPMB

### Cara Atur Deadline

1. **Login ke Filament Admin**
   ```
   URL: http://localhost:8000/admin
   ```

2. **Navigasi ke Pengaturan**
   ```
   Sidebar → Pengaturan → Setting Website
   ```

3. **Klik Tombol Hijau**
   ```
   Cari tombol "⏱️ Atur Deadline SPMB"
   ```

4. **Isi Form**
   ```
   Pilih tanggal & jam → Simpan
   Format: Y-m-d H:i:s (contoh: 2026-12-31 23:59:00)
   ```

5. **Countdown Otomatis Update**
   ```
   Halaman home → Section countdown update real-time
   ```

### Tampilan di Homepage
```
┌─────────────────────────────────────┐
│  SPMB Akan Berakhir Pada:           │
│  Batas Akhir: Kamis, 31 Desember... │
│             23:59 WIB               │
│                                     │
│  100 : 05 : 30 : 45                 │
│  Hari  Jam  Menit  Detik            │
└─────────────────────────────────────┘
```

---

## 💳 Midtrans Payment Integration

### Setup Midtrans

1. **Daftar di Midtrans**
   - Buka [midtrans.com](https://midtrans.com)
   - Buat akun merchant

2. **Dapatkan Credentials**
   - Login → Settings → Merchant Info
   - Copy `Merchant ID`, `Client Key`, `Server Key`

3. **Update .env**
   ```bash
   MIDTRANS_MERCHANT_ID=your_merchant_id
   MIDTRANS_CLIENT_KEY=your_client_key
   MIDTRANS_SERVER_KEY=your_server_key
   MIDTRANS_IS_PRODUCTION=false  # Set true untuk production
   ```

4. **Payment Flow**
   ```
   Calon Klik "Bayar" 
      ↓
   Redirect ke Midtrans Payment Page
      ↓
   Calon Input Kartu / E-wallet
      ↓
   Midtrans Process & Callback
      ↓
   Update Status di Database
      ↓
   Redirect kembali ke website
   ```

---

## 📖 Dokumentasi Lengkap

Baca file dokumentasi di root folder:

| File | Untuk | Waktu |
|------|-------|-------|
| `START_HERE.txt` | Overview & getting started | 5 min |
| `QUICK_START_SPMB.md` | Admin quick guide | 2 min |
| `FINAL_REPORT.txt` | Technical report lengkap | 10 min |
| `PREVIEW_MENU_SPMB.html` | Visual UI preview | View di browser |

---

## 🧪 Testing

### Run Unit Tests
```bash
php artisan test
```

### Run Feature Tests
```bash
php artisan test --filter=Feature
```

### Testing Checklist
Lihat `CHECKLIST_VERIFIKASI.md` untuk manual testing steps.

---

## 🐛 Troubleshooting

### Error: "Database connection refused"
```bash
# Pastikan MySQL running
mysql -u root -p

# Check .env database config
# Coba reset: php artisan migrate:fresh --seed
```

### Error: "Class not found" (Filament)
```bash
php artisan filament:cache-components
php artisan cache:clear
php artisan view:clear
```

### Countdown tidak update
```bash
# Clear cache & rebuild
php artisan cache:clear
npm run build

# Refresh browser: Ctrl+Shift+R (hard refresh)
```

### Payment callback error
```bash
# Check logs
tail -f storage/logs/laravel.log

# Verify Midtrans credentials di .env
# Test dengan Midtrans Sandbox mode dulu
```

---

## 📦 Available Commands

```bash
# Laravel Commands
php artisan serve                    # Start development server
php artisan migrate                  # Run migrations
php artisan migrate:fresh --seed     # Reset & seed database
php artisan tinker                   # Interactive shell
php artisan queue:listen             # Listen queue jobs

# Filament Commands
php artisan filament:cache-components
php artisan filament:upgrade

# NPM Commands
npm run dev                          # Vite dev server (hot reload)
npm run build                        # Build for production
npm run lint                         # Run linter

# Cache Commands
php artisan cache:clear
php artisan view:clear
php artisan config:clear
```

---

## 🔐 Security

✅ **Best Practices:**
- CSRF protection on all forms
- Input validation & sanitization
- SQL injection prevention (Eloquent ORM)
- Password hashing (bcrypt)
- Role-based access control (Filament)
- XSS protection
- HTTPS recommended for production

⚠️ **Setup Checklist:**
- [ ] Change default admin password
- [ ] Set `APP_DEBUG=false` di production
- [ ] Use strong `APP_KEY`
- [ ] Setup HTTPS (SSL certificate)
- [ ] Enable .env in .gitignore
- [ ] Regular database backups
- [ ] Monitor error logs

---

## 🚀 Deployment

### Production Setup
```bash
# 1. Clone repository
git clone ...
cd PRJCT-WebAssyams

# 2. Setup environment
cp .env.example .env
# Edit .env untuk production settings

# 3. Install dependencies
composer install --no-dev
npm ci
npm run build

# 4. Setup database
php artisan migrate --force

# 5. Optimize for production
php artisan config:cache
php artisan route:cache
php artisan view:cache

# 6. Setup queue worker (background jobs)
# Gunakan supervisor atau systemd
```

### Server Requirements (Shared Hosting)
- PHP 8.2+ dengan ext curl, mbstring, pdo_mysql, openssl
- MySQL 5.7+
- Min 512MB RAM
- Disk space: 500MB+

### Server Setup (VPS/Dedicated)
Lihat deployment guide di `docs/deployment.md` (if exists)

---

## 📞 Support & Contact

- 🐛 **Issues**: Buka issue di repository
- 💬 **Discussions**: Tanya di GitHub discussions
- 📧 **Email**: Hubungi developer

---

## 📄 License

Project ini open-source dan dilisensikan di bawah **MIT License** — silakan gunakan, modifikasi, dan distribusikan sesuai kebutuhan.

---

## 🙏 Credits

**Dikembangkan untuk:** Pondok Pesantren As-Syams  
**Framework:** Laravel 12, Filament 3.3  
**Payment Gateway:** Midtrans  
**Frontend:** Tailwind CSS, AlpineJS  

---

## 📊 Project Status

| Aspek | Status |
|-------|--------|
| Development | ✅ Complete |
| Documentation | ✅ Complete |
| Testing | ✅ Ready |
| Production | ⏳ Awaiting deployment |

---

## 🎯 Roadmap

- [ ] SMS notification untuk pengumuman
- [ ] Email auto-reply untuk pendaftar
- [ ] Cetak kartu peserta PDF
- [ ] Dashboard analytics advanced
- [ ] Multi-language support
- [ ] API untuk mobile app
- [ ] Two-Factor Authentication (2FA)

---

**Version:** 1.0.0  
**Last Updated:** 27 April 2026  
**Status:** 🟢 Ready for Production
