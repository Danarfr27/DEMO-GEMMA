# Gemma 4 E2B - Cyber Theme

Gemma 4 E2B (juga dikenal sebagai Firdhan-AI dalam mode online) adalah aplikasi asisten pribadi Android modern, premium, dan ultra-cepat yang dibangun menggunakan **Kotlin, Jetpack Compose, Material 3, MVVM, Room Database, Coroutines, dan Flow**. Aplikasi ini mengusung visual bertema **Cyber Hacker** yang gahar dan dinamis, serta dilengkapi kecerdasan offline dengan asisten suara laki-laki yang responsif dan cerdas.

---

## 🚀 Fitur Utama & Visual Baru

- **🟢 Cyber Hacker Theme**: Tampilan gelap pekat murni (`0xFF000000`) berpadu dengan aksen hijau neon menyala (`0xFF39FF14`) yang super tajam, memberikan estetika siber ala hacker profesional.
- **🚨 Parallax & Ambulance Glow Background**: Efek visual latar belakang siber interaktif yang dinamis. Menggabungkan kedipan perlahan pancaran hijau-hitam yang menyapu bergantian layaknya lampu ambulans siber, serta grid 3D dan titik node siber yang bergerak secara paralaks saat layar digeser (*drag*).
- **📋 Copy Button Instant**: Tombol salin teks cepat sekali sentuh di setiap balon chat (*bubble message*) asisten maupun pengguna untuk kemudahan dokumentasi data.
- **💬 Balon Chat Kontras Tinggi**: Desain balon chat asisten dengan warna gelap pekat dipadukan aksen hijau neon, sedangkan balon chat pengguna berwarna hijau neon cerah dengan teks berwarna hitam pekat (`Color.Black`) agar sangat mudah dibaca.
- **⚡ Smart Action Engine**: Memproses perintah sistem sehari-hari dan memicu aksi nyata pada perangkat Android secara offline maupun online:
  - Mengontrol lampu senter perangkat (*Flashlight*).
  - Membuka aplikasi terinstal (WhatsApp, Chrome, Kamera, YouTube, Spotify, dsb).
  - Membuka Pengaturan sistem (WiFi, Bluetooth, dsb).
  - Melakukan panggilan telepon & mengirim SMS.
  - Membuka navigasi peta Google Maps.
  - Menyimpan profil informasi pengguna langsung ke penyimpanan lokal (*User Memory*).
- **🗣️ Male Voice Assistant**: Karakter asisten suara diubah menjadi suara asisten laki-laki yang ramah, sopan, berwibawa, dan responsif untuk kenyamanan berinteraksi.
- **🎤 ChatGPT-style Continuous Voice**: Fitur ngobrol suara secara langsung dan terus-menerus tanpa perlu repot klik tombol mikrofon berkali-kali. Sistem secara otomatis mendengarkan, menjawab, dan mendengarkan kembali secara interaktif.
- **🌾 Sundanese Language Mode (`/sunda`)**: Dukungan bahasa daerah Sunda dalam versi offline! Cukup ketik perintah `/sunda` untuk mengaktifkan asisten berbahasa Sunda yang sopan (*lemes*). Untuk mematikan, cukup ketik `/sunda off`.
- **⏰ Alarm & Suara Pengingat Otomatis**: Integrasi pengingat langsung ke jam ponsel. Saat waktu di HP cocok dengan pengingat terdaftar, asisten akan menyalakan alarm suara dan membacakan isi pengingat sebanyak 10 kali secara otomatis. Kamu bisa mematikan alarm secara instan cukup dengan mengucapkan kata **"stop"** atau **"stop pengingat"**.
- **🔄 Sync & Offline Learning (Diajar ti Riwayat)**: Setiap obrolan online kamu dengan AI secara cerdas akan disimpan ke database lokal (*chat_history*). Ketika kamu beralih ke mode offline, asisten Gemma 4 E2B akan membaca riwayat tersebut dan memberikan jawaban cerdas yang sama persis layaknya sedang online. AI versi offline kamu sekarang bisa belajar dari riwayat masa lalu!

---

## 🛠️ Panduan Build & Instalasi

### Prasyarat
- **Android Studio Ladybug (2024.2.1)** atau yang lebih baru.
- **JDK 17+** terinstal di sistem Anda.
- Perangkat Android fisik atau Emulator dengan **Android SDK 24** ke atas.

### Langkah Build APK
1. Clone repositori ini atau ekstrak folder project.
2. Buka **Android Studio**, pilih **File > Open**, lalu arahkan ke folder root project ini.
3. Tunggu hingga Gradle sinkronisasi (*sync*) selesai secara otomatis.
4. Konfigurasikan API Key Anda di panel **Secrets** atau file `.env` di direktori root (salin dari `.env.example`).
5. Sambungkan perangkat Android Anda via USB Debugging atau jalankan Android Emulator.
6. Klik tombol **Run (:app)** di toolbar atas Android Studio, atau jalankan perintah Gradle berikut di terminal untuk membuild APK:
   ```bash
   gradle :app:assembleDebug
   ```
7. File APK hasil build akan tersimpan di:
   `app/build/outputs/apk/debug/app-debug.apk`

---

## ⚙️ Konfigurasi Mode Online / Offline

Aplikasi ini mendukung operasi transisi cerdas antara Mode Online (menggunakan Gemini API) dan Mode Offline (menggunakan asisten lokal bawaan):

### 1. Mode Offline (Lokal Perangkat)
Aplikasi secara otomatis mendeteksi perintah sistem sehari-hari dan memprosesnya secara instan tanpa memerlukan koneksi internet:
- **Pengenalan Pola Lokal**: Masukan seperti `/nyalakan lampu`, `/buka whatsapp`, `/siapa nama saya?`, atau `/catat beli kopi` diproses secara offline lewat database **Room** dan fungsi sistem internal untuk menjamin respon kilat 0-ms dan privasi 100%.

### 2. Mode Online (Awan Cerdas)
Untuk pertanyaan pengetahuan umum, penalaran rumit (*reasoning*), pengodean, atau kuis interaktif, aplikasi mengirimkan kueri ke server Gemma/Gemini secara aman menggunakan Retrofit Client.

---

## 📂 Struktur Arsitektur (Clean Architecture + MVVM)

```
com.example/
│
├── data/
│   ├── database/       # Room Database, DAO, dan Entitas (Notes, Reminders, Memory, Habits)
│   └── repository/     # Repository untuk enkapsulasi penyimpanan data lokal
│
├── ai/                 # Retrofit Client, API Service, dan Data Model untuk Gemini REST API
│
├── voice/              # Pengelola Text-to-Speech (TTS) dan integrasi Asisten Suara
│
├── utils/              # Pengendali Flashlight, Pencari Package Aplikasi, dan Action Executor
│
├── ui/
│   ├── theme/          # Konfigurasi Tema Material 3, Warna, dan Tipografi Cyber Hacker
│   ├── viewmodel/      # Master ViewModel (Manajemen State, Logika Chat, dan Aksi Perangkat)
│   ├── screens/        # Komponen Layar Jetpack Compose (Dashboard, Chat, Voice, Productivity, Settings)
│   └── components/     # HackerBackground dengan efek paralaks dan kedipan hijau-hitam ambulans
```

---

## 🔒 Pernyataan Keamanan (API Key Security)

> **Peringatan Keamanan**: API Key diletakkan secara aman menggunakan plugin Gradle Secrets dari file `.env`. Jangan pernah mempublikasikan file APK hasil kompilasi yang mengandung kunci API pribadi ke publik tanpa pengamanan proxy backend guna menghindari potensi penyalahgunaan kuota oleh pihak ketiga.
