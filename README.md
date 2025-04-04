# HTTP Status Checker API

Bu API, URL'lerin HTTP durumunu kontrol etmek için tasarlanmış bir servistir. Yönlendirmeleri tespit eder ve her URL için status kodlarını döndürür.

## Özellikler

- URL'lerin HTTP durum kodlarını kontrol eder
- Yönlendirmeleri (301, 302, vb.) tespit eder
- Hatalar ve erişilemeyen URL'ler için bilgi verir
- Maksimum 100 URL'yi tek seferde işler

## Yerel Kurulum

```bash
# Repoyu klonlayın
git clone https://github.com/yourusername/http-status-checker.git
cd http-status-checker

# Sanal ortam oluşturun (opsiyonel ama önerilir)
python -m venv venv
source venv/bin/activate  # Linux/Mac için
# veya
venv\Scripts\activate  # Windows için

# Bağımlılıkları yükleyin
pip install -r requirements.txt

# Uygulamayı çalıştırın
python app.py
```

## API Kullanımı

### URL'leri Kontrol Etme

**Endpoint:** `/api/check-urls`
**Metod:** POST
**İçerik Tipi:** application/json

**Örnek İstek:**

```json
{
  "urls": [
    "https://example.com",
    "https://example.com/page1",
    "https://example.com/nonexistent"
  ]
}
```

**Örnek Yanıt:**

```json
[
  {
    "url": "https://example.com",
    "redirect_to": "https://example.com",
    "status": 200,
    "note": ""
  },
  {
    "url": "https://example.com/page1",
    "redirect_to": "https://example.com/newpage",
    "status": 301,
    "note": "Çözüm İçin Danış"
  },
  {
    "url": "https://example.com/nonexistent",
    "redirect_to": "https://example.com/nonexistent",
    "status": 404,
    "note": "Çözüm İçin Danış"
  }
]
```

## Dağıtım

Bu API, Railway, Heroku, PythonAnywhere veya diğer Python uygulama hosting platformlarında dağıtılabilir.

### Railway ile Dağıtım

1. GitHub'a kodu push edin
2. Railway'de yeni bir proje oluşturun
3. GitHub deposunu seçin
4. Otomatik dağıtımın tamamlanmasını bekleyin

## CORS

API, varsayılan olarak tüm domainlerden gelen isteklere izin verecek şekilde yapılandırılmıştır. Güvenlik için, üretim ortamında bu ayarı kendi domain adresinizle sınırlandırmanız önerilir. 