# 06_Functional-Testing-with-WebTest

Di langkah ini menambahkan pengujian fungsional (end-to-end) menggunakan `webtest`. Tes fungsional memastikan respon HTML yang dihasilkan aplikasi sesuai harapan.

File yang dibuat:
- `setup.py` : menambahkan `webtest` ke `dev` extras.
- `tutorial/__init__.py` : fungsi `main` dan view `hello_world` (WSGI app).
- `tutorial/tests.py` : berisi tes unit (DummyRequest) dan tes fungsional (TestApp dari WebTest).
- `requirements.txt` : daftar paket yang diperlukan.

Menjalankan tes (PowerShell):
```powershell
cd D:\Documents\05\PAW\tugas-tambahan-paw\06_Functional-Testing-with-WebTest
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
pytest tutorial/tests.py -q
```

Penjelasan singkat:
- Tes fungsional membuat aplikasi WSGI menggunakan fungsi `main()` lalu membungkusnya dengan `webtest.TestApp`. `TestApp` mensimulasikan request HTTP ke aplikasi tanpa perlu menjalankan server sungguhan.
- `self.testapp.get('/', status=200)` melakukan GET ke `/` dan memverifikasi status kode. `res.body` berisi bytes respons; kita cek apakah ada `<h1>Hello World!</h1>` di dalamnya.

Manfaat:
- Tes fungsional memberi jaminan bahwa seluruh stack (routing, view, rendering) bekerja bersama.
- Tes cepat, cocok dipakai di siklus pengembangan.