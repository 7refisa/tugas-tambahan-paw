# 03_Application-Configuration-with-.ini-Files

Di langkah ini belajar cara menjalankan aplikasi Pyramid memakai file konfigurasi `.ini` dan perintah `pserve`. Keuntungan memakai `.ini` adalah konfigurasi terpisah dari kode: lebih mudah diatur, dan dapat mengatur server, logging, dan opsi lain tanpa ubah kode.

File penting yang dibuat:
- `setup.py` : sekarang punya `entry_points` yang memberitahu Pyramid di mana fungsi `main` berada (`tutorial:main`).
- `development.ini` : file konfigurasi yang dipakai `pserve` untuk mem-boot aplikasi dan mengatur server.
- `tutorial/__init__.py` : sekarang berisi fungsi `main(global_config, **settings)` yang mengembalikan aplikasi WSGI.

Langkah singkat (PowerShell):
1. Masuk ke folder proyek:
```powershell
cd D:\Documents\05\PAW\tugas-tambahan-paw\03_Application-Configuration-with-.ini-Files
```

2. Buat virtualenv dan aktifkan:
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

3. Pasang paket yang diperlukan atau install project editable:
```powershell
python -m pip install -r requirements_clean.txt
# atau
python -m pip install -e .
```

4. Jalankan aplikasi dengan `pserve` dan opsi reload:
```powershell
pserve development.ini --reload
```

5. Buka `http://localhost:6543/` di browser.

Penjelasan singkat:
- `entry_points` di `setup.py` mengatakan: "kalau Pyramid minta app bernama `main`, panggil fungsi `main` di paket `tutorial`." Dengan begitu `pserve` tahu cara memanggil aplikasi.
- `development.ini` punya dua bagian utama: `[app:main]` (pakai egg:tutorial) dan `[server:main]` (pakai egg:waitress#main dan dengarkan di localhost:6543).
- Fungsi `main(global_config, **settings)` menerima konfigurasi dari `.ini`. Parameter `**settings` berguna kalau ada opsi tambahan di file `.ini` yang ingin di pakai di kode.

Jawaban Extra Credit:
- Bisa kita tulis konfigurasi sendiri tanpa `.ini`? Ya. Kita bisa menulis script Python yang memanggil `tutorial.main()` langsung dan menjalankan server. `.ini` hanya membantu memisahkan konfigurasi dan memudahkan integrasi dengan `pserve`.
- Bisa punya banyak file `.ini`? Ya. Contohnya `development.ini`, `production.ini`, `testing.ini`. Ini berguna untuk konfigurasi yang berbeda (port, logging, database, dsb.) pada tiap lingkungan.
- Kenapa `entry_point` tidak menyebut `__init__.py` saat menulis `tutorial:main`? Karena paket Python `tutorial` sudah diwakili oleh modul `tutorial` (yang mengacu pada `tutorial/__init__.py`). Menulis `tutorial:main` berarti "ambil objek `main` dari modul `tutorial`".
- Apa arti `**settings`? `**` adalah sintaks Python untuk menerima sejumlah argumen kata kunci (keyword arguments) dalam bentuk dictionary. `settings` akan berisi pasangan kunci-nilai dari konfigurasi `.ini` yang relevan.