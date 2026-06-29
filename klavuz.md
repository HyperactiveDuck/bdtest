# Bilgi Portali Kullanim Kilavuzu

Bu belgede, bilgi portalina nasil sekme (tabs), dosya baglantilari ve gorsel ekleyebileceginiz orneklerle aciklanmistir.

---

## 1. Sekmeler (Tabs) Ekleme

Sekme grubunu olusturmak icin `<!-- tabs:start -->` ve `<!-- tabs:end -->` etiketlerini kullanabilirsiniz. Sekme basliklarini `####` (h4 heading) olarak tanimlamaniz gerekir:

### Yazim Bicimi:
```markdown
<!-- tabs:start -->

#### **macOS**
Mac uzerinde kurulum adimlari...

#### **Windows**
Windows uzerinde kurulum adimlari...

#### **Linux**
Linux uzerinde kurulum adimlari...

<!-- tabs:end -->
```

### Canli Ornek:

<!-- tabs:start -->

#### **macOS**
```bash
brew install node
```

#### **Windows**
```powershell
choco install nodejs
```

#### **Linux**
```bash
sudo apt install nodejs
```

<!-- tabs:end -->

---

## 2. Dosya Yukleme ve Baglantilar

### Belgeler Arasi Baglanti Kurma
Farkli bir markdown belgesine baglanti vermek icin goreceli (relative) yollari kullanabilirsiniz:
```markdown
Buradan [Yedekleme Betigine](/betikler/backup.md) ulasabilirsiniz.
```
*Gorece:* Buradan [Yedekleme Betigine](/betikler/backup.md) ulasabilirsiniz.

### Indirilebilir Dosya Ekleme
Kullanicilarin indirmesini istediginiz dosyalari (PDF, script, zip vb.) `docs/` klasoru altinda (ornegin `docs/assets/files/`) konumlandirip doğrudan baglanti verebilirsiniz:
```markdown
Kurulum scriptini [buradan indirin](/assets/files/setup.sh).
```

---

## 3. Gorsel Ekleme

Gorselleri `docs/assets/images/` dizinine yerlestirip asagidaki yontemlerle sitenize ekleyebilirsiniz:

### Standart Markdown Yontemi
```markdown
![Gorsel Aciklamasi](/assets/images/logo.png)
```

### HTML Yonetimi (Genislik ve Yukseklik Belirlemek Icin)
```html
<img src="/assets/images/logo.png" width="300" alt="Kurumsal Logo" />
```

> **Not:** Sitede `zoom-image` eklentisi aktif oldugu icin eklediginiz gorsellere tiklandiginda otomatik olarak buyutulecektir.
