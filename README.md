# Ses Verileri İçin Sinyal İşleme ve Öznitelik Çıkarımı
## Yapılan Teknik Çalışmalar### Veri Ön İşleme ve Gürültü Temizleme
RAVDESS veri seti, aktör bazlı (Actor-Independent) eğitim stratejisine uygun olarak train, test ve val klasörlerine ayrıştırılmıştır.

Sinyal Dönüşümü: Ham .wav dosyaları Librosa kütüphanesi ile 22.050 Hz örnekleme hızında bilgisayar ortamında işlenebilir dijital sinyallere dönüştürülmüştür.
![Sinyal](https://github.com/Uygulama-Tasarimi-Projesi/Ses-Verileri-Icin-Sinyal-Isleme-Oznitelik-Cikarimi/blob/main/sinyal.png)
Sessiz Bölüm Temizliği (Trimming): librosa.effects.trim kullanılarak sesin başındaki ve sonundaki gürültülü sessiz kısımlar atılarak sadece aktif sinyal izole edilmiştir.
Normalizasyon: Tüm sinyaller, genlik seviyelerini eşitlemek amacıyla [-1, 1] aralığına normalize edilmiştir.

Kullanılan Normalizasyon Formülü:
Veri Seti Yapısı:
## Akustik Öznitelik Çıkarımı (Feature Extraction)
Temizlenen sinyallerden, duyguyu en iyi temsil eden akustik öznitelikler çıkarılarak CNN mimarisinin işleyebileceği 2 boyutlu matrislere dönüştürülmüştür:

Mel-Spektrogram: Sesin frekans dünyasındaki izdüşümü 128 farklı frekans bandında oluşturulmuş ve logaritmik enerji (dB) ölçeğine dönüştürülmüştür.
![MelSpektrogram](https://github.com/Uygulama-Tasarimi-Projesi/Ses-Verileri-Icin-Sinyal-Isleme-Oznitelik-Cikarimi/blob/main/melspektrogram.png)
MFCC: Sesin tınısal parmak izini ve vurgu karakteristiğini temsil eden 40 adet Mel-Frekans Kepstral Katsayısı hesaplanmıştır.
![MFCC](https://github.com/Uygulama-Tasarimi-Projesi/Ses-Verileri-Icin-Sinyal-Isleme-Oznitelik-Cikarimi/blob/main/mfcc.png)
## Ses-Görüntü Dönüşümü 
Tüm öznitelikler, model eğitimi sırasında işlem hızını ve verimliliği artırmak amacıyla NumPy'ın sıkıştırılmış ikili (binary) formatı olan .npz dosyaları halinde saklanmıştır.
