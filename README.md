# 💰 Walletly - Money Manager

Aplikasi pencatatan keuangan pribadi berbasis web. Bisa langsung dipakai di browser!

## ✨ Fitur

- 🔐 **Login & Register** — Akun tersimpan di Firebase
- 📊 **Dashboard** — Ringkasan pemasukan & pengeluaran bulanan
- 📥📤 **Transaksi** — Catat pemasukan & pengeluaran dengan kategori
- 🔁 **Transaksi Berulang** — Tagihan otomatis (sewa, cicilan, internet)
- 👛 **Multi-Wallet** — Kelola beberapa sumber dana (Cash, Bank, E-Wallet)
- 📅 **Kalender** — Lihat transaksi dalam tampilan kalender
- 📊 **Laporan** — Grafik bulanan & breakdown per kategori
- ☁️ **Cloud Sync** — Data tersimpan otomatis di Firebase
- 📤 **Export** — Download data dalam format JSON

## 🚀 Cara Setup Firebase

### 1. Buat Project Firebase

1. Buka [Firebase Console](https://console.firebase.google.com/)
2. Klik **"Add Project"**
3. Beri nama project (misal: `walletly-app`)
4. Google Analytics: pilih **Enable/Disable** sesuai keinginan
5. Klik **"Create Project"**

### 2. Aktifkan Authentication

1. Di Firebase Console, klik **Authentication** (menu kiri)
2. Klik tab **"Sign-in method"**
3. Aktifkan **"Email/Password"**
4. Klik **"Save"**

### 3. Buat Firestore Database

1. Di Firebase Console, klik **Firestore Database** (menu kiri)
2. Klik **"Create database"**
3. Pilih **"Start in test mode"** (untuk development)
4. Pilih lokasi server (pilih yang terdekat, misal: `asia-southeast2` untuk Indonesia)
5. Klik **"Enable"**

### 4. Dapatkan Config Firebase

1. Di Firebase Console, klik **⚙️ Project Settings** (ikon gear di atas)
2. Scroll ke bawah, klik icon **Web** (`</>`)
3. Beri nama app (misal: `walletly-web`)
4. Klik **"Register app"**
5. Akan muncul config seperti ini:

```javascript
const firebaseConfig = {
    apiKey: "AIzaSy...",
    authDomain: "walletly-app.firebaseapp.com",
    projectId: "walletly-app",
    storageBucket: "walletly-app.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123"
};
```

6. **Copy config ini!**

### 5. Masukkan Config ke App

1. Buka file `index.html`
2. Cari bagian `// ⚠️ GANTI DENGAN CONFIG KAMU`
3. Ganti nilai config dengan milik kamu:

```javascript
const firebaseConfig = {
    apiKey: "API_KEY_KAMU",
    authDomain: "PROJECT_ID.firebaseapp.com",
    projectId: "PROJECT_ID",
    storageBucket: "PROJECT_ID.appspot.com",
    messagingSenderId: "SENDER_ID",
    appId: "APP_ID"
};
```

4. Simpan file

### 6. Atur Security Rules (Penting!)

Di Firestore Database → tab **Rules**, ganti dengan:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
      
      match /{document=**} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }
  }
}
```

Ini memastikan setiap user hanya bisa akses datanya sendiri!

## 🌐 Deploy ke GitHub Pages

### 1. Upload ke GitHub

```bash
# Buat repository baru di GitHub (misal: walletly-app)
# Lalu:
git init
git add index.html
git commit -m "Initial commit - Walletly Money Manager"
git branch -M main
git remote add origin https://github.com/USERNAME/walletly-app.git
git push -u origin main
```

### 2. Aktifkan GitHub Pages

1. Buka repository di GitHub
2. Klik **Settings** → **Pages**
3. Source: pilih **"Deploy from a branch"**
4. Branch: pilih **main** / **(root)**
5. Klik **Save**
6. Tunggu 1-2 menit
7. App bisa diakses di: `https://USERNAME.github.io/walletly-app/`

## 📱 Cara Pakai

1. Buka app di browser
2. **Daftar** akun baru (email + password)
3. **Login** dengan akun yang sudah dibuat
4. **Buat Wallet** (misal: Cash, BCA, GoPay)
5. **Tambah Transaksi** — pilih pemasukan/pengeluaran, kategori, jumlah
6. Data otomatis tersimpan di **Firebase Cloud** ☁️

## 🔒 Keamanan

- Data setiap user terpisah (tidak bisa akses data user lain)
- Password di-hash oleh Firebase Auth
- Data terenkripsi di Firestore
- Bisa export data kapan saja

## 📂 Struktur Data Firebase

```
users/
  └── {userId}/
      ├── name: "Nama User"
      ├── email: "user@email.com"
      ├── currency: "IDR"
      ├── wallets/
      │   └── {walletId}/
      │       ├── name: "BCA"
      │       ├── balance: 5000000
      │       └── icon: "🏦"
      ├── transactions/
      │   └── {transactionId}/
      │       ├── type: "expense"
      │       ├── amount: 50000
      │       ├── category: "food"
      │       ├── note: "Makan siang"
      │       ├── date: "2026-07-20"
      │       └── walletId: "w_xxx"
      └── recurring/
          └── {recurringId}/
              ├── type: "expense"
              ├── amount: 2300000
              ├── category: "rent"
              ├── note: "Sewa kos"
              └── day: 1
```

## 💡 Tips

- **Bookmark** halaman app di HP untuk akses cepat
- Data tersimpan **lokal + cloud**, jadi aman kalau browser di-clear
- Klik transaksi di list untuk **menghapus**
- Fitur **transaksi berulang** cocok untuk tagihan bulanan

---

Made with ❤️ | Walletly Money Manager
