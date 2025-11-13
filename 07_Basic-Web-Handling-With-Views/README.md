# 07_Basic-Web-Handling-With-Views

Di langkah ini memindahkan kode view ke modul terpisah `views.py` dan menggunakan decorator `@view_config` supaya konfigurasi view ditulis secara deklaratif.

Hal yang diubah:
- `tutorial/__init__.py` sekarang hanya membuat rute dan memerintahkan Pyramid untuk memindai modul `views`.
- `tutorial/views.py` berisi dua view: `home` (pada `/`) dan `hello` (pada `/howdy`). Keduanya memakai `@view_config(route_name=...)`.
- `tutorial/tests.py` diperbarui untuk menguji fungsi view langsung (unit test) dan juga melakukan pengujian fungsional via `webtest.TestApp`.

Kenapa ini lebih baik untuk proyek nyata:
- Memisahkan views membuat kode lebih terorganisir.
- `config.scan('.views')` membaca decorator `@view_config` dan otomatis mendaftarkan view ke konfigurasi Pyramid.
- Dekorator (`@view_config`) adalah cara deklaratif: kamu meletakkan konfigurasi di dekat fungsi yang relevan, sehingga mudah dibaca.

Cara menjalankan tes dan aplikasi (PowerShell):
```powershell
cd D:\Documents\05\PAW\tugas-tambahan-paw\07_Basic-Web-Handling-With-Views
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
pytest tutorial/tests.py -q
# atau jalankan aplikasi:
pserve development.ini --reload
```

Buka `http://localhost:6543/` (lihat link ke `/howdy`) dan `http://localhost:6543/howdy`.