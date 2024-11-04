# Elektrikli Araç Otomasyonu

## Proje Ekibindeki Kişiler
- Elif Sara HAN
- Fatma BEYAZ
- Melih UĞURLU

## Proje Gereksinimleri

### Genel Gereksinimler
- **Veri Tabanı Yapısı**: Elektrikli Araç Otomasyonu sistemi için bir veri tabanı yapısının kurulması.
- **Kullanıcı Rolleri**: Müşteriler, araç sahipleri, bakım personeli ve sistem yöneticisi gibi kullanıcı rollerinin tanımlanması.
- **Veri Güvenliği**: Müşteri bilgileri, ödeme detayları ve bakım geçmişi gibi kritik verilerin güvenliğinin sağlanması.
- **Kullanıcı Dostu Arayüz**: Sisteme veri girişi ve veri sorgulama işlemlerinin kolayca yapılabilmesi için kullanıcı dostu bir arayüz sağlanması.
- **Güncelleme ve İzleme**: Araç, bakım, şarj ve müşteri işlemlerinin izlenebilmesi ve gerektiğinde güncellenebilmesi.
- **Raporlama**: Şarj kullanımı, bakım maliyetleri ve müşteri bakiyeleri gibi konularda raporlama yapılabilmesi.

### Detaylı Gereksinimler
Her bir varlık ve ilişki için gereksinim detayları aşağıda verilmiştir.

1. **Müşteri**
   - **Özellikler**:
     - Müşteri_ID: Müşteri kimlik numarası.
     - İsim: Müşteri adı.
     - Bakiye: Müşteri bakiyesi, fatura ödeme ve şarj işlemleri için kullanılır.
     - İletişim Bilgileri: Müşteri ile iletişim kurulmasını sağlayan bilgiler.
   - **İlişkiler**:
     - Sahip Olur (Araç): Bir müşteri birden fazla araca sahip olabilir (Birden-Çoğa).
     - Öder (Fatura): Müşteri faturaları öder (Birden-Çoğa).

2. **Araç**
   - **Özellikler**:
     - Araç_ID: Araç kimlik numarası.
     - Model: Araç modeli.
     - Marka: Araç markası.
     - Batarya Kapasitesi: Araç batarya kapasitesi.
     - Şarj Durumu: Anlık batarya seviyesi veya durumu.
     - Son Bakım Tarihi: Aracın en son bakım yaptığı tarih.
   - **İlişkiler**:
     - Gerçekleştirilir (Sürüş Geçmişi): Araç sürüş geçmişine sahiptir (Birden-Çoğa).
     - Şarj Edilir (Şarj İstasyonu): Araçlar bir veya birden fazla şarj istasyonunda şarj olabilir (Çoktan-Çoğa).
     - Bakım Yaptırır (Bakım Geçmişi): Araç bakım işlemlerine sahiptir (Birden-Çoğa).

3. **Sürüş Geçmişi**
   - **Özellikler**:
     - Sürüş_ID: Sürüş kimlik numarası.
     - Başlangıç KM: Sürüşün başlangıç kilometresi.
     - Bitiş KM: Sürüşün bitiş kilometresi.
     - Süre: Sürüş süresi.
     - Enerji Kullanımı: Sürüşte tüketilen enerji miktarı.
   - **İlişkiler**:
     - Gerçekleştirilir (Araç): Bir araç birden fazla sürüş kaydına sahip olabilir (Birden-Çoğa).

4. **Fatura**
   - **Özellikler**:
     - Fatura_ID: Fatura kimlik numarası.
     - Fatura Tarihi: Fatura tarihi.
     - Tutar: Fatura tutarı.
   - **İlişkiler**:
     - Öder (Müşteri): Fatura bir müşteri tarafından ödenir (Çoktan-Bire).
     - Faturalandırır (Şarj): Fatura bir şarj işlemi için düzenlenebilir (Birden-Bire).

5. **Şarj İstasyonu**
   - **Özellikler**:
     - İstasyon_ID: Şarj istasyonu kimlik numarası.
     - Konum: Şarj istasyonunun konumu.
     - Kapasite: İstasyonda bulunan şarj noktalarının sayısı.
     - Mevcut Durum: İstasyonun mevcut durumu (aktif/pasif).
   - **İlişkiler**:
     - Şarj Edilir (Araç): Şarj istasyonunda birden fazla araç şarj olabilir (Çoktan-Çoğa).
     - İşletir (Personel): İstasyon bir personel tarafından işletilebilir (Çoktan-Bire).

6. **Personel**
   - **Özellikler**:
     - Personel_ID: Personel kimlik numarası.
     - Personel İsim: Personelin adı.
     - Görev: Personelin görev tanımı.
     - İşe Giriş Tarihi: Personelin işe başladığı tarih.
     - Yapılan İşlemler: Personelin gerçekleştirdiği işlemler.
   - **İlişkiler**:
     - İşletir (Şarj İstasyonu): Personel birden fazla şarj istasyonunu işletebilir (Birden-Çoğa).

7. **Bakım Geçmişi**
   - **Özellikler**:
     - Bakım_ID: Bakım kimlik numarası.
     - Bakım Tarihi: Bakımın yapıldığı tarih.
     - Kullanılan Parçalar: Bakım sırasında kullanılan parçalar.
     - Yapılan İşlemler: Bakım sırasında yapılan işlemler.
   - **İlişkiler**:
     - Bakım Yaptırır (Araç): Bakım işlemi bir araca ait olabilir (Çoktan-Bire).

8. **Şarj**
   - **Özellikler**:
     - Şarj_ID: Şarj işlemi kimlik numarası.
     - Tarih: Şarj işlemi tarihi.
     - Kullanılan Enerji: Şarj sırasında kullanılan enerji miktarı.
   - **İlişkiler**:
     - Şarj Edilir (Araç-Şarj İstasyonu): Şarj işlemi bir araç ve şarj istasyonu arasında gerçekleştirilir (Çoktan-Çoğa).

### İlişki Özetleri
- Sahip Olur (Müşteri - Araç): Birden-Çoğa
- Öder (Müşteri - Fatura): Birden-Çoğa
- Gerçekleştirilir (Araç - Sürüş Geçmişi): Birden-Çoğa
- Şarj Edilir (Araç - Şarj İstasyonu): Çoktan-Çoğa
- Bakım Yaptırır (Araç - Bakım Geçmişi): Birden-Çoğa
- İşletir (Personel - Şarj İstasyonu): Çoktan-Bire
- Faturalandırır (Fatura - Şarj): Birden-Bire

## E-R Diyagramı![eR drawio](https://github.com/user-attachments/assets/d8b84458-fe98-45a5-815a-2b3a36dd4023)

