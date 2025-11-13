# 01_Single-File-Web-Applications

Nama: Refi Ikhsanti  
NIM: 123140126

Isi folder:
- `app.py`: kode aplikasi Pyramid satu berkas yang menyediakan satu rute `/`.
- `requirements_clean.txt`: daftar paket yang harus diinstall (`pyramid` dan `waitress`).

Langkah menjalankan:
1. Buat lingkungan virtual (virtual environment) dan aktifkan:
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Pasang paket yang dibutuhkan:
```powershell
python -m pip install -r requirements.txt
```

3. Jalankan aplikasi:
```powershell
python app.py
```

4. Buka browser dan kunjungi `http://localhost:6543/`.
Penjelasan singkat bagian penting di `app.py`:
- `if __name__ == '__main__':`

  - Bagian ini hanya dijalankan kalau file `app.py` dieksekusi langsung dengan `python app.py`.

- `with Configurator() as config:`

  - `Configurator` dipakai untuk menghubungkan URL (route) dengan fungsi yang akan dipanggil. Cara ini membuat kode lebih rapi.

- `config.add_route('hello', '/')` dan `config.add_view(hello_world, route_name='hello')`

  - Artinya: kalau ada permintaan ke alamat `/`, maka jalankan fungsi `hello_world`.

- `app = config.make_wsgi_app()`

  - Membuat objek aplikasi WSGI yang bisa dilayani oleh server (misal `waitress`).

- `serve(app, host='0.0.0.0', port=6543)`

  - Jalankan server yang mendengarkan permintaan di port 6543.

- `def hello_world(request):`
  - Fungsi ini menerima objek `request` (isi permintaan dari browser) dan mengembalikan `Response` yang berisi HTML.

Pertanyaan tambahan:
- Mengapa `print('Incoming request')` bukan `print 'Incoming request'`?

  - Karena kita pakai Python 3. Di Python 3, `print` harus pakai tanda kurung. Bentuk tanpa tanda kurung adalah sintaks Python 2 dan tidak berlaku di Python 3.

- Jika view mengembalikan string HTML, atau mengembalikan daftar angka, apa yang terjadi?

  - Mengembalikan objek `Response` adalah cara yang jelas dan aman. Kadang Pyramid menerima string sebagai badan respon, tapi lebih baik pakai `Response`. Kalau mengembalikan daftar angka, server akan error karena WSGI mengharapkan byte/byte-string, bukan angka.

- Kalau kita tulis kode salah (mis. `print xyz`) lalu jalankan ulang, apa yang terjadi?

  - Server akan menampilkan error di konsol (mis. NameError) dan browser akan mendapat respon error (500). Perbaiki kodenya dan jalankan lagi.

- Apa itu WSGI dan darimana idenya?

  - WSGI singkatan dari Web Server Gateway Interface. Ide WSGI terinspirasi dari CGI (Common Gateway Interface), tapi WSGI lebih modern dan lebih efisien.

Catatan singkat:

- File `requirements_clean.txt` dibuat supaya lebih mudah dipakai saat `pip install -r`.
- Kalau mau pengembangan lebih nyaman, bisa pakai alat auto-reload agar server restart otomatis saat kode berubah.
