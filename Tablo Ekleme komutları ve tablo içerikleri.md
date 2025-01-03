Veritabanı, sistemin temel işleyişini destekleyen ve farklı veri gruplarını içeren tablolarla yapılandırılmıştır. Araçlar, müşteriler, bakım geçmişi, şarj istasyonları, personel, faturalar ve sürüş geçmişi gibi kritik bilgiler, tablolar arasında anlamlı ilişkiler kurularak organize edilmiştir.

## MusteriTB

Müşterilerin iletişim bilgileri, bakiyeleri ve kimlik bilgileri kaydedilmiştir.

```sql
INSERT INTO MusteriTB (MusteriID, TelefonNum, Bakiye, AdSoyad)  
VALUES   
(1, '05321234567', 349.25, 'Mehtap Ülker'),  
(2, '05431234567', 300.00, 'Fatma Beyaz'),  
(3, '05551234567', 1000.00, 'Elif Sara Han'),  
(4, '05349876543', 200.00, 'Melih Uğurlu'),  
(5, '05439876543', 700.00, 'Ali Veli');
```
![[WhatsApp Görsel 2025-01-02 saat 01.01.51_63e212f8.jpg]]
## AracTB

Elektrikli araçların marka, model, batarya kapasitesi ve son bakım tarihleri gibi teknik detayları içeren kayıtlar eklenmiştir.

```sql
INSERT INTO AracTB (AracID, MusteriID, Marka, Model, BataryaKapasitesi, SonBakim)  
VALUES   
(1, 1, 'Tesla', 'Model 3', 75 kWh, '2025-01-01'),  
(2, 2, 'Nissan', 'Leaf', 40 kWh, '2023-12-15'),  
(3, 3, 'BMW', 'i3', 42 kWh, '2023-11-20'),  
(4, 4, 'Renault', 'Zoe', 64 kWh, '2024-01-10'),  
(5, 5, 'Hyundai', 'Kona', 70, '2024-01-15'),
(15, 1, 'Tesla', 'Model S', 100, '2025-01-01'),  
(16, 2, 'BMW', 'i3', 80, '2025-01-02'),  
(17, 3, 'Renault', 'Zoe', 50, '2025-01-03'),  
(18, 4, 'Nissan', 'Leaf', 60, '2025-01-04'),  
(19, 5, 'Hyundai', 'Kona', 70, '2025-01-05');
```
![[WhatsApp Görsel 2025-01-02 saat 01.01.40_f424a04a.jpg]]
## SurusGecmisiTB

Araçların sürüş geçmişi, pil kullanımı, süre ve başlangıç-bitiş konumları eklenmiştir.

```sql
INSERT INTO SurusGecmisiTB (SurusID, AracID, PilKullanimi, Sure, BaslangicKonum, BitisKonum)
VALUES   
(1, 1, 20, 45, 'İstanbul Kadıköy', 'İstanbul Beşiktaş'),  
(2, 2, 15, 30, 'Ankara Çankaya', 'Ankara Keçiören'),  
(3, 3, 25, 60, 'İzmir Konak', 'İzmir Bornova'),  
(4, 4, 10, 20, 'Bursa Nilüfer', 'Bursa Osmangazi'),  
(5, 5, 30, 90, 'Antalya Muratpaşa', 'Antalya Konyaaltı');
```
![[WhatsApp Görsel 2025-01-02 saat 01.01.42_41745b38 1.jpg]]
## BakimGecmisiTB

Araçların bakım süreçleri, kullanılan parçalar ve yapılan işlemler detaylı bir şekilde kaydedilmiştir.

```sql
INSERT INTO BakimGecmisiTB (AracID, BakimTarihi, KullanilanParcalar, YapilanIslemler)  
VALUES   
(1, '2025-01-01', 'Fren Balatası, Yağ Filtresi', 'Fren Sistemi Kontrolü, Yağ Değişimi'),  
(2, '2025-01-02', 'Hava Filtresi, Lastik', 'Hava Filtresi Değişimi, Lastik Değişimi'),  
(3, '2025-01-03', 'Akü, Motor Yağı', 'Akü Kontrolü, Motor Yağı Değişimi'),  
(4, '2025-01-04', 'Fren Diski, Soğutma Sıvısı', 'Fren Sistemi Onarımı, Soğutma Sıvısı Yenileme'),  
(5, '2025-01-05', 'Far Ampulü, Cam Sileceği', 'Far Ayarı, Cam Sileceği Değişimi');
```
![[WhatsApp Görsel 2025-01-02 saat 01.01.46_5b74f087.jpg]]
## FaturaTB

Müşterilere ait fatura bilgileri, şarj istasyonlarıyla ilişkilendirilerek tutar ve tarih bilgileriyle birlikte kaydedilmiştir.

```sql
INSERT INTO FaturaTB (FaturaID, MusteriID, IstasyonID, FaturaTarihi, Tutar)  
VALUES   
(1, 1, 1, '2025-01-01', 150.75),  
(2, 2, 2, '2025-01-02', 200.50),  
(3, 3, 3, '2025-01-03', 300.00),  
(4, 4, 4, '2025-01-04', 400.25),  
(5, 5, 5, '2025-01-05', 500.00);
```
![[WhatsApp Görsel 2025-01-02 saat 01.01.48_9bc43486 1.jpg]]
## PersonelTB

Şarj istasyonlarında görev yapan personelin kimlik bilgileri, görevleri ve işe giriş tarihleri eklenmiştir.

```sql
INSERT INTO PersonelTB (PersonelID, IstasyonID, AdSoyad, Gorev, IseGiris)  
VALUES   
(1, 1, 'Ahmet Yılmaz', 'Teknisyen', '2023-01-15'),  
(2, 2, 'Ayşe Kara', 'Mühendis', '2022-05-10'),  
(3, 3, 'Mehmet Demir', 'Danışman', '2021-09-20'),  
(4, 4, 'Fatma Çelik', 'Operatör', '2024-03-01'),  
(5, 5, 'Ali Vural', 'Teknisyen', '2020-11-25');
```
![[WhatsApp Görsel 2025-01-02 saat 01.01.59_6f078951.jpg]]
## SarjIstasyonuTB

Şarj istasyonlarının adresleri, kapasiteleri ve konum bilgileri eklenmiştir.

```sql
INSERT INTO SarjIstasyonuTB (IstasyonID, Adres, Kapasite)  
VALUES   
(1, 'İstanbul, Kadıköy, Bağdat Caddesi No:123', 10),  
(2, 'Ankara, Çankaya, Atatürk Bulvarı No:45', 8),  
(3, 'İzmir, Konak, Cumhuriyet Meydanı No:7', 12),  
(4, 'Bursa, Nilüfer, FSM Bulvarı No:89', 6),  
(5, 'Antalya, Muratpaşa, Lara Caddesi No:34', 15);
```
![[WhatsApp Görsel 2025-01-02 saat 01.02.23_86201896.jpg]]

