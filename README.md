# 馃洝 VulnGuard

> **Python G眉venlik A莽谋臒谋 Taray谋c谋, S谋n谋fland谋r谋c谋 ve Onar谋c谋**  
> Kaynak kodunuzdaki g眉venlik a莽谋klar谋n谋 tespit edin, s谋n谋fland谋r谋n ve otomatik olarak onar谋n.

---

## 馃搵 陌莽indekiler

- [Genel Bak谋艧](#-genel-bak谋艧)
- [脰zellikler](#-枚zellikler)
- [Kurulum](#-kurulum)
- [H谋zl谋 Ba艧lang谋莽](#-h谋zl谋-ba艧lang谋莽)
- [Kullan谋m](#-kullan谋m)
- [G眉venlik Kurallar谋](#-g眉venlik-kurallar谋)
- [脟谋kt谋 Formatlar谋](#-莽谋kt谋-formatlar谋)
- [Otomatik Onar谋m](#-otomatik-onar谋m)
- [CI/CD Entegrasyonu](#-cicd-entegrasyonu)
- [脰rnekler](#-枚rnekler)
- [Proje Yap谋s谋](#-proje-yap谋s谋)
- [Katk谋da Bulunma](#-katk谋da-bulunma)
- [Lisans](#-lisans)

---

## 馃攳 Genel Bak谋艧

VulnGuard, Python kaynak kodlar谋n谋, konfig眉rasyon dosyalar谋n谋 ve ba臒谋ml谋l谋k tan谋mlar谋n谋 statik analiz y枚ntemiyle tarayan bir g眉venlik arac谋d谋r. Herhangi bir harici servis veya kurulum gerektirmez; tamamen yerel 莽al谋艧谋r.

**Temel felsefesi:** G眉venlik a莽谋klar谋n谋 sadece tespit etmekle kalmaz, her a莽谋k i莽in:
- 馃搶 Tam konum bilgisi (dosya + sat谋r numaras谋)
- 馃彿 脰nem seviyesi ve kategori s谋n谋fland谋rmas谋
- 馃摉 陌nsan okunabilir a莽谋klama
- 馃挕 Somut 莽枚z眉m 枚nerisi
- 馃敡 M眉mk眉nse otomatik kod onar谋m谋

sa臒lar.

---

## 鉁� 脰zellikler

| 脰zellik | A莽谋klama |
|---|---|
| 馃攷 **Statik Analiz** | Regex tabanl谋 15 g眉venlik kural谋 ile kaynak kod taramas谋 |
| 馃彿 **S谋n谋fland谋rma** | 5 枚nem seviyesi (Kritik 鈫� Bilgi) ve 10 kategori |
| 馃敡 **Otomatik Onar谋m** | 9 kural i莽in tek komutla otomatik kod d眉zeltmesi |
| 馃И **Dry-Run Modu** | Dosyalar谋 de臒i艧tirmeden onar谋m 枚nizlemesi |
| 馃搫 **HTML Raporu** | Dark-theme, profesyonel g枚rsel rapor |
| 馃搳 **JSON Raporu** | CI/CD sistemleriyle entegrasyon i莽in makine okunabilir 莽谋kt谋 |
| 馃帹 **Renkli Terminal** | ANSI renk kodlar谋yla 枚nem bazl谋 renkli terminal 莽谋kt谋s谋 |
| 馃搧 **Dizin Tarama** | T眉m proje dizinini tek komutla tara |
| 馃殾 **CI/CD 脟谋k谋艧 Kodlar谋** | Kritik a莽谋k varsa exit(2), di臒er a莽谋klar exit(1) |
| 馃攪 **Ak谋ll谋 Hari莽 Tutma** | `.venv`, `__pycache__`, `.git` gibi dizinleri otomatik atlar |

---

## 馃摝 Kurulum

VulnGuard, Python standart k眉t眉phanesini kullan谋r. Ek ba臒谋ml谋l谋k gerektirmez.

**Gereksinim:** Python 3.7+

```bash
# Depoyu klonlay谋n
git clone https://github.com/Mystery-Master/Securty-scanner-and-fixer.git
cd Securty-scanner-and-fixer.git


# Do臒rudan 莽al谋艧t谋r谋n (ba臒谋ml谋l谋k yok!)
python vulnerability_scanner.py --help
```

陌ste臒e ba臒l谋 olarak 莽al谋艧t谋r谋labilir yapabilirsiniz:

```bash
chmod +x vulnerability_scanner.py
./vulnerability_scanner.py .
```

---

## 馃殌 H谋zl谋 Ba艧lang谋莽

```bash
# Mevcut dizini tara
python vulnerability_scanner.py .

# Tek bir dosyay谋 tara
python vulnerability_scanner.py myapp.py

# Tara ve HTML + JSON raporu 眉ret
python vulnerability_scanner.py . --html rapor.html --json rapor.json

# Otomatik onar谋mlar谋 枚nizle
python vulnerability_scanner.py . --fix

# Otomatik onar谋mlar谋 ger莽ekten uygula
python vulnerability_scanner.py . --fix --no-dry-run
```

---

## 馃摉 Kullan谋m

```
kullan谋m: vulnerability_scanner.py [se莽enekler] [hedef]

Konumsal Arg眉manlar:
  target                Taranacak dosya veya dizin yolu (varsay谋lan: .)

Se莽enekler:
  -h, --help            Yard谋m mesaj谋n谋 g枚ster ve 莽谋k
  --fix                 Otomatik onar谋labilir a莽谋klar谋 onar
  --dry-run             Onar谋mlar谋 ger莽ekle艧tirmeden g枚ster (varsay谋lan: a莽谋k)
  --no-dry-run          Onar谋mlar谋 ger莽ekten uygula (dosyalar谋 de臒i艧tirir!)
  --json DOSYA          Raporu JSON olarak kaydet
  --html DOSYA          Raporu HTML olarak kaydet
  --verbose, -v         Ayr谋nt谋l谋 莽谋kt谋 (tarama s谋ras谋, e艧le艧meler)
  --min-severity SEV陌YE Minimum 枚nem filtresi: KR陌T陌K|Y脺KSEK|ORTA|D脺艦脺K|B陌LG陌
```

### Tarama Hedefleri

```bash
# Tek Python dosyas谋
python vulnerability_scanner.py app.py

# T眉m proje dizini
python vulnerability_scanner.py /projem/

# Mevcut dizin
python vulnerability_scanner.py .
```

Varsay谋lan olarak 艧u uzant谋l谋 dosyalar taran谋r: `.py` `.cfg` `.ini` `.env` `.yaml` `.yml` `.json`

---

## 馃攼 G眉venlik Kurallar谋

VulnGuard 15 g眉venlik kural谋 i莽erir. Her kural bir ID, ba艧l谋k, 枚nem seviyesi ve kategori ile tan谋mlan谋r.

### Kural Tablosu

| ID | Ba艧l谋k | 脰nem | Kategori | Oto-Onar谋m | CWE/CVE |
|---|---|---|---|---|---|
| SEC-001 | Sabit 艦ifre | 馃敶 KR陌T陌K | Sabit Gizli Veri | 鉁� | 鈥� |
| SEC-002 | Sabit API Anahtar谋 | 馃敶 KR陌T陌K | Sabit Gizli Veri | 鉁� | 鈥� |
| SEC-003 | SQL Enjeksiyonu | 馃煚 Y脺KSEK | Enjeksiyon | 鉂� | CWE-89 |
| SEC-004 | shell=True Komutu | 馃煚 Y脺KSEK | Komut Enjeksiyonu | 鉁� | 鈥� |
| SEC-005 | MD5/SHA1 Hash | 馃煛 ORTA | G眉vensiz Kriptografi | 鉁� | 鈥� |
| SEC-006 | DES/3DES 艦ifreleme | 馃煚 Y脺KSEK | G眉vensiz Kriptografi | 鉂� | 鈥� |
| SEC-007 | pickle.loads | 馃敶 KR陌T陌K | G眉vensiz Serimleme | 鉂� | CWE-502 |
| SEC-008 | Yol Ge莽i艧i | 馃煚 Y脺KSEK | Path Traversal | 鉂� | CWE-22 |
| SEC-009 | Zay谋f random | 馃煛 ORTA | G眉vensiz Rastgele Say谋 | 鉁� | 鈥� |
| SEC-010 | debug=True | 馃煚 Y脺KSEK | Debug Kodu | 鉁� | 鈥� |
| SEC-011 | Hassas Veri Loglama | 馃煛 ORTA | Debug Kodu | 鉂� | 鈥� |
| SEC-012 | eval/exec Kullan谋m谋 | 馃敶 KR陌T陌K | Enjeksiyon | 鉂� | CWE-78 |
| SEC-013 | SSL verify=False | 馃煚 Y脺KSEK | G眉vensiz Kriptografi | 鉁� | 鈥� |
| SEC-014 | XML XXE Riski | 馃煛 ORTA | Enjeksiyon | 鉂� | CWE-611 |
| SEC-015 | Geni艧 Dosya 陌zni | 馃煛 ORTA | 陌zin Hatas谋 | 鉁� | 鈥� |

### 脰nem Seviyeleri

```
馃敶 KR陌T陌K  鈥� An谋nda m眉dahale gerektirir. Uzaktan kod 莽al谋艧t谋rma, kimlik bilgisi s谋z谋nt谋s谋.
馃煚 Y脺KSEK  鈥� Yak谋n vadede d眉zeltilmeli. Enjeksiyon, kimlik do臒rulama sorunlar谋.
馃煛 ORTA    鈥� Planl谋 geli艧tirme s眉recinde ele al谋nmal谋. Zay谋f kriptografi, loglama.
馃煝 D脺艦脺K   鈥� En iyi pratiklerden sapma. Acil risk yok.
馃數 B陌LG陌   鈥� Bilgilendirme ama莽l谋. Risk i莽ermeyebilir.
```

### Kategoriler

- **Enjeksiyon** 鈥� SQL, komut, eval, XXE enjeksiyonlar谋
- **Sabit Gizli Veri** 鈥� Kodda g枚m眉l眉 艧ifre, token ve API anahtarlar谋
- **G眉vensiz Kriptografi** 鈥� Zay谋f hash ve 艧ifreleme algoritmalar谋, SSL sorunlar谋
- **G眉vensiz Serimleme** 鈥� pickle, YAML y眉kleyici g眉venlik sorunlar谋
- **Path Traversal** 鈥� Kullan谋c谋 girdisiyle kontrol edilen dosya yollar谋
- **Komut Enjeksiyonu** 鈥� shell=True ile komut 莽al谋艧t谋rma
- **G眉vensiz Rastgele Say谋** 鈥� Kriptografik ama莽l谋 zay谋f random kullan谋m谋
- **Debug Kodu** 鈥� 脺retimde aktif debug modlar谋 ve hassas loglama
- **Ba臒谋ml谋l谋k A莽谋臒谋** 鈥� Bilinen a莽谋klara sahip paket versiyonlar谋
- **陌zin Hatas谋** 鈥� A艧谋r谋 geni艧 dosya/dizin izinleri

---

## 馃摛 脟谋kt谋 Formatlar谋

### Terminal 脟谋kt谋s谋

Renkli, 枚nem bazl谋 terminal 莽谋kt谋s谋. Her a莽谋k i莽in:

```
#1 馃敶 Sabit 艦ifre Tespit Edildi [OTO-ONARILAB陌L陌R]
   ID        : SEC-001-ca88a4
   Dosya     : app.py:18
   Kategori  : Sabit Gizli Veri
   A莽谋klama  : Kaynak kodda a莽谋k metin 艧ifre bulundu.
   Kod       : password = "admin123"
   脟枚z眉m     : os.environ.get("APP_PASSWORD") kullan谋n.
```

### HTML Raporu (`--html rapor.html`)

Dark-theme, profesyonel HTML raporu. 陌莽erir:
- 脰zet istatistik kartlar谋 (toplam, kritik, y眉ksek, orta, d眉艧眉k, onar谋ld谋)
- T眉m a莽谋klar谋n 枚nem s谋ras谋na g枚re s谋ralanm谋艧 tablosu
- Onar谋m durumu rozetleri
- CWE/CVE referanslar谋

### JSON Raporu (`--json rapor.json`)

CI/CD sistemleri ve di臒er ara莽larla entegrasyon i莽in yap谋land谋r谋lm谋艧 莽谋kt谋:

```json
{
  "scan_id": "F2764517",
  "timestamp": "2026-05-27 10:26:58",
  "target": "./projem",
  "stats": {
    "toplam": 15,
    "kritik": 6,
    "y眉ksek": 4,
    "orta": 5,
    "d眉艧眉k": 0,
    "bilgi": 0,
    "otomatik_onar谋labilir": 9,
    "onar谋ld谋": 0
  },
  "vulnerabilities": [
    {
      "id": "SEC-001-ca88a4",
      "title": "Sabit 艦ifre Tespit Edildi",
      "severity": "KR陌T陌K",
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

## 馃敡 Otomatik Onar谋m

VulnGuard, 9 kural i莽in dosyalar谋n谋z谋 otomatik olarak d眉zeltebilir.

### Onar谋m 脰nizleme (Dry-Run 鈥� Varsay谋lan)

```bash
python vulnerability_scanner.py . --fix
# veya a莽谋k莽a:
python vulnerability_scanner.py . --fix --dry-run
```

脟谋kt谋:
```
[DRY-RUN] app.py:18
  - password = "admin123"
  + password = os.environ.get("APP_PASSWORD", "")
```

Dosyalar **de臒i艧tirilmez**, sadece ne de臒i艧ece臒i g枚sterilir.

### Ger莽ek Onar谋m

```bash
python vulnerability_scanner.py . --fix --no-dry-run
```

> 鈿狅笍 **Dikkat:** Bu komut kaynak dosyalar谋n谋z谋 do臒rudan de臒i艧tirir. 脰nce versiyon kontrol sisteminize (git) commit edin.

### Otomatik Onar谋m Tablosu

| Kural | Yap谋lan Onar谋m |
|---|---|
| SEC-001 | `password = "..."` 鈫� `password = os.environ.get("APP_PASSWORD", "")` |
| SEC-002 | `api_key = "..."` 鈫� `api_key = os.environ.get("API_KEY", "")` |
| SEC-004 | `shell=True` 鈫� `shell=False` |
| SEC-005 | `hashlib.md5(` 鈫� `hashlib.sha256(` |
| SEC-009 | `random.randint(` 鈫� `secrets.randint(` |
| SEC-010 | `debug=True` 鈫� `debug=False` |
| SEC-013 | `verify=False` 鈫� `verify=True` |
| SEC-015 | `chmod(path, 0o777)` 鈫� `chmod(path, 0o600)` |

---

## 鈿欙笍 CI/CD Entegrasyonu

VulnGuard, CI/CD pipeline'lar谋yla uyumlu 莽谋k谋艧 kodlar谋 d枚nd眉r眉r:

| 脟谋k谋艧 Kodu | Anlam |
|---|---|
| `0` | Hi莽bir a莽谋k bulunamad谋 鈥� temiz |
| `1` | A莽谋k bulundu ancak kritik de臒il |
| `2` | En az bir KR陌T陌K a莽谋k bulundu 鈥� build ba艧ar谋s谋z |

### GitHub Actions

```yaml
name: G眉venlik Taramas谋

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
            --min-severity Y脺KSEK \
            --json guvenlik-raporu.json \
            --html guvenlik-raporu.html

      - name: Raporu Artifact Olarak Y眉kle
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
echo "馃洝 VulnGuard g眉venlik taramas谋 莽al谋艧谋yor..."
python vulnerability_scanner.py . --min-severity Y脺KSEK
if [ $? -eq 2 ]; then
  echo "鉂� KR陌T陌K g眉venlik a莽谋臒谋 tespit edildi. Commit engellendi."
  exit 1
fi
echo "鉁� Tarama temiz."
```

---

## 馃挕 脰rnekler

### 脰rnek 1 鈥� Tek Dosya, Sadece Kritikler

```bash
python vulnerability_scanner.py app.py --min-severity KR陌T陌K
```

### 脰rnek 2 鈥� Proje Tarama + Tam Rapor

```bash
python vulnerability_scanner.py ./backend \
  --html rapor.html \
  --json rapor.json \
  --verbose
```

### 脰rnek 3 鈥� Onar ve Raporla

```bash
# 脰nce dry-run ile kontrol et
python vulnerability_scanner.py . --fix

# Onayl谋yorsan ger莽ekten onar
python vulnerability_scanner.py . --fix --no-dry-run --json sonuc.json
```

### 脰rnek 4 鈥� Savunmas谋z Kod ve D眉zeltmesi

**Tespit edilen kod:**
```python
# 鉂� G眉vensiz
password = "admin123"
hashlib.md5(password.encode())
subprocess.run(f"ping {host}", shell=True)
requests.get(url, verify=False)
```

**VulnGuard sonras谋:**
```python
# 鉁� G眉venli
password = os.environ.get("APP_PASSWORD", "")
hashlib.sha256(password.encode())
subprocess.run(["ping", host], shell=False)
requests.get(url, verify=True)
```

---

## 馃搧 Proje Yap谋s谋

```
vulnguard/
鈹�
鈹溾攢鈹€ vulnerability_scanner.py   # Ana taray谋c谋 (tek dosya, ba臒谋ml谋l谋ks谋z)
鈹溾攢鈹€ README.md                  # Bu dosya
鈹溾攢鈹€ vulnguard_report.html      # 脰rnek HTML raporu
鈹斺攢鈹€ vulnguard_report.json      # 脰rnek JSON raporu
```

### Kod Mimarisi

```
vulnerability_scanner.py
鈹�
鈹溾攢鈹€ Color                  # Terminal renk kodlar谋
鈹溾攢鈹€ Severity (Enum)        # KR陌T陌K / Y脺KSEK / ORTA / D脺艦脺K / B陌LG陌
鈹溾攢鈹€ Category (Enum)        # 10 g眉venlik kategorisi
鈹溾攢鈹€ Vulnerability          # G眉venlik a莽谋臒谋 veri yap谋s谋 (@dataclass)
鈹溾攢鈹€ ScanResult             # Tarama sonucu veri yap谋s谋 (@dataclass)
鈹�
鈹溾攢鈹€ RULES (List[Dict])     # 15 g眉venlik kural谋 tan谋m谋
鈹�
鈹溾攢鈹€ VulnerabilityScanner   # Tarama motoru
鈹�   鈹溾攢鈹€ scan_file()        # Tek dosya tarama
鈹�   鈹斺攢鈹€ scan_directory()   # Dizin tarama
鈹�
鈹溾攢鈹€ VulnerabilityFixer     # Otomatik onar谋m motoru
鈹�   鈹溾攢鈹€ fix_vulnerability()# Tek a莽谋k onar谋m谋
鈹�   鈹斺攢鈹€ fix_all()          # Toplu onar谋m
鈹�
鈹溾攢鈹€ ReportGenerator        # Rapor 眉retici
鈹�   鈹溾攢鈹€ print_banner()     # Terminal ba艧l谋臒谋
鈹�   鈹溾攢鈹€ print_summary()    # 脰zet istatistik
鈹�   鈹溾攢鈹€ print_vulnerabilities() # Detayl谋 liste
鈹�   鈹溾攢鈹€ export_json()      # JSON raporu
鈹�   鈹斺攢鈹€ export_html()      # HTML raporu
鈹�
鈹斺攢鈹€ main()                 # CLI giri艧 noktas谋 (argparse)
```

---

## 馃敀 G眉venlik Notu

VulnGuard **statik analiz** arac谋d谋r. Bu 艧u anlama gelir:

- **Yanl谋艧 pozitifler** 眉retebilir 鈥� Tespit edilen her a莽谋k ger莽ek risk ta艧谋mayabilir.
- **Yanl谋艧 negatifler** m眉mk眉nd眉r 鈥� Her g眉venlik a莽谋臒谋n谋 tespit edemeyebilir.
- **Dinamik analiz de臒ildir** 鈥� 脟al谋艧ma zaman谋 davran谋艧lar谋n谋 analiz etmez.
- **Tam g眉venlik de臒erlendirmesinin yerini tutmaz** 鈥� Penetrasyon testi ve kod incelemesini tamamlay谋c谋 niteliktedir.

---

## 馃 Katk谋da Bulunma

Yeni kural eklemek i莽in `RULES` listesine 艧u yap谋da bir s枚zl眉k ekleyin:

```python
{
    "id": "SEC-016",
    "title": "Yeni G眉venlik Kural谋",
    "pattern": r'tehlikeli_fonksiyon\s*\(',        # Regex deseni
    "category": Category.INJECTION,
    "severity": Severity.HIGH,
    "description": "Bu fonksiyon 艧u riski ta艧谋r...",
    "fix": "Bunun yerine g眉venli_fonksiyon() kullan谋n.",
    "auto_fixable": True,                          # Opsiyonel
    "fix_regex": (r'tehlikeli_fonksiyon', 'g眉venli_fonksiyon'),  # Opsiyonel
    "cve": "CWE-XXX",                             # Opsiyonel
}
```

---

## 馃摐 Lisans

MIT Lisans谋 鈥� Serbest kullan谋m, de臒i艧tirme ve da臒谋t谋m.

---

<div align="center">
  <strong>VulnGuard</strong> 鈥� G眉venli kod, g眉venli gelecek. 馃洝
</div>
