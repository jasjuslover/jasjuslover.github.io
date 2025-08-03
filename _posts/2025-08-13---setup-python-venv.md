`venv` (virtual environment) adalah alat di Python yang digunakan untuk membuat lingkungan terisolasi bagi proyek Python Anda. Tujuannya adalah untuk memisahkan dependensi proyek yang berbeda, sehingga setiap proyek dapat memiliki versi paket dan library yang berbeda tanpa saling memengaruhi. Dengan menggunakan `venv`, Anda dapat menjaga proyek Anda tetap terorganisir dan memastikan bahwa versi paket yang digunakan sesuai dengan kebutuhan proyek tanpa mengganggu pengaturan global Python di sistem.

Virtual environment sangat berguna ketika bekerja dengan beberapa proyek Python di satu mesin, karena setiap proyek bisa memiliki dependensi yang berbeda. Selain itu, `venv` memungkinkan Anda untuk menghindari konflik antara versi paket yang berbeda, mengurangi kemungkinan masalah saat menjalankan proyek yang menggunakan versi library yang lebih lama atau lebih baru.

Untuk memulai proyek Python menggunakan `venv` (virtual environment), ikuti langkah-langkah berikut:

1. **Buka terminal atau command prompt**.

2. **Buat folder proyek**:
   Jika belum memiliki folder proyek, buat folder baru dengan perintah:

   ```bash
   mkdir nama_proyek
   cd nama_proyek
   ```

3. **Buat virtual environment**:
   Jalankan perintah berikut untuk membuat virtual environment di dalam folder proyek:

   ```bash
   python -m venv venv
   ```

   Perintah ini akan membuat folder `venv` yang berisi virtual environment.

4. **Aktifkan virtual environment**:

   * **Untuk Windows**:

     ```bash
     .\venv\Scripts\activate
     ```
   * **Untuk macOS/Linux**:

     ```bash
     source venv/bin/activate
     ```

   Setelah mengaktifkan virtual environment, Anda akan melihat `(venv)` muncul di awal prompt terminal, yang menunjukkan bahwa virtual environment telah aktif.

**Catatan untuk Pengguna Fish**:
Jika Anda menggunakan shell Fish, cara untuk mengaktifkan virtual environment sedikit berbeda. Alih-alih menggunakan perintah `source`, Anda perlu menggunakan perintah berikut:

```bash
. venv/bin/activate.fish
```

Ini akan mengaktifkan virtual environment pada shell Fish Anda. Pastikan untuk menggunakan file `.fish` yang benar, karena shell Fish tidak kompatibel langsung dengan perintah `source` yang digunakan di shell lainnya seperti Bash.


6. **Instal dependensi (jika diperlukan)**:
   Setelah virtual environment aktif, Anda bisa menginstal paket atau library yang dibutuhkan menggunakan `pip`. Misalnya, untuk menginstal `requests`:

   ```bash
   pip install requests
   ```

7. **Buat file `requirements.txt` (Opsional)**:
   Untuk mencatat semua dependensi yang diinstal, Anda bisa membuat file `requirements.txt` dengan perintah:

   ```bash
   pip freeze > requirements.txt
   ```

8. **Menonaktifkan virtual environment**:
   Untuk keluar dari virtual environment, cukup jalankan perintah:

   ```bash
   deactivate
   ```

Itu saja! Anda sekarang siap untuk mulai mengembangkan proyek Python Anda dengan virtual environment.
