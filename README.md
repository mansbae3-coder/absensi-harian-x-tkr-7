# Absensi Harian X TKR 7 — Android MVP

Aplikasi Android native menggunakan Kotlin + Jetpack Compose, Firebase Authentication, Firestore online, QR Code generator, dan Google Code Scanner.

## Fitur
- Login/daftar akun guru.
- Kelas ditetapkan ke `X TKR 7`.
- Input siswa satu per satu dengan NIS dan nama.
- QR unik dibuat berdasarkan NIS.
- Guru scan QR kartu siswa; kehadiran dicatat otomatis sebagai Hadir.
- Status dapat diperbaiki manual menjadi Hadir, Izin, Sakit, atau Alpa.
- Rekap harian, hitungan status, dan bagikan CSV.
- Data per akun guru dipisahkan di Firestore.

## Menyiapkan proyek
1. Buka folder ini melalui Android Studio versi stabil yang mendukung Android Gradle Plugin 8.7.x.
2. Buat proyek di https://console.firebase.google.com/.
3. Tambahkan aplikasi Android dengan package name: `com.example.absenxtkr7`.
4. Unduh `google-services.json` dan simpan di folder `app/`.
5. Firebase Console > Authentication > Sign-in method: aktifkan Email/Password.
6. Buat Firestore Database.
7. Salin `firestore.rules` ke Firestore Database > Rules lalu tekan Publish.
8. Tunggu Gradle Sync di Android Studio, lalu jalankan ke HP Android.
9. Daftar akun guru pertama kali.
10. Masukkan NIS dan nama siswa kelas X TKR 7 satu per satu.
11. Ketuk tombol QR di kartu siswa untuk menampilkan QR. Simpan/screenshot lalu cetak.
12. Setiap pagi, tekan Scan QR dan pindai kartu siswa. Gunakan tombol status untuk memperbaiki catatan bila siswa izin/sakit/alpa.

## Struktur data
- `teachers/{uid}/students/{NIS}`
- `teachers/{uid}/attendance/{YYYY-MM-DD_NIS}`

## Catatan penting
- Proyek ini adalah kode sumber, bukan APK siap instal. File `google-services.json` harus dibuat dari Firebase milik pengguna dan tidak disertakan.
- Scan QR memerlukan layanan Google Play yang kompatibel; pemindaian pertama dapat memerlukan unduhan modul dan internet.
- Status “Alpa” yang ditampilkan sebagai hitungan adalah perkiraan siswa yang belum punya catatan pada hari tersebut. Untuk laporan resmi, guru tetap perlu memastikan ketidakhadiran.
- QR berisi NIS dan dapat dititipkan ke siswa lain. Ini bukan verifikasi identitas, jadi guru perlu memeriksa siswa secara langsung.
- MVP menggunakan satu catatan per siswa per tanggal. Jika ingin absensi beberapa sesi dalam satu hari, perlu ditambah fitur sesi.
- Ekspor saat ini membagikan teks CSV lewat aplikasi lain. Bisa dikembangkan menjadi file CSV unduhan langsung.
