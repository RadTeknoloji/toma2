echo "# toma2" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:RadTeknoloji/toma2.git
git push -u origin main



Rentack Mülk Yönetimi Uygulaması

Uygulama minimum 17.6 iOS versiyonu için yazılıyor. 
Swift dili ile yazılıyor. 
Xcode 15 kullanılıyor. 
Backend için Firebase kullanılıyor.
Sayfa yapısı olarak view, viewmodel, model olarak kurguladık. 




Kullanıcı Tipleri (Kullanıcı Rolleri):
- Agency
- Tenant
- Owner

        - Kullanıcı tipleri (rolleri), bu uygulamada standartların dışında bir yapıyla organize edilmiştir. 1 Kullanıcı, 3 ayrı kullanıcı tipine sahip olabilir. Kayıt olurken hangi kullanıcı tipi ile başlarsa başlasın, diğer iki kullanıcı tipini de sonradan ekleyerek kullanmaya başlayabilir. Ancak hiçbir kullanıcı tipi kullanıcısı aynı olsa bile, diğer kullanıcı tipiyle ilgili yönetim yapamaz. Ayrı kullanıcılar gibi davranır. Bunu böyle yapmaktaki maksadımız, gerçek hayatta bir agency, hem tenant hem de owner olabilir, farklı mülklerde. Aynı mülkte 3 kullanıcı tipine de sahip olması zaten düşünülemez. Bir kişi kendi sahibi olduğu mülkün hem de kiracısı veya emlakçısı olamaz. 
    
    Owner: Mülk Sahibi. Bu kulllanıcı tipinin yapabileceği işlemler:
        - Mülk ekleme,
        - Mülkü kiraya verme,
        - Mülkü ilanda yayınlama,
        - Mülke gider ekleme, 
        - Mülk kira tablosu oluşturma, 
        - Agency arama,
        - Agency değerlendirme,
        - Mülke Agency atama, 
        - Talep oluşturma,
        - Belge oluşturma gibi temel işlevleri yapabilir ve bu işlemlere bağlı alt işlemlerde çeşitli işlemleri yapabilir. 

    Agency: Emlakçı. 
        - Mülk ekleme,
        - Mülkü kiraya verme,
        - Mülkü ilanda yayınlama,
        - Mülke gider ekleme, 
        - Mülk kira tablosu oluşturma,
        - Personel ekleme,
        - Mülke personel atama,
        - Portföy yönetimi,
        - Talep oluşturma,
        - Belge oluşturma gibi temel işlevleri yapabilir ve bu işlemlere bağlı alt işlemlerde çeşitli işlemleri yapabilir.  

    Tenant: Kiracı. Bu kulllanıcı tipinin yapabileceği işlemler:
        - Mülk ekleme,
        - Mülke gider ekleme,
        - Mülk kira tablosu oluşturma,
        - Talep oluşturma,
        - Belge oluşturma gibi temel işlevleri yapabilir ve bu işlemlere bağlı alt işlemlerde çeşitli işlemleri yapabilir.

EŞLEŞTİRME SİSTEMİ:
    Sistemin en önemli özelliklerinden biridir. Sistemde kullanıcı tipleri ayrı ayrı mülkler oluşturmuş olabilir. Ama aslında aynı mülkü yönetiyorlardır. Bunun ortak yönetilmesi için üretilen "eşleştirme" match çözümü bir mülkü 3 kullanıcı tipinden de yönetilir olmasını sağlamaktadır. 
    Örnek: Bir tenant, bir mülk eklemiş olsun. Bu mülkün numarası (sistem propertyCode ataması yapar) 0999111 olsun. Bu tenant, mülkü kiralarını takip edebilmek için eklemiştir. Ve masraflarını da. İsterse bağımsız kullanabilir zaten. Ve bir owner da, bir mülk eklemiş olsun. Onun da numarası 8238211 olsun. Ve bir Agency kullanıcı tipi de bir mülk eklemiş olsun ve onun da numarası 17332712 olsun. Aslında bu 3 kullanıcı tipi, yani kullanıcılar, aslında aynı mülkü kendi uygulamalarından yükleyip, birbirinden bağımsız yönetiyor olmuş olacak. Ancak bu match yapma sayesinde, mülk bilgileri birleşir, ve mülk sahibinin hangi bilgileri hangi kullanıcı tipinden çağıracağını dahi belirleyerek, 3 kullanıcı tipinin de kolaylıkla yönetmesini sağlar. 
        - Burdaki önemli ayrıntı, mülk numarası ve id konusu. Eşleşme sırasında hangi mülkün asıl olduğu kabul edileceğini "Eşleşme tamamla" seçeneği ile owner belirliyor. Eğer owner yoksa, agency belirliyor. Yani sadece tenant ve agency arasındaysa eşleşme agency belirler. Owner varsa herhangi bir eşleşmede owner belirler. Artık 3 kullanıcı ownerin belirlediği mülkü ortak takip edebilirler. 

        Eşleştirme sistemini anlatmaya devam edice. 

Talepler Sistemi: 
    Kullanıcıların, kendi aralarında bazı konularda talep oluşturmasını ve talebe onay vermesini tesis eder. Bazı talep kategorileri otomatik çalışır. Kira artışı talebi, Rezervasyon talebi, Eşleştirme, Sözleşme Yenileme, Emlakçı atama gibi talepler, başka sayfalardan gelen isteklerle otomatik oluşur. 

Kira Takip Sistemi:
    Kira takibi, bir mülk için kira başlangıç ve bitiş tarihleri arasındaki ay sayısına göre, kira ödeme tablosu oluşturulması ile oluşur. "kira tablosu oluştur" butonu 1 kere kullanılır ve kapanır. 

Giderler Takip Sistemi:
    Mülk seçilerek ilerlenir ve mülk için yapılan masraflar kayıt altına alınır. 

İlanlar Sistemi:
    Mülklerin ilana çıkabilmesini ve diğer tüm kullanıcıların ilanları okuyabilmesini sağlar. 

Portföy Takip Sistemi: (Agency için)
    Agency kullanıcısı, sisteme portöylerini ekler ve yönetir. 

Personel Takip Sistemi: (Agency için)
    Agency kullanıcısı sisteme personellerini ekler ve yönetir.

Emlakçı Takip Sistemi: (Owner İçin)
    Owner kullanıcısı, sisteme emlakçılarını ekleyebilir, mevcut emlakçıları bulabilir, değerlendireme yapabilir, mülküne atama yapabilir. 

Mülklerim Siste:
    Sistemin temel işlevidir zaten. Geniş kapsamlıdır. Adım adım ilerleriz. 

İstatistikler: 
    Her kullanıcı tipine göre ayrı istatiksel veriler olmalı. Ana sayfada, kullanıcı tipleri için "istatikler" butonu zaten var. 
        Agency için olası veriler: Toplam portföy, ilan sayısı, kirada olan mülkler, toplam personel, çoğaltılabilir..
        Owner için olası veriler: Toplam mülkler, kirada olan mülkler, toplam aylık kira geliri, Toplam aylık giderler, çoğaltılabilir. 
        Tenant için olası veriler: 
        Toplam mülkler, her ödenen kira toplamı, aylık giderler, bugüne kadar ödenen toplam giderler, çoğaltılabilir.

Çoklu Dil Desteği: Uygulama 6 dilde yayınlanacak. Şimdilik ingilizce ve türkçe olarak hazırlanıyor. Sabit keyler, ingilizce olacak şekilde tasarlandı. Dil stringleri oluşturuluyor. 

Tema: ThemeKit.swift ile, tüm sayfaların tutarlı bir görünüme sahip olması sağlanır. 


    
