### 1. **Trigger 1: Müşteri Silindiğinde İlgili Araçların Silinmesi**
**Trigger Adı:** `tr_DeleteMusteri`  
**Ne İşe Yarar:**  
Bu trigger, **MusteriTB** tablosundaki bir müşteri kaydı silindiğinde, o müşteriye ait tüm araçların **AracTB** tablosundan silinmesini sağlar. Bu işlem, müşteri silindiğinde veri tutarlılığını korumak için yapılır.

```sql
CREATE TRIGGER tr_DeleteMusteri
ON MusteriTB
AFTER DELETE
AS
BEGIN
    -- Silinen müşteri kaydından MusteriID'yi alıyoruz
    DECLARE @MusteriID INT;

    -- Silinen müşteri kaydından MusteriID'yi alıyoruz
    SELECT @MusteriID = MusteriID FROM deleted;

    -- Bu MusteriID'ye ait araçları AracTB tablosundan siliyoruz
    DELETE FROM AracTB
    WHERE MusteriID = @MusteriID;
END;
```

**Açıklama:**  
- **AFTER DELETE**: **MusteriTB** tablosundan bir müşteri silindiğinde tetiklenir.
- **deleted** tablosu, silinen kayıtları tutar. Bu tablodan, silinen müşterinin **MusteriID**'sini alıyoruz.
- **AracTB** tablosunda, bu **MusteriID**'ye sahip araçları siliyoruz.

---

### 2. **Trigger 2: Bakım Kaydı Eklendiğinde Araç Son Bakım Tarihinin Güncellenmesi**
**Trigger Adı:** `tr_UpdateSonBakim`  
**Ne İşe Yarar:**  
Bu trigger, **BakimGecmisiTB** tablosuna bir yeni bakım kaydı eklendiğinde, o aracın **SonBakim** tarihini **AracTB** tablosunda günceller.

```sql
CREATE TRIGGER tr_UpdateSonBakim
ON BakimGecmisiTB
AFTER INSERT
AS
BEGIN
    -- Yeni eklenen bakım kaydından AracID'yi alıyoruz
    DECLARE @AracID INT;
    DECLARE @YeniBakimTarihi DATETIME;

    -- 'inserted' tablosundan yeni kaydın AracID ve BakimTarihi bilgilerini alıyoruz
    SELECT @AracID = AracID, @YeniBakimTarihi = BakimTarihi
    FROM inserted;

    -- AracTB tablosunda ilgili AracID'ye sahip aracın SonBakim tarihini güncelliyoruz
    UPDATE AracTB
    SET SonBakim = @YeniBakimTarihi
    WHERE AracID = @AracID;
END;
```

**Açıklama:**  
- **AFTER INSERT**: **BakimGecmisiTB** tablosuna yeni bir bakım kaydı eklendiğinde tetiklenir.
- **inserted** tablosu, yeni eklenen kayıtları tutar. Bu tablodan, eklenen bakım kaydının **AracID** ve **BakimTarihi** değerlerini alıyoruz.
- **AracTB** tablosunda, bu **AracID**'ye sahip aracın **SonBakim** tarihini güncelliyoruz.

---

### 3. **Trigger 3: Fatura Eklendiğinde Müşteri Bakiye Değerinin Azaltılması**
**Trigger Adı:** `tr_UpdateBakiye`  
**Ne İşe Yarar:**  
Bu trigger, **FaturaTB** tablosuna bir yeni fatura kaydı eklendiğinde, faturadaki **tutar** değerine göre **MusteriTB** tablosundaki ilgili müşterinin **Bakiye** değerini azaltır.

```sql
CREATE TRIGGER tr_UpdateBakiye
ON FaturaTB
AFTER INSERT
AS
BEGIN
    -- Yeni eklenen fatura kaydından MusteriID ve Tutar bilgilerini alıyoruz
    DECLARE @MusteriID INT;
    DECLARE @Tutar DECIMAL(8,2);

    -- 'inserted' tablosundan yeni kaydın MusteriID ve Tutar bilgilerini alıyoruz
    SELECT @MusteriID = MusteriID, @Tutar = Tutar
    FROM inserted;

    -- MusteriTB tablosunda ilgili MusteriID'ye sahip müşterinin Bakiye değerini güncelliyoruz
    UPDATE MusteriTB
    SET Bakiye = Bakiye - @Tutar
    WHERE MusteriID = @MusteriID;
END;
```

**Açıklama:**  
- **AFTER INSERT**: **FaturaTB** tablosuna yeni bir fatura kaydı eklendiğinde tetiklenir.
- **inserted** tablosu, yeni eklenen kayıtları tutar. Bu tablodan, faturanın **MusteriID** ve **Tutar** bilgilerini alıyoruz.
- **MusteriTB** tablosunda, bu **MusteriID**'ye sahip müşterinin **Bakiye** değerini **Tutar** kadar azaltıyoruz.

---

### Özet Rapor

| **Trigger Adı**         | **İşlevi**                                                                                                           |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------|
| **tr_DeleteMusteri**     | **MusteriTB** tablosunda bir müşteri silindiğinde, o müşteriye ait araçların **AracTB** tablosundan silinmesini sağlar. |
| **tr_UpdateSonBakim**    | **BakimGecmisiTB** tablosuna yeni bir bakım kaydı eklendiğinde, **AracTB** tablosundaki aracın **SonBakim** tarihini günceller. |
| **tr_UpdateBakiye**      | **FaturaTB** tablosuna yeni bir fatura kaydı eklendiğinde, faturadaki **Tutar** değerine göre ilgili müşterinin **Bakiye** değerini azaltır. |

---
