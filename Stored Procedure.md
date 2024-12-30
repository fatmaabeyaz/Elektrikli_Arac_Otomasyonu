# Stored Procedure Raporu - Araç Tablosu İşlemleri

Bu rapor, **AracTB** tablosu üzerinde yapılacak olan CRUD (Create, Read, Update, Delete) işlemleri için kullanılan SQL **Stored Procedure**'leri içermektedir.

## 1. **AddArac** - Araç Ekleme Stored Procedure

**İşlevi**: Bu prosedür, yeni bir araç kaydını **AracTB** tablosuna ekler. **AracID** otomatik olarak atanır çünkü **AracID** sütunu **IDENTITY** olarak tanımlanmıştır.

```sql
CREATE PROCEDURE AddArac
    @MusteriID INT,
    @Marka NVARCHAR(50),
    @Model NVARCHAR(50),
    @Batarya NVARCHAR(50),
    @SonBakim DATETIME
AS
BEGIN
    INSERT INTO AracTB (MusteriID, Marka, Model, Batarya, SonBakim)
    VALUES (@MusteriID, @Marka, @Model, @Batarya, @SonBakim);
END;
```

**Açıklama**:  
- **@MusteriID**: Aracın ait olduğu müşteri ID'si.
- **@Marka**: Araç markası.
- **@Model**: Araç modeli.
- **@Batarya**: Araç batarya kapasitesi.
- **@SonBakim**: Araç için son bakım tarihi.

**Kullanım Örneği**:

```sql
EXEC AddArac 
    @MusteriID = 1,  
    @Marka = 'Tesla',  
    @Model = 'Model S',  
    @Batarya = '100 kWh',  
    @SonBakim = '2024-12-30';
```

---

## 2. **UpdateArac** - Araç Güncelleme Stored Procedure

**İşlevi**: Bu prosedür, **AracTB** tablosunda mevcut bir araç kaydını günceller. Güncelleme işlemi, aracın **AracID**'sine göre yapılır.

```sql
CREATE PROCEDURE UpdateArac
    @AracID INT,
    @MusteriID INT,
    @Marka NVARCHAR(50),
    @Model NVARCHAR(50),
    @Batarya NVARCHAR(50),
    @SonBakim DATETIME
AS
BEGIN
    UPDATE AracTB
    SET MusteriID = @MusteriID,
        Marka = @Marka,
        Model = @Model,
        Batarya = @Batarya,
        SonBakim = @SonBakim
    WHERE AracID = @AracID;
END;
```

**Açıklama**:  
- **@AracID**: Güncellenecek aracın ID'si.
- **@MusteriID**: Aracın ait olduğu yeni müşteri ID'si.
- **@Marka**: Yeni araç markası.
- **@Model**: Yeni araç modeli.
- **@Batarya**: Yeni batarya kapasitesi.
- **@SonBakim**: Yeni son bakım tarihi.

**Kullanım Örneği**:

```sql
EXEC UpdateArac
    @AracID = 1,  
    @MusteriID = 2,  
    @Marka = 'Ford',  
    @Model = 'Mustang',  
    @Batarya = '75 kWh',  
    @SonBakim = '2024-12-31';
```

---

## 3. **DeleteArac** - Araç Silme Stored Procedure

**İşlevi**: Bu prosedür, **AracTB** tablosundan bir araç kaydını siler. Silme işlemi **AracID**'ye göre yapılır.

```sql
CREATE PROCEDURE DeleteArac
    @AracID INT
AS
BEGIN
    DELETE FROM AracTB
    WHERE AracID = @AracID;
END;
```

**Açıklama**:  
- **@AracID**: Silinecek aracın ID'si.

**Kullanım Örneği**:

```sql
EXEC DeleteArac 
    @AracID = 1;
```

---

## 4. **GetAracByMarka** - Marka Adına Göre Araçları Listeleme Stored Procedure

**İşlevi**: Bu prosedür, belirli bir markaya ait araçları **AracTB** tablosundan sorgular ve listeler.

```sql
CREATE PROCEDURE GetAracByMarka
    @Marka NVARCHAR(50)
AS
BEGIN
    SELECT AracID, MusteriID, Marka, Model, Batarya, SonBakim
    FROM AracTB
    WHERE Marka = @Marka;
END;
```

**Açıklama**:  
- **@Marka**: Arama yapılacak araç markası.

**Kullanım Örneği**:

```sql
EXEC GetAracByMarka 
    @Marka = 'Tesla';
```

---

# Kullanım Örnekleri

Aşağıda, tüm prosedürlerin nasıl kullanılacağına dair örnekler bulunmaktadır:

1. **Yeni Araç Ekleme**:

```sql
EXEC AddArac 
    @MusteriID = 1,  
    @Marka = 'Tesla',  
    @Model = 'Model S',  
    @Batarya = '100 kWh',  
    @SonBakim = '2024-12-30';
```

2. **Araç Güncelleme**:

```sql
EXEC UpdateArac
    @AracID = 1,  
    @MusteriID = 2,  
    @Marka = 'Ford',  
    @Model = 'Mustang',  
    @Batarya = '75 kWh',  
    @SonBakim = '2024-12-31';
```

3. **Araç Silme**:

```sql
EXEC DeleteArac 
    @AracID = 1;
```

4. **Markaya Göre Araçları Listeleme**:

```sql
EXEC GetAracByMarka 
    @Marka = 'Tesla';
```
