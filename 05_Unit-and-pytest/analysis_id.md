# 05_Unit-and-pytest

Di langkah ini menambahkan pengujian unit sederhana menggunakan `pytest`.  
Tujuan: memastikan fungsi `hello_world` bekerja seperti diharapkan.

File yang dibuat:
- `setup.py` : menambahkan `pytest` ke `extras_require` di `dev`.
- `tutorial/tests.py` : file tes yang memanggil `hello_world` dengan `DummyRequest`.
- `requirements_clean.txt` : daftar paket yang diperlukan untuk menjalankan tes.

Menjalankan tes (PowerShell):
1. Buat dan aktifkan virtualenv:
```powershell
cd D:\Documents\05\PAW\tugas-tambahan-paw\05_Unit-Tests-and-pytest
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Pasang dependensi (termasuk dev extras):
```powershell
python -m pip install -r requirements_clean.txt
# atau
python -m pip install -e ".[dev]"
```

3. Jalankan pytest pada file tes:
```powershell
pytest tutorial/tests.py -q
```

Output seperti `.` dan `1 passed` kalau tes berhasil.

Catatan singkat tentang tes yang dibuat:
- Tes memakai `pyramid.testing.DummyRequest` untuk membuat request palsu.
- Kita memanggil `hello_world(request)` dan mengecek `response.status_code` supaya sama dengan 200.
- `testing.setUp()` dan `testing.tearDown()` berguna kalau tes butuh konfigurasi Pyramid (mis. menambahkan route atau setting), tapi contoh sederhana ini tidak perlu banyak konfigurasi.