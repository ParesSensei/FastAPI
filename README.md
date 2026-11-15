# FastAPI Project

Proyek ini adalah API yang dibuat menggunakan FastAPI, framework web modern berbasis Python yang cepat dan mudah digunakan.

## Teknologi yang Digunakan

Proyek ini menggunakan stack teknologi berikut:

- **Backend:** Python dengan FastAPI
- **Database:** SQLite3
- **ORM:** SQLAlchemy
- **Autentikasi:** JWT, Pydantic, dan hashing password dengan bcrypt

## Instalasi

### Persyaratan

Pastikan Anda memiliki Python versi 3.8 atau lebih baru dan Docker terinstal jika ingin menjalankan aplikasi dengan container.

### 1. Clone Repository

```bash
git clone https://github.com/ParesSensei/FastAPI.git
cd FastAPI
```

### 2. Buat Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # Untuk Linux/Mac
venv\Scripts\activate     # Untuk Windows
```

### 3. Install Dependensi

```bash
pip install -r requirements.txt
```

## Menjalankan Aplikasi

### Dengan Uvicorn (tanpa Docker)

```bash
uvicorn main:app --reload
```

Aplikasi akan berjalan di `http://127.0.0.1:8000/`

Saat pertama kali dijalankan, file database `todosapp.db` akan dibuat otomatis
lewat `models.Base.metadata.create_all()` di `main.py`, jadi tidak perlu migrasi
manual untuk sekadar mencoba aplikasinya.

## Autentikasi

Sebelum memakai endpoint todos atau admin, buat user dulu lewat `POST /auth/`,
lalu tukar username dan password menjadi token di `POST /auth/token`.

```bash
# 1. Daftarkan user baru
curl -X POST http://127.0.0.1:8000/auth/ \
  -H "Content-Type: application/json" \
  -d '{
    "username": "hayyan",
    "email": "hayyan@example.com",
    "first_name": "Hayyan",
    "last_name": "Dev",
    "password": "rahasia123",
    "role": "admin"
  }'

# 2. Ambil access token (form-data, sesuai standar OAuth2 password flow)
curl -X POST http://127.0.0.1:8000/auth/token \
  -d "username=hayyan&password=rahasia123"
```

Simpan `access_token` dari responsnya, lalu kirim sebagai header
`Authorization: Bearer <token>` pada request berikutnya.

## Dokumentasi API

Setelah aplikasi berjalan, Anda dapat mengakses dokumentasi interaktif dengan mengunjungi salah satu dari:

- Swagger UI: `http://127.0.0.1:8000/docs`
- Redoc: `http://127.0.0.1:8000/redoc`

## Struktur Proyek

```
FastAPI/
├── main.py             # File utama aplikasi
├── database.py         # Konfigurasi engine dan session SQLAlchemy
├── models.py           # Model database (Users dan Todos)
├── routers/            # Kumpulan route API
│   ├── auth.py         # Registrasi user dan penerbitan token JWT
│   ├── todos.py        # CRUD todo milik user
│   └── admin.py        # Endpoint khusus role admin
├── requirements.txt    # Dependensi proyek
├── todosapp.db         # Database SQLite (dibuat otomatis saat pertama jalan)
└── README.md           # Dokumentasi proyek
```

## Database Implementation

Proyek ini menggunakan SQLite3 sebagai database utama. Struktur tabel utama adalah sebagai berikut:

- User Table:
  - id: ID unik pengguna
  - username: Nama pengguna unik
  - first_name: nama depan
  - last_name: nama belakang
  - email: Email unik
  - is_active: Di set default ke True
  - role: role pengguna
  - hashed_password: Password yang telah dienkripsi

- Todo Table:
  - id: ID unik todo
  - title: Judul todo
  - description: Deskripsi todo
  - priority: Prioritas todo (1-5)
  - complete: Status penyelesaian, default False
  - owner_id: Foreign key ke tabel users

## Autentikasi

Proyek ini menggunakan JWT untuk autentikasi dan bcrypt untuk hashing password serta Pydantic untuk validasi request. Implementasi ini memastikan keamanan dalam penyimpanan dan verifikasi kredensial pengguna.

## Lisensi

Proyek ini menggunakan lisensi [MIT](LICENSE).