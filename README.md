# EEM4011 — Sentetik EKG'de Gürültü ve R-Tepe Tespiti

## Projenin Amacı

Bu projede, sentetik EKG sinyallerine 50 Hz şebeke paraziti ve taban çizgisi kayması ekleyerek bu bozucu etkilerin kalp hızı ölçümünü nasıl etkilediğini incelemeyi amaçladım.

Kalp hızını hesaplamak için genlik eşiğine dayalı D1 yöntemi ile türev enerjisine dayalı D2 yöntemini karşılaştırdım.

Ayrıca 50 Hz notch filtresi uygulayarak filtreleme öncesi ve sonrasındaki ölçüm hatalarını değerlendirdim.

## Yöntem

Bu projede ECGSYN modeli kullanılarak 15 sentetik EKG kaydı üretilmiştir.

- Hedef kalp hızları: 60, 80 ve 100 bpm
- Kayıt süresi: 60 saniye
- Örnekleme frekansı: 500 Hz
- Eklenen parazitler: 50 Hz şebeke girişimi ve 0.3 Hz taban çizgisi kayması
- D1: Genlik eşiğine dayalı R-tepe tespiti
- D2: Türev enerjisine dayalı R-tepe tespiti

Her iki yöntem, 50 Hz notch filtresi uygulanmadan önce ve uygulandıktan sonra karşılaştırılmıştır.

## Nasıl Çalıştırılır?

1. `EEM4011_ECG_Projesi.ipynb` dosyasını Google Colab'da açın.
2. **Çalışma zamanı → Tümünü çalıştır** seçeneğini kullanın.
3. İlk hücre gerekli Python paketlerini kurar.
4. Diğer hücreler sentetik EKG sinyallerini üretir, analiz eder ve sonuç dosyalarını oluşturur.

Harici EKG veri dosyası indirmek gerekmez. Sinyaller kod tarafından üretilir.

## Üretilen Dosyalar

| Dosya | Açıklama |
|---|---|
| `sekil1_kesit.png` | Temiz ve parazitli EKG kesitlerinin karşılaştırılması |
| `sekil2_welch.png` | Welch yöntemiyle güç spektral yoğunluğu karşılaştırması |
| `tablo_asama2.csv` | Filtresiz D1 ve D2 hata sonuçları |
| `tablo_asama2_filtreli.csv` | Notch filtreli D1 ve D2 hata sonuçları |

## Sonuçlar

15 kayıt üzerinden hesaplanan ortalama mutlak hata (MAE) değerleri:

| Yöntem | Ortalama mutlak hata (bpm) |
|---|---:|
| D1 — Filtresiz | 19.259 |
| D2 — Filtresiz | 0.032 |
| D1 — Filtreli | 6.645 |
| D2 — Filtreli | 0.000 |

Not: Değerler üç ondalık basamağa yuvarlanmıştır.

Deney sonuçlarında D2 yöntemi, hem filtreli hem de filtresiz sinyallerde D1 yönteminden daha düşük ortalama kalp hızı hatası vermiştir. 50 Hz notch filtresi, D1 yönteminin hatasını azaltmış; D2 yönteminin hatası ise filtreleme öncesinde de oldukça düşük kalmıştır. Bu sonuçlar, kullanılan sentetik EKG sinyalleri ve seçilen parazit seviyeleri için D2 yönteminin daha başarılı olduğunu göstermektedir.

## Çalışma Ortamı

- Python 3.13.16
- NeuroKit2 0.2.13
- WFDB 4.3.1
- Google Colab
- Baştan sona testte ölçülen çalışma süresi: 37.14 saniye

Çalışma süresi kullanılan ortama göre değişebilir.

## Kaynaklar

- McSharry, P. E. ve ark. (2003). *A Dynamical Model for Generating Synthetic Electrocardiogram Signals*. IEEE Transactions on Biomedical Engineering. https://doi.org/10.1109/TBME.2003.808805
- Makowski, D. ve ark. (2021). *NeuroKit2: A Python toolbox for neurophysiological signal processing*. Behavior Research Methods. https://doi.org/10.3758/s13428-020-01516-y

## Lisans

Bu projenin kodları MIT lisansı altında paylaşılacaktır. Lisans koşulları `LICENSE` dosyasında belirtilecektir.
