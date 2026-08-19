Obsidian dan Git adalah pasangan yang sangat sempurna. Karena Obsidian menyimpan semua catatan dalam format teks biasa (Markdown / `.md`), Git bisa melacak perubahannya dengan sangat ringan dan akurat.
  
Berikut adalah alasan kenapa ide ini sangat layak dieksekusi:
### 1. _Version Control_ (Fitur Dewa)

Ini adalah keuntungan terbesar yang bahkan tidak dimiliki oleh Obsidian Sync berbayar secara mendetail. Dengan Git, kamu punya riwayat (_history_) lengkap dari setiap catatanmu. Ini akan menjadi penyelamat nyawa yang luar biasa untuk mengamankan draf metodologi skripsi atau dokumentasi _source code_—kalau suatu hari ada bab atau paragraf penting yang tidak sengaja terhapus atau tertimpa, kamu tinggal mengecek _commit history_ dan mengembalikannya dalam hitungan detik.
### 2. Sepenuhnya Gratis & Privat

Kamu bisa membuat _Private Repository_ di GitHub atau GitLab secara gratis. Kapasitas repositori Git biasanya lebih dari cukup untuk menampung ribuan catatan berbasis teks, bahkan jika kamu menyisipkan banyak gambar di dalamnya.
### Cara Mengeksekusinya Secara Elegan
**Gunakan Community Plugin: "Obsidian Git"**
  
1. Buka pengaturan Obsidian, masuk ke tab **Community plugins**, matikan _Safe mode_, lalu cari plugin bernama **Git**.
      
2. Plugin ini akan berjalan di latar belakang dan melakukan eksekusi perintah Git secara otomatis.
      
3. Kamu bisa mengaturnya agar melakukan _auto-commit_ dan _auto-push_ setiap 10 menit, atau setiap kali kamu menutup aplikasi Obsidian. Ia juga bisa otomatis melakukan _git pull_ saat aplikasi baru dibuka agar laptopmu selalu mendapat catatan versi terbaru.
### ⚠️ Satu Kekurangan Utama (Harus Tahu)

Kelemahan dari metode ini hanya ada pada **sinkronisasi ke perangkat _Mobile_ (HP)**. Aplikasi Obsidian di Android/iOS tidak memiliki akses _native_ ke sistem Git.

Jika kamu ingin membuka catatan itu di Android, kamu harus sedikit _ngoprek_ menggunakan aplikasi pihak ketiga seperti Termux atau aplikasi Git _client_ Android (seperti MGit) untuk menarik repositorinya ke memori internal HP, yang mana prosesnya kurang praktis. Tapi jika kebutuhanmu hanya sinkronisasi antar PC/Laptop (misal antara Linux dan Windows), Git adalah solusi paling tangguh.

Untuk menghubungkan folder lokal ke repositori _private_ di _cloud_, prosesnya sebenarnya standar seperti proyek _coding_ pada umumnya. Hal yang membuatnya menjadi _private_ ditentukan saat kamu membuat wadahnya di GitHub atau GitLab.
  
Berikut adalah langkah _sat-set_ dari awal sampai catatanmu berhasil mengudara dengan aman:
### 1. Buat Repositori Kosong di GitHub/GitLab

1. Buka _browser_ dan masuk ke akun GitHub atau GitLab milikmu.
      
2. Buat repositori baru (_New Repository_).
      
3. Beri nama repositori (misalnya `obsidian-vault`).
      
4. **Krusial:** Pada bagian visibilitas, pastikan kamu memilih opsi **Private** agar orang lain tidak bisa melihat catatan pribadimu.
      
5. Jangan centang apa pun di bagian inisiasi (_Add a README, .gitignore_, dll). Biarkan benar-benar kosong.
      
6. Klik **Create repository**.
      
7. Salin URL repositori yang muncul (contoh: `[https://github.com/username/obsidian-vault.git](https://github.com/username/obsidian-vault.git)`).
### 2. Inisiasi Git di Terminal Lokal

Buka terminal openSUSE-mu, arahkan langsung ke folder tempat _vault_ itu berada, dan mulai inisiasi:

```
cd ~/Documents/Obsidian\ Vault
git init
```

### 3. Tambahkan Aturan `.gitignore` (Wajib untuk Obsidian)

Sebagai _developer_, kamu pasti tahu pentingnya mengabaikan _file_ yang sering berubah tapi tidak penting. Di Obsidian, _file_ yang mengatur posisi tab dan _layout_ layar akan berubah setiap detik saat kamu menggunakan aplikasinya. Jika tidak diabaikan, _commit history_-mu akan dipenuhi sampah perubahan _layout_.
  
Jalankan perintah ini untuk membuat _file_ `.gitignore` yang memblokir _file_ _layout_ tersebut:
  
```
echo ".obsidian/workspace.json" > .gitignore
echo ".obsidian/workspace-mobile.json" >> .gitignore
```

### 4. Commit dan Sambungkan ke Remote

Sekarang saatnya membungkus seluruh catatanmu (termasuk folder `.obsidian` yang berisi tema dan pengaturan) lalu mendorongnya ke repositori _private_ tadi.
  
Jalankan perintah ini secara berurutan:
  
```
git add .
git commit -m "Initial commit: Setup Obsidian Vault"
git branch -M main
git remote add origin URL_REPOSITORY_YANG_KAMU_SALIN_TADI
git push -u origin main
```

> **💡 Catatan Autentikasi:**
> 
> Jika kamu menggunakan URL HTTPS (bukan SSH), saat menjalankan `git push`, GitHub/GitLab tidak lagi menerima _password_ akun biasa. Pastikan kamu menggunakan **Personal Access Token (PAT)** sebagai _password_-nya, atau _setting_ SSH Key agar lebih praktis ke depannya.  

Setelah proses _push_ selesai, folder `~/Documents/Obsidian Vault` milikmu sudah resmi terhubung secara _private_. Selanjutnya kamu tinggal mengonfigurasi _plugin_ "Obsidian Git" di dalam aplikasinya agar proses _add, commit_, dan _push_ ini berjalan otomatis di latar belakang!

Berikut adalah cara mencari _username_ dan membuat _password_ (Token) tersebut (asumsi kamu menggunakan **GitHub**):
### 1. Cari Tahu _Username_ Aslimu

1. Buka browser dan masuk ke [github.com](https://github.com/) (kamu akan otomatis _login_ dengan Google-mu).
      
2. Klik foto profilmu di pojok kanan atas.
      
3. Di situ akan tertulis **Signed in as ...** (misalnya `rokhman-dev`). Itulah _username_ yang harus kamu ketik di terminal nanti.
### 2. Buat Personal Access Token (Pengganti Password)

1. Klik foto profilmu lagi, lalu pilih menu **Settings** (Pengaturan).
      
2. Di menu sebelah kiri, _scroll_ paling bawah dan klik **Developer settings**.
      
3. Di menu kiri lagi, klik **Personal access tokens**, lalu pilih **Tokens (classic)**.
      
4. Klik tombol **Generate new token (classic)** di sebelah kanan atas.
      
5. Isi kolom **Note** dengan nama yang mudah diingat (misal: `Obsidian openSUSE`).
      
6. Pada bagian **Expiration**, atur menjadi **No expiration** agar tokennya tidak kedaluwarsa (karena ini untuk _vault_ catatanmu sendiri).
      
7. Di bagian **Select scopes** (kotak centang), **kamu WAJIB mencentang kotak `repo`**. (Ini memberikan izin agar token tersebut bisa membaca dan menulis di repositori _private_).
      
8. _Scroll_ ke paling bawah dan klik **Generate token**.
      
9. **PENTING:** Akan muncul deretan kode panjang (dimulai dengan `ghp_...`). **Salin kode tersebut sekarang juga!** Kode ini hanya akan ditampilkan satu kali seumur hidup.
### 3. Eksekusi di Terminal

Kembali ke terminal openSUSE-mu dan jalankan ulang perintah `git push -u origin main`.
  
- **Username:** Ketik _username_ yang kamu temukan di Langkah 1, lalu tekan Enter.
      
- **Password:** _Paste_ (Tempelkan) kode token `ghp_...` yang sudah kamu salin tadi.
    _(Catatan Linux: Saat kamu mem-paste atau mengetik password di terminal, layarnya tidak akan memunculkan bintang atau karakter apa pun. Terlihat seperti tidak terjadi apa-apa, padahal kodenya sudah masuk. Langsung saja tekan Enter!)._

### 💡 Trik Ekstra agar Tidak Ditanya Password Terus

Karena ke depannya kamu akan menggunakan _plugin_ Obsidian Git agar dia melakukan _push_ secara otomatis, kamu harus menyimpan token ini di laptopmu agar Git tidak menanyakan _password_ lagi setiap menit.
  
Setelah kamu berhasil melakukan _push_ pertama tadi, jalankan perintah ini di terminal:

```
git config --global credential.helper store
```

Lalu lakukan `git push` satu kali lagi (secara manual). Git akan meminta _username_ dan token-mu untuk yang **terakhir kalinya**, lalu menyimpannya secara permanen di dalam sistem openSUSE-mu. Setelah itu, _plugin_ Obsidian Git bisa berjalan otomatis di latar belakang dengan mulus!