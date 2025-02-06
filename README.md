# FastAPI Project

Proyek ini adalah API yang dibuat menggunakan FastAPI, framework web modern berbasis Python yang cepat dan mudah digunakan.

## Teknologi yang Digunakan

Proyek ini menggunakan stack teknologi berikut:

- **Backend:** Python dengan FastAPI
- **Database:** Sqlite3
- **ORM:** SQLAlchemy
- **Autentikasi:** JWT, pydantic dan hashing password dengan bcrypt



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

###

# Dokumentasi API

Setelah aplikasi berjalan, Anda dapat mengakses dokumentasi interaktif dengan mengunjungi salah satu dari:

- Swagger UI: `http://127.0.0.1:8000/docs`
- Redoc: `http://127.0.0.1:8000/redoc`

# Struktur Proyek

```
FastAPI/
│── app/
│   ├── main.py        # File utama aplikasi
│   ├── routers/       # Folder untuk route API
│   ├── models/        # Folder untuk model database
│   ├── schemas/       # Folder untuk skema data
│   ├── config.py      # Konfigurasi aplikasi
│── tests/             # Folder untuk unit test
│── requirements.txt   # Dependensi proyek
│── README.md          # Dokumentasi proyek
```

# Database Implementation

Proyek ini menggunakan Sqlite3 sebagai database utama. Struktur tabel utama adalah sebagai berikut:

- User Table:
  - id: ID unik pengguna
  - username: Nama pengguna unik
  - first_name: nama depan
  - last_name: nama belakang
  - email: Email unik
  - is_active: Di set default ke True
  - role: role pengguna
  - hashed_password: Password yang telah dienkripsi



hashed_password: Password yang telah dienkripsiAutentikasi

Proyek ini menggunakan JWT untuk autentikasi dan bcrypt untuk hashing password serta pydantic untuk validasi request post. Implementasi ini memastikan keamanan dalam penyimpanan dan verifikasi kredensial pengguna.


##

## Lisensi

Proyek ini menggunakan lisensi [MIT](LICENSE).

