# 🎂 Birthday Website untuk Pacarmu 💕

Website ucapan ulang tahun romantis dengan animasi dan musik!

## ✨ Fitur

- 🎬 **Slideshow romantis** - Kata-kata manis ditampilkan satu per satu dengan efek typing
- 🎂 **Kue ulang tahun animasi** - Dibuat dengan CSS murni, ada lilin yang bisa ditiup!
- 🎊 **Confetti particles** - Efek confetti yang meriah menggunakan canvas
- 💕 **Floating hearts** - Hati-hati beterbangan di background
- 🎵 **Background music** - Musik romantis untuk suasana spesial
- 📱 **Responsive** - Cantik di HP maupun desktop

## 🎀 Cara Kustomisasi

### 1. Ganti Nama Pacar

Buka file `src/App.vue` dan cari bagian ini:

```typescript
// Nama pacarmu
const girlfriendName = ref('Sayang')
```

Ganti `'Sayang'` dengan nama pacarmu.

### 2. Tambahkan Foto Pacar

1. Taruh foto pacarmu di folder `public/` (contoh: `public/foto-sayang.jpg`)
2. Update di `src/App.vue`:

```typescript
// URL foto pacarmu
const girlfriendPhoto = ref('/foto-sayang.jpg')
```

### 3. Ganti Musik

1. Taruh file musik (MP3) di folder `public/` (contoh: `public/lagu-romantis.mp3`)
2. Buka `src/components/MusicPlayer.vue`
3. Ganti source audio:

```html
<source src="/lagu-romantis.mp3" type="audio/mpeg">
```

### 4. Edit Kata-kata Slideshow

Buka `src/components/SlideShow.vue` dan edit array `slides`:

```typescript
const slides: Slide[] = [
  { text: "Hai Sayang...", emoji: "💕" },
  { text: "Hari ini spesial banget", emoji: "✨" },
  // Tambah atau edit sesuai keinginan...
]
```

### 5. Edit Pesan Spesial

Di `src/App.vue`, cari bagian "Special message" dan edit sesuai keinginanmu.

## 🚀 Cara Deploy ke Vercel

### Opsi 1: Via GitHub

1. Push project ini ke repository GitHub kamu
2. Buka [vercel.com](https://vercel.com) dan login
3. Klik "New Project"
4. Import repository GitHub kamu
5. Vercel akan otomatis detect Vue/Vite dan deploy!

### Opsi 2: Via Vercel CLI

```bash
# Install Vercel CLI
npm install -g vercel

# Login ke Vercel
vercel login

# Deploy
vercel
```

## 💻 Development

```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Build untuk production
npm run build

# Preview production build
npm run preview
```

## 📁 Struktur Project

```
birthday-app/
├── public/              # Taruh foto & musik di sini
├── src/
│   ├── components/
│   │   ├── BirthdayCake.vue    # Kue ulang tahun animasi
│   │   ├── Confetti.vue        # Efek confetti
│   │   ├── FloatingHearts.vue  # Background hearts
│   │   ├── MusicPlayer.vue     # Player musik
│   │   ├── PhotoFrame.vue      # Frame foto
│   │   └── SlideShow.vue       # Slideshow kata-kata
│   ├── App.vue          # Main app (kustomisasi di sini!)
│   ├── main.ts
│   └── style.css        # Tailwind & animasi
├── index.html
└── package.json
```

## 💝 Tips

- Pilih foto dengan rasio portrait (3:4) untuk hasil terbaik
- Gunakan musik instrumental agar tidak mengganggu membaca
- Test di HP sebelum kirim ke pacar!
- Kirim link-nya pas tengah malam biar surprise! 🎉

---

Made with 💖 untuk pacarmu yang tercinta
