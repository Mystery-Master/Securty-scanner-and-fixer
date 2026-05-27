# 🛡 VulnGuard

> **Python Güvenlik Açığı Tarayıcı, Sınıflandırıcı ve Onarıcı**  
> Kaynak kodunuzdaki güvenlik açıklarını tespit edin, sınıflandırın ve otomatik olarak onarın.

---

## 📋 İçindekiler

- [Genel Bakış](#-genel-bakış)
- [Özellikler](#-özellikler)
- [Kurulum](#-kurulum)
- [Hızlı Başlangıç](#-hızlı-başlangıç)
- [Kullanım](#-kullanım)
- [Güvenlik Kuralları](#-güvenlik-kuralları)
- [Çıktı Formatları](#-çıktı-formatları)
- [Otomatik Onarım](#-otomatik-onarım)
- [CI/CD Entegrasyonu](#-cicd-entegrasyonu)
- [Örnekler](#-örnekler)
- [Proje Yapısı](#-proje-yapısı)
- [Katkıda Bulunma](#-katkıda-bulunma)
- [Lisans](#-lisans)

---

## 🔍 Genel Bakış

VulnGuard, Python kaynak kodlarını, konfigürasyon dosyalarını ve bağımlılık tanımlarını statik analiz yöntemiyle tarayan bir güvenlik aracıdır. Herhangi bir harici servis veya kurulum gerektirmez; tamamen yerel çalışır.

**Temel felsefesi:** Güvenlik açıklarını sadece tespit etmekle kalmaz, her açık için:
- 📌 Tam konum bilgisi (dosya + satır numarası)
- 🏷 Önem seviyesi ve kategori sınıflandırması
- 📖 İnsan okunabilir açıklama
- 💡 Somut çözüm önerisi
- 🔧 Mümkünse otomatik kod onarımı

sağlar.

---

## ✨ Özellikler

| Özellik | Açıklama |
|---|---|
| 🔎 **Statik Analiz** | Regex tabanlı 15 güvenlik kuralı ile kaynak kod taraması |
| 🏷 **Sınıflandırma** | 5 önem seviyesi (Kritik → Bilgi) ve 10 kategori |
| 🔧 **Otomatik Onarım** | 9 kural için tek komutla otomatik kod düzeltmesi |
| 🧪 **Dry-Run Modu** | Dosyaları değiştirmeden onarım önizlemesi |
| 📄 **HTML Raporu** | Dark-theme, profesyonel görsel rapor |
| 📊 **JSON Raporu** | CI/CD sistemleriyle entegrasyon için makine okunabilir çıktı |
| 🎨 **Renkli Terminal** | ANSI renk kodlarıyla önem bazlı renkli terminal çıktısı |
| 📁 **Dizin Tarama** | Tüm proje dizinini tek komutla tara |
| 🚦 **CI/CD Çıkış Kodları** | Kritik açık varsa exit(2), diğer açıklar exit(1) |
| 🔇 **Akıllı Hariç Tutma** | `.venv`, `__pycache__`, `.git` gibi dizinleri otomatik atlar |

---

## 📦 Kurulum

VulnGuard, Python standart kütüphanesini kullanır. Ek bağımlılık gerektirmez.

**Gereksinim:** Python 3.7+

```bash
# Depoyu klonlayın
git clone https://github.com/Mystery-Master/Securty-scanner-and-fixer.git
cd vulnguard

# Doğrudan çalıştırın (bağımlılık yok!)
python vulnerability_scanner.py --help
```

İsteğe bağlı olarak çalıştırılabilir yapabilirsiniz:

```bash
chmod +x vulnerability_scanner.py
./vulnerability_scanner.py .
```

---

## 🚀 Hızlı Başlangıç

```bash
# Mevcut dizini tara
python vulnerability_scanner.py .

# Tek bir dosyayı tara
python vulnerability_scanner.py myapp.py

# Tara ve HTML + JSON raporu üret
python vulnerability_scanner.py . --html rapor.html --json rapor.json

# Otomatik onarımları önizle
python vulnerability_scanner.py . --fix

# Otomatik onarımları gerçekten uygula
python vulnerability_scanner.py . --fix --no-dry-run
```

---

## 📖 Kullanım

```
kullanım: vulnerability_scanner.py [seçenekler] [hedef]

Konumsal Argümanlar:
  target                Taranacak dosya veya dizin yolu (varsayılan: .)

Seçenekler:
  -h, --help            Yardım mesajını göster ve çık
  --fix                 Otomatik onarılabilir açıkları onar
  --dry-run             Onarımları gerçekleştirmeden göster (varsayılan: açık)
  --no-dry-run          Onarımları gerçekten uygula (dosyaları değiştirir!)
  --json DOSYA          Raporu JSON olarak kaydet
  --html DOSYA          Raporu HTML olarak kaydet
  --verbose, -v         Ayrıntılı çıktı (tarama sırası, eşleşmeler)
  --min-severity SEVİYE Minimum önem filtresi: KRİTİK|YÜKSEK|ORTA|DÜŞÜK|BİLGİ
```

### Tarama Hedefleri

```bash
# Tek Python dosyası
python vulnerability_scanner.py app.py

# Tüm proje dizini
python vulnerability_scanner.py /projem/

# Mevcut dizin
python vulnerability_scanner.py .
```

Varsayılan olarak şu uzantılı dosyalar taranır: `.py` `.cfg` `.ini` `.env` `.yaml` `.yml` `.json`

---

## 🔐 Güvenlik Kuralları

VulnGuard 15 güvenlik kuralı içerir. Her kural bir ID, başlık, önem seviyesi ve kategori ile tanımlanır.

### Kural Tablosu

| ID | Başlık | Önem | Kategori | Oto-Onarım | CWE/CVE |
|---|---|---|---|---|---|
| SEC-001 | Sabit Şifre | 🔴 KRİTİK | Sabit Gizli Veri | ✅ | — |
| SEC-002 | Sabit API Anahtarı | 🔴 KRİTİK | Sabit Gizli Veri | ✅ | — |
| SEC-003 | SQL Enjeksiyonu | 🟠 YÜKSEK | Enjeksiyon | ❌ | CWE-89 |
| SEC-004 | shell=True Komutu | 🟠 YÜKSEK | Komut Enjeksiyonu | ✅ | — |
| SEC-005 | MD5/SHA1 Hash | 🟡 ORTA | Güvensiz Kriptografi | ✅ | — |
| SEC-006 | DES/3DES Şifreleme | 🟠 YÜKSEK | Güvensiz Kriptografi | ❌ | — |
| SEC-007 | pickle.loads | 🔴 KRİTİK | Güvensiz Serimleme | ❌ | CWE-502 |
| SEC-008 | Yol Geçişi | 🟠 YÜKSEK | Path Traversal | ❌ | CWE-22 |
| SEC-009 | Zayıf random | 🟡 ORTA | Güvensiz Rastgele Sayı | ✅ | — |
| SEC-010 | debug=True | 🟠 YÜKSEK | Debug Kodu | ✅ | — |
| SEC-011 | Hassas Veri Loglama | 🟡 ORTA | Debug Kodu | ❌ | — |
| SEC-012 | eval/exec Kullanımı | 🔴 KRİTİK | Enjeksiyon | ❌ | CWE-78 |
| SEC-013 | SSL verify=False | 🟠 YÜKSEK | Güvensiz Kriptografi | ✅ | — |
| SEC-014 | XML XXE Riski | 🟡 ORTA | Enjeksiyon | ❌ | CWE-611 |
| SEC-015 | Geniş Dosya İzni | 🟡 ORTA | İzin Hatası | ✅ | — |

### Önem Seviyeleri

```
🔴 KRİTİK  — Anında müdahale gerektirir. Uzaktan kod çalıştırma, kimlik bilgisi sızıntısı.
🟠 YÜKSEK  — Yakın vadede düzeltilmeli. Enjeksiyon, kimlik doğrulama sorunları.
🟡 ORTA    — Planlı geliştirme sürecinde ele alınmalı. Zayıf kriptografi, loglama.
🟢 DÜŞÜK   — En iyi pratiklerden sapma. Acil risk yok.
🔵 BİLGİ   — Bilgilendirme amaçlı. Risk içermeyebilir.
```

### Kategoriler

- **Enjeksiyon** — SQL, komut, eval, XXE enjeksiyonları
- **Sabit Gizli Veri** — Kodda gömülü şifre, token ve API anahtarları
- **Güvensiz Kriptografi** — Zayıf hash ve şifreleme algoritmaları, SSL sorunları
- **Güvensiz Serimleme** — pickle, YAML yükleyici güvenlik sorunları
- **Path Traversal** — Kullanıcı girdisiyle kontrol edilen dosya yolları
- **Komut Enjeksiyonu** — shell=True ile komut çalıştırma
- **Güvensiz Rastgele Sayı** — Kriptografik amaçlı zayıf random kullanımı
- **Debug Kodu** — Üretimde aktif debug modları ve hassas loglama
- **Bağımlılık Açığı** — Bilinen açıklara sahip paket versiyonları
- **İzin Hatası** — Aşırı geniş dosya/dizin izinleri

---

## 📤 Çıktı Formatları

### Terminal Çıktısı

Renkli, önem bazlı terminal çıktısı. Her açık için:

```
#1 🔴 Sabit Şifre Tespit Edildi [OTO-ONARILABİLİR]
   ID        : SEC-001-ca88a4
   Dosya     : app.py:18
   Kategori  : Sabit Gizli Veri
   Açıklama  : Kaynak kodda açık metin şifre bulundu.
   Kod       : password = "admin123"
   Çözüm     : os.environ.get("APP_PASSWORD") kullanın.
```

### HTML Raporu (`--html rapor.html`)

Dark-theme, profesyonel HTML raporu. İçerir:
- Özet istatistik kartları (toplam, kritik, yüksek, orta, düşük, onarıldı)
- Tüm açıkların önem sırasına göre sıralanmış tablosu
- Onarım durumu rozetleri
- CWE/CVE referansları

### JSON Raporu (`--json rapor.json`)

CI/CD sistemleri ve diğer araçlarla entegrasyon için yapılandırılmış çıktı:

```json
{
  "scan_id": "F2764517",
  "timestamp": "2026-05-27 10:26:58",
  "target": "./projem",
  "stats": {
    "toplam": 15,
    "kritik": 6,
    "yüksek": 4,
    "orta": 5,
    "düşük": 0,
    "bilgi": 0,
    "otomatik_onarılabilir": 9,
    "onarıldı": 0
  },
  "vulnerabilities": [
    {
      "id": "SEC-001-ca88a4",
      "title": "Sabit Şifre Tespit Edildi",
      "severity": "KRİTİK",
      "category": "Sabit Gizli Veri",
      "file": "app.py",
      "line": 18,
      "code_snippet": "password = \"admin123\"",
      "description": "...",
      "fix_suggestion": "...",
      "auto_fixable": true,
      "fixed": false
    }
  ]
}
```

---

## 🔧 Otomatik Onarım

VulnGuard, 9 kural için dosyalarınızı otomatik olarak düzeltebilir.

### Onarım Önizleme (Dry-Run — Varsayılan)

```bash
python vulnerability_scanner.py . --fix
# veya açıkça:
python vulnerability_scanner.py . --fix --dry-run
```

Çıktı:
```
[DRY-RUN] app.py:18
  - password = "admin123"
  + password = os.environ.get("APP_PASSWORD", "")
```

Dosyalar **değiştirilmez**, sadece ne değişeceği gösterilir.

### Gerçek Onarım

```bash
python vulnerability_scanner.py . --fix --no-dry-run
```

> ⚠️ **Dikkat:** Bu komut kaynak dosyalarınızı doğrudan değiştirir. Önce versiyon kontrol sisteminize (git) commit edin.

### Otomatik Onarım Tablosu

| Kural | Yapılan Onarım |
|---|---|
| SEC-001 | `password = "..."` → `password = os.environ.get("APP_PASSWORD", "")` |
| SEC-002 | `api_key = "..."` → `api_key = os.environ.get("API_KEY", "")` |
| SEC-004 | `shell=True` → `shell=False` |
| SEC-005 | `hashlib.md5(` → `hashlib.sha256(` |
| SEC-009 | `random.randint(` → `secrets.randint(` |
| SEC-010 | `debug=True` → `debug=False` |
| SEC-013 | `verify=False` → `verify=True` |
| SEC-015 | `chmod(path, 0o777)` → `chmod(path, 0o600)` |

---

## ⚙️ CI/CD Entegrasyonu

VulnGuard, CI/CD pipeline'larıyla uyumlu çıkış kodları döndürür:

| Çıkış Kodu | Anlam |
|---|---|
| `0` | Hiçbir açık bulunamadı — temiz |
| `1` | Açık bulundu ancak kritik değil |
| `2` | En az bir KRİTİK açık bulundu — build başarısız |

### GitHub Actions

```yaml
name: Güvenlik Taraması

on: [push, pull_request]

jobs:
  vulnguard:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Python Kur
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'

      - name: VulnGuard ile Tara
        run: |
          python vulnerability_scanner.py . \
            --min-severity YÜKSEK \
            --json guvenlik-raporu.json \
            --html guvenlik-raporu.html

      - name: Raporu Artifact Olarak Yükle
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: vulnguard-raporu
          path: |
            guvenlik-raporu.json
            guvenlik-raporu.html
```

### GitLab CI

```yaml
security-scan:
  stage: test
  script:
    - python vulnerability_scanner.py . --json rapor.json --html rapor.html
  artifacts:
    when: always
    paths:
      - rapor.json
      - rapor.html
  allow_failure: false
```

### Pre-commit Hook

```bash
# .git/hooks/pre-commit
#!/bin/bash
echo "🛡 VulnGuard güvenlik taraması çalışıyor..."
python vulnerability_scanner.py . --min-severity YÜKSEK
if [ $? -eq 2 ]; then
  echo "❌ KRİTİK güvenlik açığı tespit edildi. Commit engellendi."
  exit 1
fi
echo "✅ Tarama temiz."
```

---

## 💡 Örnekler

### Örnek 1 — Tek Dosya, Sadece Kritikler

```bash
python vulnerability_scanner.py app.py --min-severity KRİTİK
```

### Örnek 2 — Proje Tarama + Tam Rapor

```bash
python vulnerability_scanner.py ./backend \
  --html rapor.html \
  --json rapor.json \
  --verbose
```

### Örnek 3 — Onar ve Raporla

```bash
# Önce dry-run ile kontrol et
python vulnerability_scanner.py . --fix

# Onaylıyorsan gerçekten onar
python vulnerability_scanner.py . --fix --no-dry-run --json sonuc.json
```

### Örnek 4 — Savunmasız Kod ve Düzeltmesi

**Tespit edilen kod:**
```python
# ❌ Güvensiz
password = "admin123"
hashlib.md5(password.encode())
subprocess.run(f"ping {host}", shell=True)
requests.get(url, verify=False)
```

**VulnGuard sonrası:**
```python
# ✅ Güvenli
password = os.environ.get("APP_PASSWORD", "")
hashlib.sha256(password.encode())
subprocess.run(["ping", host], shell=False)
requests.get(url, verify=True)
```

---

## 📁 Proje Yapısı

```
vulnguard/
│
├── vulnerability_scanner.py   # Ana tarayıcı (tek dosya, bağımlılıksız)
├── README.md                  # Bu dosya
├── vulnguard_report.html      # Örnek HTML raporu
└── vulnguard_report.json      # Örnek JSON raporu
```

### Kod Mimarisi

```
vulnerability_scanner.py
│
├── Color                  # Terminal renk kodları
├── Severity (Enum)        # KRİTİK / YÜKSEK / ORTA / DÜŞÜK / BİLGİ
├── Category (Enum)        # 10 güvenlik kategorisi
├── Vulnerability          # Güvenlik açığı veri yapısı (@dataclass)
├── ScanResult             # Tarama sonucu veri yapısı (@dataclass)
│
├── RULES (List[Dict])     # 15 güvenlik kuralı tanımı
│
├── VulnerabilityScanner   # Tarama motoru
│   ├── scan_file()        # Tek dosya tarama
│   └── scan_directory()   # Dizin tarama
│
├── VulnerabilityFixer     # Otomatik onarım motoru
│   ├── fix_vulnerability()# Tek açık onarımı
│   └── fix_all()          # Toplu onarım
│
├── ReportGenerator        # Rapor üretici
│   ├── print_banner()     # Terminal başlığı
│   ├── print_summary()    # Özet istatistik
│   ├── print_vulnerabilities() # Detaylı liste
│   ├── export_json()      # JSON raporu
│   └── export_html()      # HTML raporu
│
└── main()                 # CLI giriş noktası (argparse)
```

---

## 🔒 Güvenlik Notu

VulnGuard **statik analiz** aracıdır. Bu şu anlama gelir:

- **Yanlış pozitifler** üretebilir — Tespit edilen her açık gerçek risk taşımayabilir.
- **Yanlış negatifler** mümkündür — Her güvenlik açığını tespit edemeyebilir.
- **Dinamik analiz değildir** — Çalışma zamanı davranışlarını analiz etmez.
- **Tam güvenlik değerlendirmesinin yerini tutmaz** — Penetrasyon testi ve kod incelemesini tamamlayıcı niteliktedir.

---

## 🤝 Katkıda Bulunma

Yeni kural eklemek için `RULES` listesine şu yapıda bir sözlük ekleyin:

```python
{
    "id": "SEC-016",
    "title": "Yeni Güvenlik Kuralı",
    "pattern": r'tehlikeli_fonksiyon\s*\(',        # Regex deseni
    "category": Category.INJECTION,
    "severity": Severity.HIGH,
    "description": "Bu fonksiyon şu riski taşır...",
    "fix": "Bunun yerine güvenli_fonksiyon() kullanın.",
    "auto_fixable": True,                          # Opsiyonel
    "fix_regex": (r'tehlikeli_fonksiyon', 'güvenli_fonksiyon'),  # Opsiyonel
    "cve": "CWE-XXX",                             # Opsiyonel
}
```

---

## 📜 Lisans

MIT Lisansı — Serbest kullanım, değiştirme ve dağıtım.

---

<div align="center">
  <strong>VulnGuard</strong> — Güvenli kod, güvenli gelecek. 🛡
</div>
