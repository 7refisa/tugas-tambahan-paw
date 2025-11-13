# 04_Easier-Development-with-debugtoolbar

Di langkah ini menambahkan alat `pyramid_debugtoolbar` supaya debugging waktu pengembangan jadi lebih mudah.

Apa yang kita ubah:
- `setup.py`: ditambahkan `extras_require` bernama `dev` yang berisi `pyramid_debugtoolbar`.
- `development.ini`: menambahkan `pyramid.includes = pyramid_debugtoolbar` supaya Pyramid memuat konfigurasi toolbar otomatis.
- `requirements_clean.txt`: ditambahkan `pyramid_debugtoolbar` untuk memudahkan instalasi.
- `tutorial/__init__.py`: tetap berisi fungsi `main` yang mengembalikan objek WSGI.

Kenapa ini berguna:
- `pyramid_debugtoolbar` adalah paket Python yang dipasang lewat `pip`. Paket ini menambahkan sebuah toolbar di sisi browser yang membantu melihat informasi debugging (stack trace, variabel, setting, dsb.).
- Dengan meletakkan `pyramid_debugtoolbar` di `pyramid.includes` pada file `.ini`, kita bisa mengaktifkan atau menonaktifkannya tanpa mengubah kode, cukup ubah file `.ini`.
- `extras_require` di `setup.py` memberi cara mudah memasang dependensi khusus pengembangan (dev). 

Perintah instalnya seperti:
```powershell
python -m pip install -e ".[dev]"
```

Langkah singkat menjalankan (PowerShell):
```powershell
cd D:\Documents\05\PAW\tugas-tambahan-paw\04_Easier-Development-with-debugtoolbar
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements_clean.txt
# atau pakai extras dev
python -m pip install -e ".[dev]"
pserve development.ini --reload
```

Buka `http://localhost:6543/` lalu klik tombol toolbar di kanan untuk membuka alat debugging.

Catatan penting:
- Toolbar menambahkan sedikit HTML/CSS ke halaman (dekati `</body>`). Kalau ada masalah tampilan aneh, nonaktifkan toolbar dengan menghapus `pyramid_debugtoolbar` dari `pyramid.includes` di `.ini`.
- `extras_require` berguna supaya pengguna tidak perlu menginstall dependensi pengembangan, cukup menginstall paket utama.