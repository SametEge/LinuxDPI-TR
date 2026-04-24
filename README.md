<div align="center">

# LinuxDPI-TR

**Türkiye'deki internet kısıtlamalarını aşmak için Linux masaüstü uygulaması**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://python.org)
[![GTK4](https://img.shields.io/badge/GTK-4-green?logo=gnome)](https://gtk.org)
[![Arch Linux](https://img.shields.io/badge/Arch-Linux-1793D1?logo=arch-linux)](https://archlinux.org)
[![Yapımcı](https://img.shields.io/badge/Yapımcı-Samet%20Ege%20Derin-orange)](https://github.com/sametege)

</div>

---

## Nedir?

**LinuxDPI-TR**, Türkiye'deki internet kullanıcıları için geliştirilmiş, DPI (Derin Paket İnceleme) atlatma ve VPN tünelleme araçlarını tek bir GTK4 arayüzünden yönetmenizi sağlayan açık kaynaklı bir Linux uygulamasıdır.

Cloudflare WARP, Zapret, ByeDPI gibi popüler araçların kurulum ve yönetimini **tek tıkla** halleder; teknik bilgi gerektirmez.

---

## Özellikler

| Sekme | Açıklama |
|---|---|
| **WireGuard** | Cloudflare WARP üzerinden WireGuard tüneli — tek buton bağlan/kes |
| **ByeDPI** | SOCKS5 proxy ile DPI atlatma, systemd servisi olarak çalışır |
| **Zapret** | nfqws tabanlı sistem geneli DPI atlatma, ISP'ye göre hazır ayarlar |
| **DNS** | Google, Cloudflare, Quad9, OpenDNS seçenekleri |
| **Gelişmiş** | Tüm servisleri yönet, kaldır, logları izle |

- Eksik araçlar **otomatik kurulur** (pacman + AUR)
- Polkit yerine **kendi şifre diyaloğu** (tek seferlik sorar, önbelleğe alır)
- Koyu tema, Türkçe arayüz
- Systemd servisi olarak otomatik başlatma

---

## Kurulum

### Yöntem 1 — Tek Komut (En Hızlı)

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/sametege/LinuxDPI-TR/main/install.sh)
```

Hepsi bu kadar. Script gerekli tüm paketleri kurar ve her şeyi otomatik olarak ayarlar.

---

### Yöntem 2 — Adım Adım

**Adım 1 — Git yoksa kur**
```bash
sudo pacman -S git
```

**Adım 2 — Repoyu klonla**
```bash
git clone https://github.com/sametege/LinuxDPI-TR.git
cd LinuxDPI-TR
```

**Adım 3 — Kurulum scriptini çalıştır**
```bash
bash install.sh
```

Script otomatik olarak şunları yapar:
- Gerekli paketleri kurar (`python-gobject`, `gtk4`, `wireguard-tools`, `nftables`)
- `yay` veya `paru` varsa AUR araçlarını kurar (`wgcf`, `byedpi`, `zapret`)
- Uygulamayı `/usr/local/bin/linuxdpi-tr` olarak ekler
- Uygulama menüsüne masaüstü kısayolu oluşturur

**Adım 4 — Başlat**
```bash
linuxdpi-tr
```
Ya da uygulama menüsünden **LinuxDPI-TR** olarak ara.

---

### Yöntem 3 — Kurmadan Çalıştır

Kurmadan denemek istiyorsan:

```bash
git clone https://github.com/sametege/LinuxDPI-TR.git
cd LinuxDPI-TR
python3 linuxdpi.py
```

> Önce bağımlılıkları manuel kurman gerekebilir:
> ```bash
> sudo pacman -S python-gobject wireguard-tools nftables
> yay -S wgcf byedpi zapret   # yay veya paru gerekli
> ```

---

## Gereksinimler

| Zorunlu | İsteğe Bağlı |
|---|---|
| Python 3.8+ | yay veya paru (AUR yardımcısı) |
| python-gobject (GTK4) | proxychains-ng |
| wireguard-tools | |
| nftables | |

> AUR yardımcısı yoksa `wgcf`, `byedpi`, `zapret` araçları otomatik kurulamaz — manuel kurabilir ya da uygulama içinden sonradan kurabilirsin.

---

## Kullanım

### WireGuard / Cloudflare WARP

1. **WireGuard** sekmesine geç
2. **"Bağlan"** butonuna bas
3. İlk çalıştırmada şifre istenir (oturum boyunca bir kez)
4. Eksik araçlar otomatik kurulur, kayıt yapılır, bağlantı kurulur

### ByeDPI (SOCKS5 Proxy)

1. **ByeDPI** sekmesine geç
2. Port numarasını belirle (varsayılan: `1080`)
3. **"Servis Kur"** butonuna bas
4. Tarayıcı proxy ayarını `127.0.0.1:1080` yap

> Discord için: `proxychains discord`

### Zapret (Sistem Geneli DPI Atlatma)

1. **Zapret** sekmesine geç
2. Servis sağlayıcını seç (Türk Telekom / Turkcell / Vodafone TR / Genel)
3. **"Hizmet Kur"** — sistem başlangıcında otomatik çalışır
4. **"Tek Seferlik"** — sadece şu an için çalıştırır

### DNS Ayarları

1. **DNS** sekmesine geç
2. DNS sunucusunu seç
3. **"DNS Ayarla"** butonuna bas

---

## Ekran Görüntüleri

> *(Ekran görüntüleri yakında eklenecek)*

---

## Desteklenen Dağıtımlar

Birincil hedef **Arch Linux** olmakla birlikte GTK4 ve Python bulunan her dağıtımda çalışır:

- Arch Linux / CachyOS / Manjaro
- Fedora (paket isimleri farklı olabilir)
- Ubuntu 22.04+ / Debian 12+

---

## Kullanılan Araçlar ve Atıflar

- **[wgcf](https://github.com/ViRb3/wgcf)** — Cloudflare WARP WireGuard profili oluşturma
- **[wireguard-tools](https://git.zx2c4.com/wireguard-tools)** — WireGuard VPN istemcisi
- **[byedpi](https://github.com/hufrea/byedpi)** — DPI bypass SOCKS5 proxy
- **[zapret](https://github.com/bol-van/zapret)** — Sistem geneli DPI atlatma (nfqws)
- **[nftables](https://netfilter.org/projects/nftables/)** — Linux paket filtreleme

---

## Sorumluluk Reddi

Bu yazılım yalnızca **eğitim ve kişisel kullanım** amaçlıdır.  
Kullanımdan doğan yasal sorumluluk kullanıcıya aittir.

---

## Lisans

MIT License — © 2026 Samet Ege Derin  
Detaylar için [LICENSE](LICENSE) dosyasına bakın.

---

## Katkı

Pull request ve issue açmaktan çekinmeyin.  
GitHub: [github.com/sametege/LinuxDPI-TR](https://github.com/sametege/LinuxDPI-TR)
