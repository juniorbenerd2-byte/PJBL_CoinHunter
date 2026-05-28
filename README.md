# 🪙 Coin Hunter

> **Game platformer pengumpul koin berbasis browser — dibangun dengan Phaser 3**

Coin Hunter adalah game platformer 2D di mana pemain harus mengumpulkan semua koin yang tersebar di tiap level untuk naik ke level berikutnya. Hindari musuh yang bergerak bebas, gunakan kemampuan double jump untuk menjangkau platform tinggi, dan raih skor setinggi mungkin!

---

## 🎮 Cara Bermain

### Keyboard Controls

| Tombol | Aksi |
|--------|------|
| `→` / `D` | Bergerak ke kanan |
| `←` / `A` | Bergerak ke kiri |
| `↑` / `W` / `Space` | Lompat (bisa double jump!) |

### Mobile Controls (Layar Sentuh)
Pada perangkat mobile (landscape), tombol virtual otomatis muncul di layar:

| Tombol | Aksi |
|--------|------|
| `◀` | Bergerak ke kiri |
| `▲` | Lompat |
| `▶` | Bergerak ke kanan |
| `JUMP` | Lompat (tombol aksi kanan) |

> ⚠️ **Catatan Mobile:** Game hanya bisa dimainkan dalam mode **landscape**. Jika layar dalam posisi portrait, akan muncul peringatan untuk memutar perangkat.

---

## 🌟 Fitur Utama

- **🪙 Sistem Koin** — Kumpulkan semua 10 koin di setiap level untuk lanjut ke level berikutnya. Setiap koin bernilai **+10 poin**.
- **🦘 Double Jump** — Pemain dapat melompat dua kali di udara untuk menjangkau platform yang lebih tinggi.
- **👾 Musuh Dinamis** — Mulai level 3, musuh muncul dan bergerak acak di arena (bouncing dengan kecepatan random).
- **✨ Efek Partikel Koin** — Animasi partikel meledak saat koin berhasil dikumpulkan.
- **🔄 Transisi Level Mulus** — Layar fade in/out dengan animasi teks saat berpindah level.
- **💀 Game Over & Restart** — Layar game over dengan tombol restart langsung ketika tertabrak musuh.
- **📱 Responsive & Mobile-Friendly** — Skala canvas otomatis menyesuaikan ukuran viewport.

---

## 🗺️ Level & Layout Platform

Game memiliki **5 level** dengan layout platform yang berbeda-beda:

| Level | Jumlah Platform Tambahan | Musuh | Keterangan |
|-------|--------------------------|-------|------------|
| **Level 1** | 6 platform | ❌ Tidak ada | Level tutorial dasar |
| **Level 2** | 9 platform | ❌ Tidak ada | Layout lebih kompleks |
| **Level 3** | 5 platform | ✅ 1 musuh muncul | Mulai ada ancaman! |
| **Level 4** | 6 platform | ✅ Musuh bertambah | Layout sama seperti level 1 tapi ada musuh |
| **Level 5** | 9 platform | ✅ Musuh bertambah | Layout sama seperti level 2 tapi ada musuh |

Setiap level selalu memiliki **lantai dasar** yang memanjang dari ujung ke ujung layar.

### 📍 Spawn Point per Level
| Level | Posisi Spawn |
|-------|-------------|
| Level 1 | X: 100, Y: 500 |
| Level 2 | X: 200, Y: 400 |
| Level 3+ | X: 100, Y: 500 (default) |

---

## 👤 Karakter (Player)

### Spesifikasi Fisika
| Atribut | Nilai |
|---------|-------|
| Gravity Y | 800 |
| Bounce | 0.2 |
| Velocity X (bergerak) | ±200 px/s |
| Velocity Y (lompat) | -510 px/s |
| Max Jumps | 2 (double jump) |
| Sprite Size | 44.8 × 93 px per frame |

### 🎬 Animasi Karakter

| Animasi | Frame | Kondisi |
|---------|-------|---------|
| `right` | Frame 5–8 | Bergerak ke kanan di lantai |
| `left` | Frame 0–3 | Bergerak ke kiri di lantai |
| `front` | Frame 4 | Diam / menghadap depan |
| `jumpRight` | Frame 8 | Melompat ke kanan |
| `jumpLeft` | Frame 3 | Melompat ke kiri |

Semua animasi berjalan pada **12 fps** dengan loop tak terbatas.

---

## 👾 Musuh

Musuh mulai muncul sejak **Level 3** dan terus bertambah setiap level.

| Atribut | Nilai |
|---------|-------|
| Tipe | 3 jenis (Musuh01, Musuh02, Musuh03) — dipilih acak |
| Spawn posisi X | Acak antara 100 hingga (lebar canvas - 100) |
| Velocity X | Acak antara -200 hingga +200 px/s |
| Velocity Y | 20 px/s (sedikit ke bawah) |
| Gravity | Tidak terpengaruh gravity (`allowGravity = false`) |
| Bounce | 1 (memantul sempurna di dinding/batas dunia) |
| Collide World Bounds | ✅ Ya — musuh tidak bisa keluar layar |

**Efek terkena musuh:** Game langsung pause, pemain berubah merah, layar fade gelap, muncul layar **Game Over** dengan tombol restart.

---

## 🪙 Sistem Koin

| Atribut | Nilai |
|---------|-------|
| Jumlah koin per level | 10 koin |
| Nilai per koin | +10 poin |
| Bounce Y | 0.2 – 0.3 (acak, sedikit memantul) |
| Gravity | 800 (jatuh ke bawah) |
| Spawn posisi Y | -100 (dari atas, jatuh ke platform) |
| Efek kumpul | Partikel meledak di posisi koin + suara `koin.mp3` |

**Cara naik level:** Kumpulkan semua 10 koin → level otomatis naik → layout platform baru disiapkan.

---

## 🔊 Sistem Audio

| Key Audio | File | Deskripsi |
|-----------|------|-----------|
| `music_play` | `music_play.mp3` | BGM utama gameplay (loop) |
| `snd_coin` | `koin.mp3` | Suara koin terkumpul |
| `snd_jump` | `lompat.mp3` | Suara lompat |
| `snd_leveling` | `ganti_level.mp3` | Suara transisi level |
| `snd_lose` | `kalah.mp3` | Suara game over |
| `snd_walk` | `jalan.mp3` | Suara jalan (loop, aktif saat bergerak di tanah) |
| `snd_touch` | `touch.mp3` | Suara klik tombol Play |

> Semua audio tersedia dalam format **MP3** dan **OGG** untuk kompatibilitas lintas browser.

---

## 🖼️ Aset Gambar

| File | Ukuran | Kegunaan |
|------|--------|---------- |
| `BG.png` | ~90 KB | Background game & ambient layar |
| `CharaSpriteAnim.png` | ~40 KB | Spritesheet karakter (9 frame) |
| `Koin.png` | ~5 KB | Sprite koin |
| `Musuh01.png` | ~13 KB | Sprite musuh tipe 1 |
| `Musuh02.png` | ~9 KB | Sprite musuh tipe 2 |
| `Musuh03.png` | ~11 KB | Sprite musuh tipe 3 |
| `Tile50.png` | ~5 KB | Sprite platform/tanah |
| `PanelCoin.png` | ~7 KB | Panel HUD tampilan skor koin |
| `ButtonPlay.png` | ~27 KB | Tombol Play & Restart |
| `GameOver.png` | ~33 KB | Gambar layar Game Over |

---

## 🏗️ Struktur Proyek

```
Coin-Hunter/
├── index.html           # Entry point — konfigurasi Phaser & mobile controls
├── scenePlay.js         # Scene utama — seluruh logika gameplay
├── README.md            # Dokumentasi proyek ini
│
└── Assets/
    ├── images/
    │   ├── BG.png               # Background
    │   ├── CharaSpriteAnim.png  # Spritesheet karakter
    │   ├── Koin.png             # Sprite koin
    │   ├── Musuh01.png          # Musuh tipe 1
    │   ├── Musuh02.png          # Musuh tipe 2
    │   ├── Musuh03.png          # Musuh tipe 3
    │   ├── Tile50.png           # Platform/tanah
    │   ├── PanelCoin.png        # Panel skor
    │   ├── ButtonPlay.png       # Tombol play & restart
    │   └── GameOver.png         # Gambar game over
    │
    └── audio/
        ├── music_play.mp3/.ogg  # BGM utama
        ├── koin.mp3/.ogg        # Suara koin
        ├── lompat.mp3/.ogg      # Suara lompat
        ├── jalan.mp3/.ogg       # Suara berjalan
        ├── ganti_level.mp3/.ogg # Suara ganti level
        ├── kalah.mp3/.ogg       # Suara kalah
        └── touch.mp3/.ogg       # Suara tombol
```

---

## 🛠️ Teknologi

| Komponen | Teknologi |
|----------|-----------|
| Game Framework | **Phaser 3** (v3.55.2) via CDN |
| Bahasa | JavaScript (ES5 class pattern via `Phaser.Class`) |
| Physics Engine | Phaser Arcade Physics |
| Rendering | WebGL / Canvas (otomatis dipilih Phaser) |
| Resolusi Canvas | 1024 × 768 px |
| Responsive Scaling | CSS transform scale + Pointer Events API |
| Mobile Input | Custom touch → keyboard event bridge |
| Font | Verdana / Arial (built-in) |

---

## 🚀 Cara Menjalankan

Game ini adalah **pure web app** berbasis browser, tanpa instalasi apapun.

### Opsi 1: Live Server (VS Code) — Disarankan
```
1. Install ekstensi "Live Server" di VS Code
2. Klik kanan pada index.html
3. Pilih "Open with Live Server"
4. Browser akan terbuka otomatis
```

### Opsi 2: Python HTTP Server
```bash
cd Coin-Hunter
python -m http.server 8000
# Buka: http://localhost:8000
```

### Opsi 3: Node.js npx serve
```bash
cd Coin-Hunter
npx serve .
# Buka URL yang muncul di terminal
```

> ⚠️ **Penting:** Jangan buka `index.html` langsung via `file://` — audio dan aset tidak akan termuat dengan benar. Selalu gunakan HTTP server lokal.

---

## 🧠 Arsitektur Kode

```
index.html
├── Phaser 3 CDN (v3.55.2)
├── scenePlay.js (Logika utama)
│
└── Script inline
    ├── Konfigurasi Phaser Game (1024×768, Arcade Physics)
    ├── Responsive Canvas Scaler (CSS transform)
    └── Mobile Controls Bridge (Touch → KeyboardEvent)

scenePlay.js  (Phaser.Scene: "scenePlay")
├── preload()     → Load semua aset (gambar, audio, spritesheet)
├── create()      → Inisialisasi dunia, player, koin, musuh, animasi
│   ├── prepareWorld()         → Reset & buat layout platform per level
│   ├── newLevelTransition()   → Animasi teks + fade transisi level
│   ├── collectCoin()          → Handler kumpul koin + cek level naik
│   └── hitEnemy()             → Handler game over
└── update()      → Game loop: input player, animasi, audio berjalan
```

---

## 🎯 Alur Permainan

```
[Layar Menu / Tombol Play]
         │
         ▼
[Level dimulai — koin jatuh dari atas]
         │
    ┌────┴────┐
    │         │
[Kumpul koin] [Kena musuh]
    │         │
[Semua koin   [GAME OVER]
  terkumpul]  [→ Restart]
    │
[Naik level → Level baru disiapkan]
    │
[Level 3+: musuh mulai muncul]
    │
[Loop hingga ... (level tak terbatas)]
```

---

## 📱 Dukungan Platform

| Platform | Status |
|----------|--------|
| Desktop (Chrome, Firefox, Edge) | ✅ Penuh |
| Mobile Landscape (iOS Safari, Android Chrome) | ✅ Penuh + Virtual Controls |
| Mobile Portrait | ⚠️ Tampil peringatan rotate |
| Tablet Landscape | ✅ Penuh |

---

## 👨‍💻 Informasi Proyek

| | |
|-|-|
| **Nama Game** | Coin Hunter |
| **Framework** | Phaser 3 |
| **Tipe** | PJBL (Project-Based Learning) |
| **Repo** | PJBL-CoinHunter / Coin-Hunter |
| **Versi** | 1.2 |
| **Tahun** | 2026 |

---

*"Kumpulkan semua koin, hindari musuh, dan jadilah Coin Hunter terbaik!"* 🪙
