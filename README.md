# CardScan Pro - QR Code Web Fallback

Bu klasör GitHub Pages üzerinden serve edilir. QR kod okutulduğunda uygulama yüklü değilse bu sayfa açılır.

## Kurulum

### 1. GitHub Repository Oluştur

```bash
# Yeni bir repo oluştur (örnek: "card")
# https://github.com/new
```

### 2. Bu dosyaları yükle

```bash
# Bu docs klasörünün içeriğini repo'nun kök dizinine kopyala
# Veya bu projeyi direkt push et
```

### 3. GitHub Pages Aktifleştir

1. GitHub repo → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** (veya master)
4. Folder: **/ (root)** veya **/docs**
5. **Save**

### 4. URL'leri Güncelle

GitHub Pages URL'niz: `https://USERNAME.github.io/REPO_NAME/`

Güncellenecek dosyalar:

**1. CardPayload.swift (Xcode'da):**
```swift
static var webBaseURL: String = "https://USERNAME.github.io/REPO_NAME/c.html"
```

**2. CardScanProAI.entitlements:**
```xml
<key>com.apple.developer.associated-domains</key>
<array>
    <string>applinks:USERNAME.github.io</string>
</array>
```

**3. c.html (App Store ID - opsiyonel):**
```javascript
// Line 464: App Store link
document.getElementById('app-store-link').href = 'https://apps.apple.com/app/id123456789';
```

## Dosya Yapısı

```
docs/
├── .well-known/
│   └── apple-app-site-association  # Universal Links için
├── c.html          # Kart görüntüleyici (QR fallback)
├── index.html      # Landing page
├── privacy.html    # Gizlilik politikası
├── support.html    # Destek sayfası
└── README.md       # Bu dosya
```

## Test

1. GitHub Pages URL'nizi açın: `https://USERNAME.github.io/REPO_NAME/`
2. `.well-known/apple-app-site-association` dosyasının erişilebilir olduğunu kontrol edin
3. QR kodu okutun ve sayfanın açıldığını doğrulayın

## Universal Links

Universal Links çalışması için:

1. **Associated Domains** Capability Xcode'da aktif olmalı
2. **apple-app-site-association** dosyası HTTPS üzerinden erişilebilir olmalı
3. Team ID + Bundle ID doğru olmalı: `LB86P743G5.com.berk.cardscanproai.ios`
