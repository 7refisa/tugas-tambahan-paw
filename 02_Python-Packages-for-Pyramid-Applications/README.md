# 02_Python-Packages-for-Pyramid-Applications

Nama: Refi Ikhsanti  
NIM: 123140126

Di tugas ini membuat aplikasi "Hello World" sebagai paket Python di dalam sebuah proyek kecil. Tujuan utamanya supaya belajar cara membuat paket dan bagaimana menginstallnya di mode development (editable).

Struktur yang dibuat:
- `setup.py` : berisi instruksi supaya project bisa diinstall menggunakan `pip install -e .`.
- `tutorial/` : direktori paket Python.
  - `__init__.py` : file kosong (atau berisi komentar) yang menandakan folder ini adalah paket Python.
  - `app.py` : file aplikasi yang sama seperti contoh single-file, tapi sekarang berada dalam paket.
- `requirements_clean.txt` : daftar paket yang diperlukan (`pyramid`, `waitress`) untuk dipasang dengan `pip`.

Langkah singkat (PowerShell):
1. Masuk ke folder proyek:
```powershell
cd D:\Documents\05\PAW\tugas-tambahan-paw\02_Python-Packages-for-Pyramid-Applications
```

2. Buat virtual environment dan aktifkan:
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

3. Pasang paket-paket dasar (opsi A: dari file helper):
```powershell
python -m pip install -r requirements_clean.txt
```

atau (opsi B: langsung install editable project):
```powershell
python -m pip install -e .
```

4. Jalankan aplikasi dari dalam paket:
```powershell
python tutorial/app.py
```

Buka `http://localhost:6543/` di browser untuk melihat hasil.

Penjelasan singkat yang penting:
- `setup.py` memberikan informasi kepada `pip`/`setuptools` bagaimana menginstall project. Di sini hanya memakai `install_requires` untuk memberitahu dependensi.
- `pip install -e .` (editable install) membuat paket bisa diimpor dari lingkungan Python tanpa perlu di-copy tiap kali ada perubahan. Berguna saat sedang mengembangkan.
- `__init__.py` diperlukan supaya Python mengenali folder `tutorial` sebagai paket.
- Menjalankan `python tutorial/app.py` tetap mungkin, tapi biasanya bukan cara terbaik untuk produksi. Ini dipakai di tutorial agar langkah-langkahnya mudah dimengerti.

Kenapa ini berguna untuk belajar:
- Belajar struktur dasar paket Python.
- Melihat bagaimana `setup.py` dan `pip` bekerja untuk mengelola dependensi dan instalasi lokal.

Langkah lanjutan (opsional):
- Buat `console_scripts` di `setup.py` supaya bisa menjalankan server dengan perintah yang lebih singkat.