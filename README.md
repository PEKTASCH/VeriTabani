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

