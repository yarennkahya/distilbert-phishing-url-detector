# DistilBERT Phishing URL Detector

Phishing URL'lerini tespit etmek için DistilBERT derin öğrenme modelini kullanan bir proje.

## Proje Açıklaması

Bu proje, DistilBERT (BERT'in hafif versiyonu) transformer modelini kullanarak URL'lerin phishing olup olmadığını sınıflandırır. Model, URL metinsel özelliklerini analiz ederek yüksek doğruluk oranı ile tehditli siteleri tanımlamaya yardımcı olur.

## Özellikler

- DistilBERT transformer mimarisi kullanan derin öğrenme modeli
- GPU desteği (CUDA) ile hızlı eğitim ve tahminleme
- Jupyter Notebook formatında kolay kullanılabilir kod
- Google Colab'da çalıştırmaya hazır
- Detaylı model değerlendirmesi ve metrikleri
- Düşük bellek kullanımı ve hızlı çıktı

## Kurulum ve Gereksinimler

### Gerekli Kütüphaneler

```bash
pip install torch transformers pandas numpy scikit-learn
```

### Gereksinimler

- Python 3.7+
- PyTorch
- Hugging Face Transformers
- Pandas, NumPy, Scikit-learn

### Google Colab'da Kurulum

Colab'da GPU etkinleştirin: Runtime > Change Runtime Type > GPU

```python
!pip install torch transformers pandas scikit-learn
```

## Kullanım Rehberi

### Temel Kullanım

```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification
import torch

# Modeli ve tokenizer'ı yükleyin
model_name = "distilbert-base-uncased"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForSequenceClassification.from_pretrained(model_name, num_labels=2)

# URL'yi tokenize edin
url = "https://example.com"
inputs = tokenizer(url, return_tensors="pt")

# Tahmin yapın
outputs = model(**inputs)
predictions = torch.softmax(outputs.logits, dim=1)
```

### Google Colab'da Çalıştırma

1. `distilbert_phishing_url_detector.ipynb` dosyasını açın
2. Google Colab'da açın
3. GPU etkinleştirin
4. Hücreleri sırasıyla çalıştırın

### Yerel Ortamda Çalıştırma

```bash
jupyter notebook distilbert_phishing_url_detector.ipynb
```

## Model Yapısı

DistilBERT modeli şu bileşenlerden oluşur:

- Embedding Layer: URL metinini vektörlere dönüştürür
- Transformer Blocks: 6 transformer katmanı ile işleme
- Classification Head: İkili sınıflandırma (Phishing/Legitimate)

Model, BERT'in parametrelerinin %40'ını kullanırken benzer performans gösterir.

## Teknik Detaylar

| Parametre | Değer |
|-----------|-------|
| Model | distilbert-base-uncased |
| Maksimum Token Uzunluğu | 512 |
| Batch Size | 32 |
| Learning Rate | 2e-5 |
| Epoch Sayısı | 3-5 |
| Optimizer | AdamW |
| Loss Function | CrossEntropyLoss |

## Performans Metrikleri

- Doğruluk (Accuracy): ~95%
- Hassasiyet (Precision): ~94%
- Geri Çağırma (Recall): ~96%
- F1 Skoru: ~95%

Not: Metrikler test setinde ölçülmüştür.

## Uyarılar ve Sınırlamalar

- Model eğitim sırasında görmediği URL'lerde performans düşebilir
- Yalnızca İngilizce URL'ler için optimize edilmiştir
- Gerçek zamanlı phishing tespiti için ek güvenlik katmanları önerilir
- Model güncellemeleri ve yeniden eğitim gerekebilir

## Proje Yapısı

```
distilbert-phishing-url-detector/
├── distilbert_phishing_url_detector.ipynb  # Ana Jupyter Notebook
├── README.md                                 # Bu dosya
└── requirements.txt                          # (Opsiyonel) Bağımlılıklar
```

## Yararlı Kaynaklar

- [Hugging Face Transformers](https://huggingface.co/transformers/)
- [DistilBERT Dokümantasyonu](https://huggingface.co/docs/transformers/model_doc/distilbert)
- [PyTorch Resmi Sitesi](https://pytorch.org/)
- [BERT Orijinal Makalesi](https://arxiv.org/abs/1810.04805)
- [DistilBERT Makalesi](https://arxiv.org/abs/1910.01108)
