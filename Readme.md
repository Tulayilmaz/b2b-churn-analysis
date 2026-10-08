> ⚠️ **Not:** GitHub'ın Jupyter Notebook dosyalarını görüntülerken yaşadığı teknik sorunlar nedeniyle, kodları ve analiz çıktılarını (tablolar/skorlar) tam formatıyla görmek için lütfen aşağıdaki linke tıklayın:
> 
> 👉 **[Proje Notebook'unu Görüntüle (Nbviewer)](https://nbviewer.org/github/Tulayilmaz/b2b-churn-analysis/blob/main/analiz.ipynb)**

# B2B SaaS Müşteri Terk (Churn) Tahmini ve Stratejik Aksiyon Planı

Bu proje, bir B2B SaaS (Hizmet Olarak Yazılım) şirketinin veri tabanında yer alan müşteri davranışlarını analiz ederek, **aylık %42.1 seviyesindeki müşteri terk (churn) oranının** kök nedenlerini teşhis etmeyi ve makine öğrenmesi (Random Forest) kullanarak gelecekteki churn risklerini önceden tahmin etmeyi amaçlamaktadır. 

Salt metrik raporlamanın ötesine geçilerek, teknik bulgular Pazarlama ve Müşteri Başarısı (CS) ekipleri için **doğrudan uygulanabilir iş stratejilerine** dönüştürülmüştür.

## 🎯 İş Problemi ve Finansal Etki
* **Mevcut Durum:** Şirket aylık **%42.1** churn oranı ile sektör standartlarının çok üzerindedir.
* **Finansal Hasar:** İptal edilen abonelikler nedeniyle aylık **$51,176** MRR (Tekrarlayan Gelir) kaybı yaşanmaktadır (Yıllık projeksiyonda ~$614K kayıp).
* **Hedef:** Riskli müşterileri tespit edip erken müdahale (early warning) sistemi kurarak MRR kaybını minimize etmek.

## 🛠️ Kullanılan Teknolojiler
* **Veritabanı & Sorgulama:** SQLite, SQL (`JOIN`, `GROUP BY`, Aggregate Fonksiyonlar)
* **Veri Manipülasyonu:** Python, Pandas, NumPy
* **Makine Öğrenmesi:** Scikit-Learn (`RandomForestClassifier`, `train_test_split`, `classification_report`)
* **İş Ortamı:** Jupyter Notebook / VS Code

## 🧠 Analitik Yaklaşım ve Yöntem
Bu projede geleneksel, ezbere dayalı (örn. yaş/cinsiyet analizleri gibi B2B dinamiklerinde geçersiz olan) metrikler bilinçli olarak analiz dışı bırakılmış, doğrudan ürün kullanımı ve finansal taahhütlere odaklanılmıştır.

1. **Teşhis Edici Analiz (SQL):** Müşteri tablosu, kullanım verileri ve ödeme segmentleri birleştirilerek sorunun kaynağı (fiyat/ödeme yöntemi vs. ürün deneyimi) izole edildi.
2. **Tahminsel Modelleme (Machine Learning):** Kategorik değişkenler sayısallaştırılarak (One-Hot Encoding) Random Forest algoritması eğitildi.
3. **Risk Skorlaması:** Model, henüz aktif olan müşterilerin verileriyle beslenerek her bir kullanıcı için %0 ile %100 arasında bir **"Churn Risk Skoru"** üretti.

## 📊 Temel Çıktılar ve Kök Nedenler
Geliştirilen tahmin modeli test verisi üzerinde **%93.50 Doğruluk (Accuracy)** ve **%97 Churn Tahmin Hassasiyeti (Precision)** ile çalışmıştır. Modelin "Özellik Önemi" (Feature Importance) analizine göre churn'ü tetikleyen ilk 3 faktör:

1. **Sisteme Giriş Yapmama / Atıllık (Etki: %31.9):** 30 günden uzun süre sisteme girmeyen müşterilerin churn ihtimali dramatik şekilde artmaktadır.
2. **Taahhütsüz Sözleşmeler (Etki: %31.1):** Aylık pakete sahip olan kullanıcılar, iptal kolaylığı nedeniyle şirketin MRR kaybının %91'ini oluşturmaktadır.
3. **Çözülemeyen Teknik Sorunlar (Etki: %15.5):** 2 ve üzeri teknik destek bileti açan müşterilerin ürünü terk etme hızı ivmelenmektedir.

## 🚀 Yönetim İçin Aksiyon Planı
Veri analizinden elde edilen çıktılar doğrultusunda ilgili departmanlar için oluşturulan aksiyon planı:

* **Pazarlama Ekibi:** Aylık aboneleri yıllık paketlere geçirmeye yönelik "12 Ay Al, 10 Ay Öde" kampanyalarının başlatılması.
* **Müşteri Başarısı (Customer Success):** Ürüne 14 günden uzun süre giriş yapmayan (soğuma evresindeki) müşterilere otomatik 're-engagement' e-postaları gönderilmesi.
* **Teknik Destek Ekibi:** 2 ve üzeri bilet açan müşterilerin doğrudan kıdemli temsilcilere (VIP Escalation) aktarılarak şikayet çözme hızının artırılması.

## 📂 Kurulum ve Kullanım
Projeyi kendi bilgisayarınızda çalıştırmak için:
1. Repoyu klonlayın: `git clone https://github.com/KULLANICI_ADIN/saas-churn-prediction.git`
2. Gerekli kütüphaneleri yükleyin: `pip install pandas scikit-learn`
3. `analiz.ipynb` dosyasını Jupyter ortamında açarak hücreleri sırasıyla çalıştırın.
