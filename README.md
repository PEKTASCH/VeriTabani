# Waterfall Süreç Modeli ile Müzik Veritabanı


## - Planlama

    Projenin maaliyeti müşteriye bildirilir. Veritabanını oluşturmak için gerekli yetkinliğe sahip kişiler projeye dahil edilir.


## - Gereksinim Analizi

    Bir müzik uygulamasında,

    Kullanıcıların kişisel bazı bilgilerini, hesap abonelik türlerini, çalma listelerini gösteren, 
    Kullanıcıların sahip olduğu abonelik fiyatlandırma ve ayrıcalıklarını belirten,
    Kullanıcıların oluşturduğu çalma listelerini ve çalma listelerindeki şarkıları listeleyen,
    Sanatçıların şarkılarını ve albümlerini göstermek için kullanılacak bir ilişkisel veritabanı oluşturmak.

## - Tasarım

    Tasarım aşamasında ilişkisel veri tabanı yapısı kullanılacaktır. 
    
    Bir kullanıcının birden fazla çalma listesinin olabileceğini ve bir çalma listesinin sadece bir kullanıcının sahip olabileceğini, (One-to-Many)
    Bir çalma listesi birden fazla şarkı içerebileceğini, bir şarkının  birden fazla çalma listesinde olabileceğini, (Many-to-Many)
    Bir şarkının sadece bir albümde olabileceğini, ve bir albümün içinde birden fazla şarkının olabileceğini, (One-to-Many)
    Bir şarkı sadece bir sanatçıya ait olabileceğini, bir sanatçının birden fazla şarkısının olabileceğini, (One-to-Many)
    Bir kullanıcının sadece bir abonelik türünün olabileceiğini, bir abonelik türünün birden fazla kullanıcının sahip olabileceiğini, (One-to-Many)
    diyagram ile gösterilecektir.

### Oluşturulacak tablolar arasındaki ilişkiler ve tablo içindeki verilerin şema diyagramı ile gösterimi:

![Diyagram](https://github.com/PEKTASCH/VeriTabani/assets/108456677/0336e6c2-ea03-4243-bf13-f1cf461e51d2)
![SQLDiagram](https://github.com/PEKTASCH/VeriTabani/assets/108456677/02f2ee26-67ce-4423-8e4f-18b6e5a7cae6)

## - Kodlama

    SQL Server Managment Studio ile tasarımı oluşuturulan ilişkisel veri tabanı için kodlama aşamasına geçilir. 
    Veritabanı yaratıldı.
    Tablolar oluşturuldu.
    Oluşturulan tablolar için veri girişi yapıldı.

### Veritabanı Oluşturulur

    ```sql
    CREATE DATABASE MuzikVeritabani;
    ```

```sql
CREATE TABLE Kullanicilar (
    KullaniciID INT PRIMARY KEY,  /*KullaniciID" sütununu "Kullanici" tablosundaki otomatik artış, birincil anahtar alanı olarak tanımlanır. */
    KullaniciAdi VARCHAR(100) NOT NULL,  /*Her kullanıcının kullanıcı adı olmalı.*/
    Mail VARCHAR(150) UNIQUE NOT NULL,
    AbonelikID INT,
    FOREIGN KEY (AbonelikID) REFERENCES Abonelikler(AbonelikID)
);

CREATE TABLE Abonelikler (
    AbonelikID INT PRIMARY KEY,
    PlanIsmi VARCHAR(255) NOT NULL,
    Fiyat VARCHAR(15) NOT NULL,   /* '8.99 TL'*/
    Ayricaliklar TEXT  /*Boyutu kadar yer kaplaması için TEXT kullandım.*/
);

CREATE TABLE Sarkilar (
    SarkiID INT PRIMARY KEY,
    SarkiAdi VARCHAR(255) NOT NULL,
    SanatciID INT,  /*SanatciID*/
    AlbumID INT,
    Sure DECIMAL,
    YayinlanmaTarihi DATE,
    Tur VARCHAR(100),  /* Şarkı türü */
    FOREIGN KEY (AlbumID) REFERENCES Albumler(AlbumID),
    FOREIGN KEY (SanatciID) REFERENCES Sanatcilar(SanatciID)
);

CREATE TABLE CalmaListeleri (
    CalmaListesiID INT PRIMARY KEY,
    Baslik VARCHAR(255) NOT NULL,
    Aciklama TEXT,   /*Kullanici calma listesine bir açıklama yazmışsa açıklamasını göster.*/
    OlusturmaTarihi DATE,
    KullaniciID INT
    FOREIGN KEY (KullaniciID) REFERENCES Kullanicilar(KullaniciID)
);

CREATE TABLE CalmaListesiSarkilari (  /*Bakım aşamalarında kullanıcıların gizli listeler yapabilmesi için yeni listeler oluşturulabilir, geliştirilebilir.*/
    CalmaListesiID INT,
    SarkiID INT,
    PRIMARY KEY (CalmaListesiID, SarkiID),
    FOREIGN KEY (CalmaListesiID) REFERENCES CalmaListeleri(CalmaListesiID),
    FOREIGN KEY (SarkiID) REFERENCES Sarkilar(SarkiID)
);

CREATE TABLE Albumler (
    AlbumID INT PRIMARY KEY,
    Baslik VARCHAR(255) NOT NULL,
    Sanatci VARCHAR(200) NOT NULL,
    YayinlanmaTarihi DATE
);

CREATE TABLE Sanatcilar (
    SanatciID INT PRIMARY KEY,
    SanatciAdi VARCHAR(200) NOT NULL,
    Tur VARCHAR(100)
);
```

