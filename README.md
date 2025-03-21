# Selamün Aleyküm Arkadaşlar,

![Free Palestine](Images/free-palestine.jpg)


Bu seride toplamda 16 bölüm bulunmaktadır (giriş bölümü hariç). Bölümlerde eksik fazla olduğunu düşündüğünüz noktalar için geri dönüşleriniz ve PR'larınızı bekliyoruz!


**Giriş: Index[0]**

Çok uzun süredir notlarımda olan ve hep yazmak istediğim bir seriye Allah’ın izniyle başlıyorum. Yıllar önce izlemiş olduğum [bu videoda](https://www.youtube.com/watch?v=a3ehu_Yv96U&t=2671s&ab_channel=MustafaVarank) not aldığım 16 başlığı 16 ayrı bölüm olarak ele alıyorum. Sadece başlıkları buradan almış olup içeriği özgün olarak oluşturmaya gayret ettim. Böyle düşününce gerçekten zor bir hedef gibi görünüyor, ancak birincisine niyet edip başlarsak inşaAllah gerisi de gelir diye düşünüyorum..

Bu bölüm girizgah kısmı olacak. Hangi konuları ele alacağımızı belirtip özet mahiyetinde birkaç cümle ile kısa kısa açıklamalar yapacağız. Daha sonra yeni yazıları yazdıkça buradaki linkleri de güncelliyor oluruz inşaAllah. Bazı konular hakkında daha çok bilgi sahibiyken bazı konularda benim de daha fazla okumalar yapmam lazım. Bu yolculuğa bir "assignment" [projesi](https://github.com/malikmasis/TelephoneDirectory) ile başlayıp onu belirli aralıklarla geliştirmeye devam ettim. Bunu daha önce bu [yazımda](https://medium.com/software-development-turkey/mikroservis-maceram-1e070463d0ea) dile getirmiştim. Devam eden süreçte de ayrıca bir yazı yazmadım. Hep bu yazıyı güncelleyerek veya Github projesini geliştirerek devam ettim, ancak bu sefer önüme zorlu da olsa bir hedef koymak istedim. Rabbim utandırmasın.

Mikroservis nedir, ne değildir gibi sorulara girmeyi pek düşünmüyorum açıkçası. Bu yazı serisi biraz daha bu işi bilen ya da en azından merak eden kesime yönelik olacak. Her ne kadar son projemde çok etkin bir şekilde bu yapıları kullansam da konuların derli toplu olması açısından veya projeye dalıp kaçırdığımız noktalar var ise öncelikle kendimi de geliştirmek açısından ele alıyorum. Hata, eksik veya fazla olduğunu düşündüğünüz yerler olursa elbette desteklerinize açık olduğumu da belirtmeden geçemeyeceğim.

Mikroservis konusu ile ilgili kendi adıma diyebileceğim en net şey, gerçekten ihtiyaç olduğuna ikna iseniz ve buna da uygun takım ya da takımlarınız var ise bu işe girmenizi naçizane öneriririm. Aksi halde siz ve ekibiniz için çok zorlu bir dönem başlayabilir. Nedenlerini önümüzdeki bölümlerde zaman zaman değiniyor oluruz. Ufaktan başlayalım.

---

1. **[Bounded Context](#1-bounded-context)**: Domain Driven Design ile bağlamı net bir şekilde ortaya koymak gerekir. Bağlam düzgün kurgulandığında birçok şey daha kolay oluyor. Fazla veya eksik olduğunda ise buradaki hatalarınızı gidermek için fazlaca yıpranabilirsiniz. Şahsi fikrim burası işin kalbi...

2. **[Async Messaging](#2-async-messaging)**: Asenkron iletişim mikroservis sisteminin olmazsa olmazıdır. Hem servisler arası iletişimde hem de uzun süren işlemlerde ilaç gibi gelir.

3. **[Composing Microservice](#3-composing-microservice)**: Gelen isteğin cevabını birçok servisten toplayarak farklı kanallar üzerinden toplayarak bunu cevap olarak döner. Bu konunun hızlıca anti-pattern'a dönme ihtimali var. Bunun için de bazı çözümler öneriliyor.

4. **[Achieving Data Consistency](#4-achieving-data-consistency)**: Mikroservis konusunun şahsımca en zor konusu bu olabilir. Veri tutarlığını sağlamak için bir sürü pattern olsa da bunu tam anlamıyla mükemmel uygulamak gerçekten kolay bir şey değil. Burası ne kadar sorunlu olursa o derece operasyon maliyeti artıyor.

5. **[Centralizing Access](#5-centralizing-access)**: Dışarıdan gelen tüm isteklerin nerelere nasıl yönlendirileceğini ele alır. Birbirine benzeyen ve çok karıştırılan 3 yapıya da değineceğiz. Özetle kalenin giriş kapıları olarak düşünebiliriz.

6. **[Separated Databases](#6-separated-databases)**: En sık düşülen hatalardan veya monolit yapılardaki geçişlerde en zorlanılan konulardan biridir. Her bir servisin ayrı bir veritabanı olmalıdır. Aksi halde veri tabanındaki herhangi bir hatada bütün sistem de çökmüş olacaktır.

7. **[Arch API-based](#7-arch-api-based)**: Api tabanlı iletişimi ele alır. Bunu sağlamanın birden çok yolu var. Her birinin de kendine göre avantaj ve dezavantajları var.

8. **[Resiliency](#8-resiliency)**: Bir servise yapılan çağrıların belirli bir sebepten dolayı cevap vermemesi sonucu orada bağlantıyı keserek bütün sisteme yük binmesine engel olur. Belirli dönemlerde buradaki problem düzelip düzelmediğini kontrol eder, düzelmiş ise tekrar bağlantıya izin verir.

9. **[Backward Compatibility](#9-backward-compatibility)**: Eskiye yönelik servislerin çalışırlığını ele alır. Bunun için versiyonlama kullanılan genel çözümlerden biridir. Aksi halde yaptığınız radikal bir değişiklik (breaking change) burayı kullanan eski istemcileri olumsuz etkileyecektir.

10. **[Documenting Contracts](#10-documenting-contracts)**: İstemci ve sunucu arasında bir protokol, anlaşma diyebiliriz. Interface'ler ile yazılımda nasıl bazı konular için el sıkışıyorsak bunu da öyle anlayabiliriz desek yanlış ifade etmiş olmayız herhalde. Open Api gibi standartlarla bunları ele alabiliriz.

11. **[Centralized Logging](#11-centralized-logging )**: İlk başta çok önemsenmese de servisler arttıkça hatalar oldukça loglamanın önemini çok daha iyi anlıyorsunuz. Özellikle debug yapmanın zor olduğu böyle bir ortamda bu çok daha kıymetli olmaktadır.

12. **[Cloud Based Infrastructure](#12-cloud-based-infrastructure)**: Bu başlık itibariyle biraz daha devops tarafına girişmeye başlıyoruz. Fiziksel sunucular yerine buluttaki hizmetleri ele almayı önerir. Birçok güzelliği olsa da elinizi verdiğinizde kolunuzu kaptırma ihtimaliniz de var :)

13. **[Deployment Automation](#13-deployment-automation)**: Bu işe girişmeyi düşünüyorsanız manuel deployment'i hayatınızdan çıkarmış olmanız gerekiyor. Servisleriniz her birinin otomatik olarak sunuculara gitmesi gerekmektedir. Hatta gün içinde istediğiniz anda bu işi de yapabiliyor olmalısınız.

14. **[Configuration Management](#14-configuration-management)**: Dev test prod gibi farklı ortamlarınızın olması gerekir. Bu aslında monolit yapılarda da olan bir konu ancak bazen gün içinde birden fazla deployment hedeflenen sistemlerde olmazsa olmaz durumuna dönüşüyor.

15. **[Service Registry & Discovery](#15-service-registry--discovery)**: Servislerin birbiriyle iletişim kurduğu durumları ele alır. Özellikle dinamik olarak ölçeklenme, dağıtılma gibi konularda daha da önemi artmaktadır. Yine birçok konudaki gibi bunu da yapan bazı araçlar mevcut.

16. **[Monitoring](#16-monitoring)**: Birden fazla servisiniz varsa bunları yönetmek de doğal olarak zorlaşabiliyor. Bunlardan herhangi birinde bir problem olduğunda kullanıcıdan önce sizin haberiniz olmalı. Hem durumları takip edebileceğimiz hem de bize alarm durumlarını önceden haber etmeye olanak sağlar.

---

**Sonuç:**

Yukarıdaki 16 konuya ufak ufak bazı notlar yazmaya çalıştık. Yazının devamında her bir konuyu ayrı ayrı olarak ele almayı düşünüyoruz. Niyet bizden, takdir ve başarı Allah'tandır.

Ben bu yazıyı taslak olarak yazarken şu an hala Gazze'deki insanlar açlıktan ölüyor. Rabbim buradaki kardeşlerimize de büyük bir zafer ihsan eylesin. Dualarımı ve bu yazı serisini, niyetleri Allah'ın rızasını kazanmak olan bu koca yürekli insanlara ithaf ediyorum.

**“Ve de ki: ‘Bütün başarı ve zafer, sadece Allah’tandır.’” (Al-i İmran, 3:126)**

### 1. Bounded Context

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özette de belirttiğimiz gibi bu işin kalbi bana göre sınırları doğru çizebilmek. Sınırları doğru ve net belirlediğimizde geriye kalan işler kolaylaşacaktır. Monolit yapılarda veritabanı tasarımının projedeki en önemli kısım olduğunu düşündüm hep. İyi bir veri tabanı iyi bir backend yazılımına, o da iyi bir arayüze ve günün sonunda iyi bir uygulama vesile olur. Mikroservis mimarisinde ise aynı şeyi "bounded context" için düşünüyorum.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Konuya bir anı ve ardından gelen bir soru ile girmekte fayda olabilir. Girdiğim bir mülakatta konu DDD'ye gelmişti. Ben de projemi bu yaklaşıma uygun geliştirdiğimi söylemiştim. Buna karşılık mülakatı yapan kişi bana peki DDD sadece yazılımcı için olan bir konu mu demişti?

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dürüst olmak gerekirse öyle bir soruyu hiç beklemiyordum. Daha önce de yaptığım bazı okumalarla birlikte yazılımcı bunun önemli bir parçası ama her şeyi değil demiştim. Gerçekten de bu ekipçe aynı dili, terminolojiyi kullanmaktan geçer. Ekip dediğim sadece yazılımcılardan bahsetmiyorum. Bunlarla birlikte ürüncü, testçi, analist ve artık daha kimler varsa. Özetle bu işin altına elini sokmuş tüm arkadaşlar diyebiliriz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Genel manada her bir bağlam (bounded context) bir mikroservisi teslim eder, edebilir. Muhtemelen çokça karşılaşmışsınızdır. Order, Payment, Product gibi servis isimleri geçer. Mikroservis teknolojisinin öncülüğünü bizim ülkede e-ticaret siteleri yaptığı için (ya da onlar daha önce çıkardığı için de olabilir) genelde örnekler de hep buradan geliyor. Farklı domainlerde çalışıyorsanız oturup biraz daha düşünmeniz veya kendi yoğurt yiyişinize göre sistemi tasarlamanız gerekebilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Şu an ben mobilite sektöründe çalışıyorum. Bu yüzden bizim kapsamlar baya farklı. Bağlamları belirlerken Rental (kiralama süreci), Vehicle (araç ve iot), Branch (bölge yönetimi) diye bizim birbirinin içine giren ama aslında farklı olabilecek 3 domainimiz vardı (diğerlerini net bir şekilde belirledik). Bunları ayrı birer bağlam mı yoksa hepsini tek bağlam altında toplama konusunda kararsızlık yaşadık. Benim şahsi fikrim bunları ayırmanın daha doğru olacağı yönündeydi, ancak bunları birlikte ele alarak devam ettik.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Geliştirmeler tüm hızla devam ediyor. 10 kişilik yazılım ekibi aynı projede geliştirmelerini sürdüyor (aslında 3 takım, her takımın, ayrıca yazılımcı olmayan üyeleri de var tabii ki). Zamanla kapsamlar birbirine yaklaştıkça toplantılar yaparak problemleri gidererek yolumuza hızlı bir şekilde devam ettik. Kapsamları birleştirmeye ilk başta çok sıcak bakmasam da zamanla tabii ki sıkıntılar çıksa da bunun çok daha iyi olduğunu anladım. En azından bizim için iyi olduğunu anladım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ayağı yere daha iyi basan veya daha oturmuş ekiplerle, daha uzun vadeli bir geliştirme yapılıyor olsa belki hala bu bağlamları ayrı ayrı ele almak iyi olacaktı. Ancak alınan kararlar göre değişkenlik gösterebiliyor. Teknik olarak doğrusu yanlışından ziyade bu işin size neler getirip sizden neler götüreceğini iyi tespit etmek lazım. Yoksa öteki türlü her çözüm her yere uygulanabilir olsaydı bu sektör belki de buralara gelmeyecekti...

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Başka bir projede de yaşadığım başka bir tecrübeden bahsetmek istiyorum. Bu işe sonradan dahil olduğum için, yapılan işi ve hangi sıkıntılarla karşılaştığımızdan bahsedeceğim. Yaklaşık 13-15 mikroservisli bir var ve bazıları mikroservis değil [nanoservis](https://nanoservices.io/docs/docs/concepts/nanoservice/) seviyesine gelmiş. Tablolar birbiriyle direkt ilişkili. A servisinden veriyi B servisine senkron olarak çekip oradan gelen veriye göre iş yapılıyor. Bu 1-2 defa yapılan bir iş değil bütün kurgu maalesef bu şekilde. Yani her ayrı olan kavramı ayrı birer mikroservis olarak ele almışlar, ancak orada "over engineering" oluşmuş ve günün sonunda ekipçe oturup bu servislerin bazılarını birleştirelim diye karar aldık.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2 ayrı örnekte de belirttiğim gibi, bu işin doğrusu yanlışından ziyade uygulanabilirliği önemli diye düşünüyorum. Her şeyi servislere bölmek de yanlış bir seçim, bütün her şeyi de tek bir servis altında toplamak zaten ayrı bir yanlış seçim olabilir. Bu işin dengesini ve kararını iyi verebilmek lazım. Orada düşünüp vereceğimiz bir karar inanın bütün projenin geliştirme sürecini çok derinden etkileyecektir. O yüzden kervan yolda düzülür gibi kararlardan naçizane sıyrılmanızı tavsiye ederim. Projeyi canlıya bile almadan her yeri yamalanmış bir proje ile karşı karşıya kalabilirsiniz veya daha kötü canlıya bile çıkmadan yolun sonuna gelmiş olabilirsiniz...

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle, projenin isterlerini ve gereksinimlerini iyi analiz ederek kapsamları doğru bir şekilde ortaya koymak projenin en kritik noktası olabilir. Bu yüzden başlangıç noktasında çok acele etmeden çok da "over engineering" yapmadan size uyacak en doğru kararı vermeniz duasıyla.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu bölümü birer ayet-i kerim ve hadis-i şerif ile bitirelim.

> "Biz her şeyi bir ölçüye göre yarattık." (Kamer, 54/49)

> "Muhakkak ki Allah, her işte ihsanı (en iyi şekilde yapmayı) emretmiştir." (Müslim, Sayd, 57; Ebû Davud, Edahi, 11)

 ### 2. Async Messaging
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin ikinci bölümünde asenkron iletişimi ele alacağız. Servisler arası iletişimde temelde iki yöntem var. Bu yöntemlerden biri senkron (rest api, grpc) ve diğeri asenkron olarak ele alabiliriz. Birbirilerine göre avantaj ve dezavantajları olsa da servislerin birbirine olan bağımlılıkları en aza indirgemek için asenkron iletişim bu işin temel parçalarından biri haline geliyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bir mikroservis sistemi tasarımında mümkün mertebe servisleri birbirinden izole olmasını isteriz. Bunun sebeplerinden bir tanesi o servisle ilgili herhangi bir olumsuzlukta sistemin ayakta kalmaya devam etmesidir. Örneğin, kampanyalar servisiniz düştü ancak kullanıcı hala alış-verişini yapmaya devam edebilmeli. Kampanya servisi düştüğü için bütün sistemin çalışılmaz hale gelmesine gerek yoktur.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Servislerin birbirine gevşek bağımlı hale gelmesini peki nasıl sağlarız? Bunun çözümlerinden biri, iletişimin asenkron olmasıdır. Senkron olan iletişimde servislerinden biri çöktüğünde diğer servis oradan gelecek cevabı bekleyecektir ve bu da sistemde bir gecikmeye sebep olacaktır (tabii ki bunun da çözümleri mevcut. Circuit breaker, timeout, fallback vb), ancak iletişim asenkron olduğunda bu problemler oldukça azalır (tabii ki farklı problem çıkabilir :) ).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peki her servis çağrısında asenkron iletişim mi kullanmalıyız? Bunun için mümkün olduğunca sistemi esnek tutabilmek açısından evet ama bazen diğer servislerden gelen cevabı beklememiz gerekiyorsa o zaman senkron iletişim kaçınılmaz hale geliyor. Ancak bazen de verilerin her iki servisin veri tabanında da tutulması konusu gündeme gelebilir. CDC (Change Data Capture) konusuna önümüzdeki bölümlerde değiniyor olacağız.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asenkron mesajlaşmanın daha da önemli hale geldiği konulardan bazıları; uzayan veya hemen işlenmesi çok kritik olmayan konular. Eposta, sms veya bildirim atmak, log işlemleri bunlara örnek olarak gösterilebilir. Bu tarz işlemler için bu konu daha da önemli hale gelebilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asenkron mesajlaşmada kullanılan birçok araç var. Bu araçlardan en göze çarpanları rabbitmq, kafka veya bulut çözümlerin kendi ürünleri de mevcut (amazon sqs, azure service bus). Bu araçların birbirlerine göre fiyat, performans gibi birçok artı ve eksi yönleri var. Dotnet dünyasında özellikle Rabbitmq'nin çok kullanıldığına şahit oluyorum ve onu implemente eden açık kaynaklı proje olan MassTransit ile birlikte kullanımı daha da kolay hale gelebiliyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asenkron mesajlaşmayı çok övdük de hiç mi eksik yanı yok derseniz, tabii ki her hastalığa aynı ilacı vermek söz konusu olamaz. Yukarıda da bahsettiğimiz gibi cevap bekleyen durumlarda veya basit sistem tasarımlarında bunu kullanmak sistemi daha karmaşık hale getirecektir. Öğrenmesi, yönetmesi ve takip etmesi gibi bazı zorlukları getirir. Verilerin doğru bir şekilde işlenmesi, iletilmesi, bazı durumlarda çoklanması gibi farklı zorluklar ortaya çıkmaktadır (veri tutarlığı konusuna ileride değiniyor olacağız). İlk başlarda bu zorlukları aşmak da çok kolay olmuyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle, asenkron mesajlaşma mikroservis mimarisinde bir zorunluk olmasa da önemli yapı taşlarından biridir. Genel sistem içerisinde tabii ki senkron ve asenkron iletişimin birlikte kurgulanabilir, hatta kurgulanmalı. Nereden hangisini kullanılacağını tespit edip ona göre işlemleri devam ettirmek en doğrusu olacaktır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerim ve hadis-i şerif ile bitirelim.

> "Ve yardım edin birbirinize takvada ve takvaya davette, günah ve düşmanlıkta ise yardım etmeyin." (Mâide, 5:2)

> "Dil bir kılıç gibidir, onunla ya kurtulursun ya da helak olursun." (İbn Mâce, Zühd, 19)

 ### 3. Composing Microservice

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin üçüncü bölümünde "composing microservice" konusunu ele alacağız. Birden çok servisten gelen cevapları toplayarak yanıt olarak istemciye (client) geri döner. Mikroservisin bağımsızlık ilkesine ters olsa da iş modelinin isterlerine göre kaçınılmaz olabiliyor. Bu durum, genel tasarıma zarar verebileceğinden burayı tasarlamak ilerideki birbirine bağımlı servislerin oluşmasına engel olmak açısından çok önemlidir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Genel itibariyle çok fazla servisimiz olduğunu varsayalım. Her birinin yaptığı işler belli, ancak gerçek hayattaki isterler tahmin edebileceğiniz üzere çok karmaşıklaşabiliyor. Bazen birden çok servisten bilgiyi toplayarak bir yanıt dönmemiz gerekiyor. Böyle durumlarda başvuracağımız yöntemlerden biri de bu servislerden gelen cevapları alarak toplu bir yanıt dönmek olacaktır. Bunun bazı yöntemleri var:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Api üzerinden bu verileri toplayarak gerekli cevaplar dönebiliriz, bununla birlikte Orchestration dediğimiz merkezi bir yapı ile bunu yapabiliriz. Servisleri sırasıyla çağırıp cevapları birleştirerek iletir. Choreography denilen diğer bir yapı ise merkezi bir yapı olmadan servislerin kendi arasında haberleşerek bu işi yapmasıdır. Servis sayısı veya karmaşıklık az ise bu yöntem daha uygun olabilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu yöntemlerin hepsi genel itibariyle aynı probleme çözüm araralar ama beraberinde de bazı zorluk ve sıkıntılara sebebiyet verebilirler. Veri tutarsızlığı (sonraki konumuz), performans problemleri, hataların yönetimi gibi zorlukları da beraberinde getirir. Bunlara önlem olarak tabii ki çözümler üretmek mümkün. Ancak bu problemlere bulaşmadan bu işleri çözebilir miyiz sorusu da insanın aklına gelmiyor değil.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bunlara alternatif bazı yöntemler elbette var ancak her birinin de kendisiyle birlikte getirdiği zorluklar oluyor. CQRS, GraphQL, veri çoklama(duplicate) ve bağlamların doğru bir şekilde tasarlanması örnek verilebilir. Dediğimiz gibi her birinin de beraberinde getirdiği zorluklar olsa da burada problemi doğru tespit edip bizlere hangi çözümün daha uygun olduğunu ortaya koymak işin teknik zorluğu diye düşünüyorum.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu arada bu çözümlerin birini kullandık diye diğerlerinden vazgeçmek zorundayız anlamına gelmez. Bunların birlikte kullanılması da mümkün. Örneğin bir servisten diğerine çağrıda bulunuyorsunuz ve sadece bir veriyi almanız gerekir, böyle bir durumda veri çoklama (Data Repliction) çözüm olabilir, ancak gittiğiniz servisten birçok önemli veriyi almanız gerekiyordur ve bütün bu verileri kendi tarafınıza taşımak doğru değil ise o zaman da isteği yapıp gelen veri kullanabilirsiniz. Bazen de  birçok servisten cevap almanız gerekiyordur o zaman da bunu gateway seviyesinde yapabilirsiniz. Dediğimiz gibi her birinin artı ve eksi yönleri olsa da bunun doğru veya yanlış bir cevabından ziyade size uygun olan cevabı önemli olur.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle iş ihtiyaçlarına göre bazı konularda farklı çözümler bulmamız gerekebilir. Çözümleri uygularken artı ve eksilerini iyi düşünüp kendi yapımıza uyarlarken, bunların eksi olan yöntemlerini nasıl sıfıra indirgeyebiliriz diye düşünüp o çözümleri de uygulamak genel manada güzel olur diye düşünüyorum.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü bir ayet-i kerime ve her probleme ayrı bir çözüm sunan Peygamber Efendimiz(s.a.v.) ile ilgili olan bir hadis yorumu ile bitirmek istiyorum.

> "Rabbinin yoluna hikmetle ve güzel öğütle çağır ve onlarla en güzel şekilde mücadele et. Şüphesiz ki Rabbin, yolundan sapanları da en iyi bilendir; hidayete erenleri de en iyi bilendir." (Nahl, 16/125)

> “Ey Allah’ın Resûlü! Hangi amel daha faziletlidir?” diye sorduğunda, farklı sahabilere farklı cevaplar verdiği görülür. 
- Örneğin: Biri için “Namazı vaktinde kılmak” 
- Bir başkası için “Ana babaya iyilik etmek” 
- Bir diğeri için ise “Allah yolunda cihad etmek” cevabını vermiştir. 
> Bu hadis, insanların durumlarına, ihtiyaçlarına ve önceliklerine göre çözüm sunmanın İslam’da önemli bir ilke olduğunu gösterir. (Buhârî, Edeb 1; Müslim, İman 137)


### 4. Achieving Data Consistency

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin dördüncü bölümünde, dananın kuyruğunun koptuğu bir konuyu ele alacağız: Veri tutarlığı. Önce bu konu neden önemli, sağlanmadığında ne gibi problemler yaşanabilir, ardından monolit yapılarda bunu nasıl sağlıyoruz ve son olarak da mikroservislerde ne gibi zorluklar yaşanıyor ve buna sunulan çözümler nelerdir gibi konulara değinmeye çalışacağız.


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Veri tutarlığı konusu gerçekten çok geniş, bu konuyu iyi anlayabilmek için öncelikle ACID ve CAP konularını iyi anlamak gerekiyor. Buralardaki başlıklar nelerden bahsediyor veya herhangi bir veri tabanını tercih ettiğimizde nereden feragat ettiğimizi doğru anlamamız gerekiyor. Bu hem monolith yapılar için hem de mikroservis yapılar için geçerlidir. Temel mantık oturduktan sonra geriye kalan işler yöntem ve prensiplerdir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Monolit yapılarda veri tutarlığını sağlamak mikroservis yapılara göre daha kolay. Bunun en önemli sebebi tek bir veri tabanının kullanılmasıdır. Böyle olunca tek transaction üzerinden tüm işleri bekletip tüm işlemler başarılı olduğunda bunu onaylıyoruz. Kullandığımız ORM araçları bunlara varsayılan ayarlarla bir yere kadar çözümler üretiyor. Sizin özel kullanımlarınıza göre bunlar tabii ki ayarlanabilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Monolit yapılardaki en kolay konu bile mikroservislerde karmaşıklaşabiliyor. Bunun sebebi birçok servis, veritabanı, farklı yapılar… Özetle büyük sistemlerde dolaşmak doğal olarak daha zor oluyor, ancak veri tutarlığı gibi bir yapı biraz daha zor olabiliyor. Özellikle birbiriyle haberleşen servisler arttıkça bunu yönetmek zorlaşıyor. Çünkü herhangi bir adımda meydana gelen hataya göre bir önlem almak lazım ve bu işleri geri almak gerekir. Bu yapılan geri almaların başarılı olacağını bir yere kadar garanti edebiliyoruz. Bunu sağlayan çözümlerimiz bulunmaktadır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mikroservislerde veri tutarlığı dediğimizde aklımıza ilk gelen şey, mülakatların gözbebeği, SAGA pattern olsa gerek. Saga denilince temelde iki şey karşımıza çıkar. İlki merkezi bir yapı kurgulayan Orchestration ve diğeri servislerin birbiriyle haberleştiği Choreography. Her iki yöntemin de kullanılacağı durumlar var. Orchestration 3–4 servis sonrası kullanımda tavsiye edilirken Choreography daha az servisin birbiriyle haberleşmede kullanılması tavsiye ediliyor. Çünkü Choreography'de tüm servisler birbirlerine gelerek bu işlemleri yönettiği için daha zor yönetebiliyor. Daha az servis kullanımında ise karmaşık yapıya girmeden kendi aralarında bunu çözebiliyorlar. Birçok yerde dediğimiz gibi probleme göre çözüm burada da var.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;İkinci bir yöntem ise 2PC (Two Phase Commit) tasarım şablonudur. Ya hep ya hiç kuralını işletir. Veri tutarlığı garantisi verir, ancak bütün işlemleri beklettiği için performans ile ilgili problemlere sebebiyet verebilir ya da her durum için uygun olmayabilir diyelim. Burada ödeme ile alakalı çok kritik bir işlem yapıyorsanız sizin için uygun olurken, daha toleranslı olabilecek işlemler için tercih etmeyebilirsiniz. Hem cam kenarı hem koridor olsun diyemiyoruz. Bir şeyi seçerken başka bir şeyden feragat ettiğimizi unutmayalım. Özetle bu yapı mikroservislerde çok fazla tercih edilmez bunun yerine eventual consistency (nihai tutarlılık) tercih edilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yardımcı çözümlerden biri olan Inbox/Outbox, eventual consistency sağlayan bir tasarım şablonudur. Event bazlı yapılan işlemlerde kullanılabilir. Bir tablomuz var, ilk atılan istek sonrası buraya bir kayıt atılır, eğer karşı tarafdan bu işlem başarılı bir şekilde dinlenerek işlem başarılı olursa bu sefer aynı tablodaki verimiz silinir. Bu da işlemin başarılı olduğunu gösterir, bir aksilik olduğu taktirde o veri orada kalır ve bunu farklı yöntemlerle eritmeye çalışırız. Inbox tasarım şablonu ise dinleyen taraftaki farklı bir tabloya kayıt ederek gelebilecek işlemlerin tekil olmasını sağlar.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Eventual consistency konusuna değinmişken, compensating transactions (telafi edilebilirlik) konusuna da dokunmakta fayda var. Eventual consistency tercih eden sistemlerin hata ve eksiklikleri telafi etmek için ortaya konan bir yöntemdir. Monolit yapılardaki rollback gibi düşünebilirsiniz ama rollback tek bir işlem üzerinden devam ederken (atomic) burada birden çok akış vardır ve tüm işlemlerin sonunda olumlu veya olumsuz verinin tutarlı olması sağlanır. Bu işlemi tam olarak geri almaktan ziyade çıkan sorunu/problemi bir şekilde telafi etmek olarak algılayabiliriz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Şimdi de biraz hata durumlarında ne gibi yöntemler öneriliyor konusunu konuştuktan sonra yazıyı ufaktan sonlandırabiliriz. Compensating transactions bu yöntemlerden biri. Saga ile kullanılarak bu işlemleri yapabiliriz. Bununla birlikte aşağıdaki noktalara da göz atabiliriz.

- Retry: İletilmeyen işlemlerin/kuyrukların belirli aralıklarla tekrar gönderilmesi. Bunlar gönderilirken karşı taraf da bunu yönetmeli yoksa birden fazla kez işleme alma tehlikesi de olabilir.
- Timeout: Cevap gelmediğinde sistemin işlemini iptal ederek bunun olmadığını kabul etmesidir.
- Circuit Breaker: Bir servisin başarısız olması durumunda belirli bir süre o servise gitmeme durumudur. Daha sonra tekrar deneyip servis ayağa kalktıysa oraya istek atabilir.
- İşlem Logları: İşlem logları ile nerede nasıl hata olduğunu tespit edip bu işlemleri tekrarlamak

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle monolith yapılarda veri tutarlığı nasıl sağlanırdan yola çıkarak mikroservislerde bunun farklı çözümleri ve zoruluklarını, problemlerle karşılaştığımızda nasıl çözümler üretebileceğimize dair bazı notlar paylaşmaya çalıştık. Umarım verimli olmuştur.


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerime ve hadis-i şerif ile bitirelim.
>"Allah, size emanetleri ehline vermenizi ve insanlar arasında hükmettiğinizde adaletle hükmetmenizi emreder. Şüphesiz ki Allah, size ne güzel öğütler veriyor. Şüphesiz Allah, her şeyi işitendir, görendir." Nisa Suresi, 58. Ayet


>"Kim bir işin başına geçirilirse, halk ona emanet edilmiş olur. O da ona karşı sorumludur." Sahih al-Buhari, Hadis 89

### 5. Centralizing Access
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin beşinci bölümünde olan merkezi erişim konusuna başlıyoruz. Burada ele alacağımız 3 kavram olan gateway, reverse proxy ve load balancer konuları olacak. Hepsi gelen trafiği karşılayıp gerekli servislere yönlendiren yapılar olmasına rağmen birbirlerinden farklılaştığı noktalar mevcut. Ayrıca böyle bir kurgunun ne gibi bir işlevi var, ne tür avantajlar sağlar, hangi işlemleri burada yapmalıyız gibi konulara da değinmeye çalışacağız.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Genel yapı itibariyle dışarıdan gelen isteklerin hepsini ilk karşılayan kale kapısı olarak düşünebilirsiniz. Bu kapılardan içeri girmeyen kimse kale içine de giremez. Öncelikle buralardan içeri giriş yapılmalı. İçeriye de rastgele gidilmiyor tabii ki. Gelen isteğin nereye gideceğini sorguluyor ve ona göre en uygun yere yönlendiriyor. Load balancer ile kullanılan bazı yönlendirme yöntemleri şunlardır:
Round Robin: Sunuculara sırasıyla yönlendirme yapılır.
Least Connections: Aktif bağlantısı sayısı en az olan sunucuya yönlendirme yapılır.
IP Hash: IP Hashlenerek aynı istemciden gelen tüm istekler buraya yönlendirilir.
Random: Gelen yükü sunuculara rastgele dağıtır.
Path-based Routing: Url tabanlı yönlendirme yapar. Mikroservis kurgusu için uygundur.
Geographical Routing: Coğrafi konuma göre en yakın sunucuya yönlendirir.
Content-based Routing: İsteğin türüne göre yönlendirme yapılır. Web veya mobil olarak ayrılabilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Her bir yöntem farklı ihtiyaçlar için kullanılabilir. Gelen isteklerin tek bir yerden geçerek dağıtılmasının birçok avantajı olabilir. Yukarıda da bahsettiğimiz gibi gelen bütün trafiği yönetir. Yetkilendirme işlemleri yapılabilir. Rate limiter kullanılarak gelen riskler azaltılabilir. Gelen giden tüm istekler loglanabilir. Bu ve benzeri işleri her bir servis için ayrı ayrı yapmaktansa tek bir yerden yönetebiliyoruz. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Birçok avantajı olsa da bazı dezavantajları da yok değil. Bu öndeki kapı düştüğünde bütün maçı kaybetmiş sayılabiliriz (Single Point of Failure). Projenin yumuşak karnı gibi düşünebiliriz (Bu durumda  birden fazla kapı kurarak, biri düşse dahi sistemin devamlılığını sağlamak lazım). Karmaşıklığı artırır ve dolayısıyla performans kaybı da yaşanır (sisteme göre tolere edilebilir veya en azından iyi gözlem yapılması gerekir).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Şimdi de bölümün başındaki birbirlerine benzeyen 3 yapıya değinelim.
* Api Gateway: Api çağrıları için özel olarak tasarlanmıştır. (Ocelot, Kong, Tyk)
* Load Balancer: Sunucuya gelen yükleri dağıtmak için tasalanmıştır. (Nginx, HAProxy)
* Reverse Proxy: İstekleri yönlendirmek için tasarlanmıştır. (Yarp, Caddy)

![Kaynak](Images/api.jpg)
    

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yukarıdaki resimdeki bazı kavramları kısaca açıklamak gerekirse;
* Authorization: Gelen kullanıcının yetkisinin kontrol edilmesidir.
* Rate Limiting: Gelen istek sayısını sınırlamasıdır. Böylece fazla istekler engellenebilir.
* Caching: Sık kullanılan verilerin depolanması ve böylece yanıt süreleri kısaltılır.
* Composition: Birden çok servisten gelen cevapların birleştirerek tek bir cevap olarak iletilir.
* Circuit breaker: Sistem aşırı yük aldığında, yük alan servisin istekleri geçici olarak durdurur.
* Retry: Hatalı bir istek olduğunda bunun tekrar olarak gönderir.
* Url Rewrite: Gelen url'lerin düzeltilerek istenilen formata getirilerek ilerletir
* Failover: Arıza durumunda yedek sunucuya otomatik geçişi sağlanır.
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle bahsedilen 3 kavram aynı işlemleri yapıyor gibi görünse de aslında birbirlerinden ciddi farkları olduğunu görmüş olduk. Projemizin ihtiyaçlarına göre en doğru yapı kurmamız gerekir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerime ve hadis-i şerif ile sonlandıralım.
> "Ey iman edenler! Mallarınızı aranızda haksız yere yediğiniz ve insanları yoldan çıkarmak için aldatıcı yollarla, aranızda birbirinizin malını yemeyin..." (Bakara Suresi, 2:188)

> "Birinizin diğerini yönlendirmesi, ona yardımcı olması, doğru yolu göstermesi, onunla işbirliği yapması hayırlıdır." (Buhârî, İlim, 30)

### 6. Separated Databases
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu bölümde mikroservis sistemlerde her servisin kendine ait veri tabanın olması konusunu ele alacağız. Bununla birlikte genel olarak veri tabanı seçimleri, veri senkronizasyonu ve çoklaması, ayrı veri tabanlarını yönetmedeki zorluklar ve bunlara yönelik çözümler hakkında konuşmaya çalışacağız.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Daha önceki bölümlerde de belirttiğimiz gibi, iyi bir veri tabanı tasarımı iyi bir projeyi oluşturmanın temel noktalarından bir tanesidir. İyi bir veri tabanı tasarımı ve belki de ondan önce doğru bir veri tabanı seçimi bu konuyu daha da önemli hale getirmektedir. Burada sadece veri tabanı ürünlerinden bahsetmiyorum, SQL ve NoSQL gibi veri tabanı türlerinin seçiminden de bahsediyorum.
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Her konuda olduğu gibi veri tabanını seçmeden önce ihtiyaçlarımızı doğru bir şekilde ortaya koymalıyız. Genel olarak bahsedersek veriler arası sıkı bir ilişki var ve veri tutarlığı sizin için çok kritik ise SQL veri tabanları tercih edilirken hız ve yüksek ölçeklenebilirlik gibi konular sizin için daha kritik ise NoSQL veri tabanları genel itibariyle daha çok işinizi görecektir. Türünü seçtikten sonra hangi ürünü kullanacağız ise yine ihtiyaçlarınıza göre değişecektir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Veri tutarlığı her proje açısından kritik olur, ancak bunu ne kadar tolera edebildiğiniz de bir o kadar önemli. Bazı sistemlerde her daim veri tutarlığı olması gerekirken bazı sistemlerde önceki bölümde de bahsettiğimiz nihai tutarlılık yeterli olabilir. Özellikle mikroservis sistemlerde nihai tutarlılık daha çok öne çıkıyor olabilir. Belki kaba bir tabir olacak ama arabanın hakkını vermek istiyorsanız nihai tutarlılık sizin için daha uygun olabilir. Bu konuya yukarıda bahsettiğimiz yazımızda çokça değindiğimiz için burayı geçiyoruz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mikroservis sistemlerde veri tutarlığı sağlamak takdir ederseniz ki daha zor olabiliyor. Bunun sebeplerinden biri de her servisin kendi veri tabanının olmasıdır. Veri tabanlarının ayrı olmalarının ölçeklenebilirlik, performans, sistemin bağımsız olması gibi avantajları var iken; veri tutarlığı, bakım zorluğu, operasyon bakım gibi yükleri de bulunmaktadır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peki veri tabanlarını ayırdık, servisler arası iletişim ve gerekli verilerin alınması konusu ortaya çıktığında neler yapabiliriz. Servis çağrıları yaparak verileri alabilir (senkron / asenkron) ya da veri çoklaması yapabiliriz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Veri çoklaması denilince akla CDC (change data capture) geliyor, ancak bununla birlikte ECST (event-carried state transfer) de akla gelmeli. İkisi de amaç olarak veriyi diğer veri tabanında çoklamayı hedeflerken takip ettikleri yollar nedeniyle birbirinden ayrılır. CDC veri tabanı bazında çalışırken (veri tabanında herhangi bir değişiklik olduğunda diğer veri tabanını günceller), ECST uygulama bazında çalışır (belirtilen tabloya kayıt atıldığında, event yakalanır ve diğer servis de kendi veri tabanını günceller). İkisinin de kendine göre hem kullanım alanları hem de bunları yapan araçları mevcuttur.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hangi durumlarda hangisini kullanmak daha mantıklı diye akıllara bir soru geliyor. Verinin okuması çok yoğun bir şekilde yapılıyorsa ve veriniz de sık güncellenen bir veri değil ise çoklama yapmak daha mantıklı durabilir, ancak verinin sık güncellenen bir veri ise o zaman her iki veri tabanı için de sürekli benzer işler yapacağınızdan çağrı yapmak daha makul olabilir. Ayrıca veri tutarlılığı sizin için daha kritik ise veri senkronize konusuyla uğraşmamak adına çağrı yapmak daha doğru olacaktır. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu seride çokça bahsettiğimiz ve muhtemelen de tekrar bahsedeceğimiz şey, aslında bahsedilen yöntemlerin birçoğunun doğru veya yanlış olmasından ziyade ihtiyaçlara göre olmasıdır. Hatta bu mikroservis mi monolit mi tercih etmeliyiz sorusunun cevabı için de böyledir. İhtiyaçlara göre çözümler elbette değişecektir. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle elimizden geldiğince servislerin kendi veri tabanları olduklarında avantajlarıyla birlikte ne gibi zorlukları olacağını ve bu zorluklara nasıl çözümler getirebileceği hakkında konuşmaya çalıştık. Umarız faydalı olmuştur.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerime ve hadis-i şerif ile noktayalım.


> "Ve yeryüzünde bozgunculuk yapmayın; oysa ki Allah, bozguncuları sevmez."
(Fasıl: 5, Ayet: 64)

> "Müslüman, diğer Müslümanların ellerinden ve dillerinden zarar görmediği kişidir."      (Sahih-i Buhari, Kitâbü'l-İman, Hadis No: 10/457)   

### 7. Arch API-based 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin yedinci bölümünde API tabanlı mimariyi ele alıyor olacağız. Önceki bölümlerde asenkron iletişimden, veri tutarlığının zorluğundan, ayrı veri tabanlarının kullanılmasından ve burada ortaya çıkan problemlerde ve hangi durumlarda hangi yapıların kullanılması daha uygun olur gibi konulardan bahsetmiştik. Bugün ise asenkron iletişimde API tabanlı iletişim var. Çeşitleri nelerdir, hangi durumalarda hangisi kullanılır, ne gibi avantaj ve dezavatajları var gibi konulara değinmeye çalışacağız.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API tabanlı sistemler temel manada servislerin bağımsız olarak tasarlanıp gerektiği durumlarda birbirleriyle iletişimde olmayı hedefler. Bu bağımsızlık servis bazlı ölçeklenebilirlik (her servisin getirdiği yüke göre büyüp küçülmesi), bir servisin bir sorumluluğu olması (single responsibility), teknoloji seçimi gibi avantajlar sağlar. Önceki bölümlerde bahsettiğimiz bu servislerin önüne de zorunlu olmasa da genel olarak bir API Gateway tarzında bir yapı kurulur. 
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API tabanlı iletişim denilince aklımıza gelmesi gereken ilk üç yapı RESTful, gRPC ve GraphQL'dir. Şimdi bu üç yapıya kısaca bakalım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RESTful API, HTTP protokolü üzerinden çalışan, web servislerde sıkça kullanılan hepimizin aşi olduğu JSON tabanlı bir yapıdır. HTTP protokolünde PUT, POST, GET gibi çeşitli metodları var. Kendine has belirli standartları vardır. Anlaşılması ve kullanılması kolay, herkesin hayatında yer alan, tüm dillerle entegre çalışabildiği için nerdeyse standart haline gelmiştir. Nesneler büyüdüğünde JSON yapılı olmasından kaynaklı hem gereksiz veriler gelebilir hem de sisteme ek bir yük oluşturabilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;gRPC, Google tarafından geliştirilmiş, hızlı ve tip güvenli bir yapı sağlar. Protobuf denilen bir yapı kullanır. Bu da JSON yapısına göre çok daha hızlı çalışır. Bu veriler ise JSON dosyalarında değil de proto dosyalarında saklanır. Öğrenmesi ve kavraması RESTful'a göre biraz daha zordur, dosya okuması da JSON'a göre biraz daha zordur.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphQL, Facebook tarafından geliştirilen ve RESTful'a alternatif olarak sunulmuştur. RESTful'da sunucunun döndüğü yapı sabit iken GraphQL'de ihtiyaca göre değişir. RESTful'da her istek için ayrı bir endpoint tasarlanırken, GraphQL'de ise tek endpoint üzerinden tüm veriler alınabilir. İstemci neye ihtiyaç duyuyorsa sadece o kısmı alıyor. Böylece endpoint şu kolon olsa iyi, bu kolon olmasa da olur gibi problemlerden de kurtulmuş oluruz. Böyle esnek bir yapı kurgular, gereksiz veriyi de önlem olur. Cachleme ve performans gibi konularda zorluklar çıkarabilmektedir. N+1 denilen bir problemi bulunur. Bu arada bunun da dosya yapısı RESTful gibi JSON'dır. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yukarıda da bahsettiğimiz gibi her birinin avantaj ve dezavantajları var. Sistemi kurgularken ihtiyaca göre tasarlamak en doğru yol olacaktır, ancak internal servisler arasında özellikle hıza ihtiyaç duyulursa gRPC kullanılıyor. Özellikle kullanımına aşina olundukça bu kullanımların zamanla artacağını düşünüyorum. Ancak dışarıya açılan durumlarda daha çok rest kullanıldığına şahit oluyorum. GraphQL ise daha çok front-end (single page) yapılarda daha çok tercih edilmeye başlanıyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Önceki bölümde de belirttiğimiz gibi servisler arası veri tutarlığı çok önemli ise veya o servisten gelen cevaba göre bir işlem yapılacaksa veya sistem sık kayıt atılan/güncellenen bir servis ise asenkron iletişimi kullanmak doğru olacaktır. Her şartta her yöntemi kullanmak değil, doğru yerde doğru yöntemi kullanmak bizim her zamanki parolamız olacaktır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerim ve hadis-i şerif ile bitirelim.

> "Ey iman edenler! Eğer bir fasık size bir haber getirirse, onu iyice araştırın. Yoksa, bilmeden bir topluluğa zarar verir ve yaptığınıza pişman olursunuz." (Hucurat Suresi, 49:6)

> "Her birinizin dili, kalbinden daha öncedir. Çünkü kişi dilinin ne söylediğine dikkat etmezse, kalbi o söze uymayabilir." (Tirmizi, Birr, 25)

### 8. Resiliency
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin sekizinci bölümüne hoş geldiniz. Önceki bölümlerde şimdiye kadar genel itibariyle veri üzerine daha çok yoğunlaştık, ancak bu bölümde herhangi bir sebepten dolayı cevap vermeyen servislerle ilgili ne yapabileceğimizi konuşacağız. Bu kavrama dayanıklılık (resiliency) diyoruz. Peki sistemlerin dayanıklı olabilmesi için neler yapabiliriz?

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dayanıklık denilince akla her ne kadar devre kesici (Circuit Breaker) gelmiş de olsa sistemi daha dayanıklo kılmak için birden fazla yöntem mevcut. Bunlardan kısaca bahsedip ne gibi sorunlara çözüm aradıklarını ele almaya çalışacağız.
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Devre kesici, bir sebepten dolayı bir serviste oluşan bir hatanın tüm sistemi etkilememesi adına o servise giden istekler durdurulur (kırmızı ışık). Tüm sistemi kaybetmektense o servis geçici olarak devre dışı bırakılır. Belirli bir süre sonra geçici olarak servis açılır (sarı ışık) eğer sistem düzeldiyse oradaki anahtar indirilir (yeşil ışık) ve sistem hayatına devam eder ancak sistemde hala problem var ise tekradan kapatılır. En bilindik olarak kullanılan araç ise Polly'dir. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retry, sistemde belirli sebeplerden dolayı oluşan kopmalarda isteği tekrar atmak isteyebiliriz. Çünkü bazen geçici problem yaşanır ve sonraki isteklerde oluşan hata tekrarlanmaz, ancak bazen hata kalıcıdır böyle durumlarda da denemeleri makul seviyede tutmakta fayda var. Polly burada da kullanılan bir araçtır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Timeout, yapılan istekler farklı sebeplerden dolayı geç cevap verebilir. Böyle durumlarda sistemi yormamak adına belirli bir süreyi geçen istekleri iptal edebiliriz. Ayrıca uzun süren işlemi bazen de kullanıcı iptal eder, burada da "CancellationToken" kullandığımızda bu çağrı timeout'a düşmeden direkt sonlanır ve sisteme ek yük yapmaktan kaçınmış oluruz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bulkhead, servislerin birbirinden bağımsız olmasıdır. Yani bir servis çöktüğünde ona bağımlı bir servis var ise onun da çökmemesi ve hayatına devam etmesi gerekir. Bunun için de neler yapabilirizi önceki bölümlerde epey bahsettik. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Failover, hata oluşan serviste yedek senaryosunun hazır olması durumudur. Sakatlanan futbolcunun yerine takım arkadaşının oyuna dahil olması gibi düşünebiliriz. Consul bu konuda iyi bilinen bir araçtır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Graceful Degredation, sistemde oluşan hatada bazı bölümlerin en azından sınırlı şekilde çalışabilmesidir. Kolu kırılan bir hastanın hayati fonksiyonlarını yerine getirmesi olarak düşünebiliriz. LauncDarkly gibi araçlarla yeni eklenen özelliklerin açılıp kapanması bu konuya örnek verilebilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Load balancing, daha önceki bölümlerde bahsettiğimiz üzere yükün servislere doğru ve adil bir şekilde dağıtılması veya fazla yük alan servisin ölçeklendirilmesini sağlar. En iyi bilinen araçlardan biri NGINX'tir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Monitoring ve Alert, sistemle ilgili olağanüstü durumlar yaşandığında bunun en azından kullanıcılardan önce haberiniz olması gerekir ve buna en hızlı şekilde müdahale ederek son kullanıcıya yansımadan problemi çözmek kritik bir davranıştır. Prometheus ve Grafana ikilisi piyasada en bilinen açık kaynaklı araçlardır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Distributed Tracing, servisler arası çağrıları takip edebilmek ve hangi aşamada, nerede tıkanma olmuş gibi bütün verileri size vermesi açısından çok kritiktir. Sizin o problemi tekrardan tespit etmenize gerek kalmadan size nerede problem olduğunu söylemeli ve ona göre hızlı müdahale yapabilmeliyiz. Son dönemlerde OpenTelemetry adından sıkça bahsettirmektedir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Health Check, servislerin ayakta olup olmadığını kontrol eder. Servislerin bağlı olduğu veri tabanı, kuyruk yapıları gibi bağımlılıklar var ise onlar da kontrol edilip her şey yolunda mı diye haber verir. Varsayılan olarak dotnet içerisinde gelen özelliği de kullanabilirsiniz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sistemlerde hata olmasını engellemek kadar, hata olduğunda bunu hızlı bir şekilde ayağa kaldırmak da bir o kadar önemlidir (Chaos Monkey göz atmanızı naçizane tavsiye ederim). Yukarıda bazı önlemlerden kısa kısa bahsetmeye çalıştık. Bu konuların bazılarına ileriki bölümlerde daha ayrıntılı değiniyor olacağız. Bölümün kapsamı gereği biraz daha özet şeklinde ilerledik. İhtiyaç duyulan kısımlar için hem sonraki bölümlerde hem de farklı okumalar yapmanız iyi olabilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerime ve hadis-i şerif ile bitirelim.


 > "Ey iman edenler! Sabır ve namaz ile Allah’tan yardım dileyin. Şüphesiz Allah, sabredenlerle beraberdir." (Bakara Suresi, 2:153)

> "Deveni bağla, sonra tevekkül et." (Tirmizî, Kıyamet 60)

### 9. Backward Compatibility

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin dokuzuncu bölümünde Backward Compatibility (geriye uyumluluk) konusuna bakıyor olacağız. Geriye uyumluluk sadece mikroservis sistemlerde değil, monolit sistemlerde de önemli bir yere sahip bir kavramdır. Dış servisler veya sistemler tarafından kullanılan uçlarımızda bir değişiklik yaptığımızda önceki halini bozmayacak bir şekilde geliştirilmesi gerekiyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Öncelikle konuyu kısaca monolit sistemler için ele alarak başlayalım. Bir modül veya sistemde kullanılan bir endpoint veya DTO birçok yer tarafından kullanılabilir, burada meydana gelen bir "breaking change" diğer tarafları da etkileyebilir. Bütün sistemi her zaman aynı anda güncellemek mümkün olmayacağından burada yapılan değişikliklerin geriye uyumlu olması lazım. Bununla birlikte dış bağımlılıklar ve istemcinin kullandığı noktalar da bu kapsama girer.
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yukarıda bahsedilen konular mikroservis sistemler için de geçerlidir. Ancak mikroservis sistemlerde birçok servis olacağı için bunların birbirleriyle konuşması diğer ekipleri de ilgilendireceği için yapılan geliştirme çok daha kritik olabilmektedir. Bununla birlikte monolit yapının tersine buradaki aksaklık belirli bir servisi etkilerken, monolit sistemde yapılan değişiklik tüm sistemi etkileyebilir. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peki geri uyumluluk diyoruz, buna sebebiyet veren durumların "breaking change" olduğunu ifade ettik. Kısaca eskiden sisteme gelen bir istemci yapılan değişiklikten sonra sistemden beklediği cevabı alamıyordur. Parametre sayısının veya tipinin değişmesi, DTO'dan herhangi bir alanın silinmesi ve zorunlu hale getirilmesi buna örnek olarak gösterilebilir. Yapılan her değişiklik de "breaking change" manasına gelmez bunu da hatırlatmakta fayda var. Bunların olmaması için birkaç çözümü ele alalım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API Versiyonlama, herhangi bir endpoint'te yapılan bir geliştirme "breaking change" (kırılganlığa) sebep oluyorsa endpoint'lerimizi değiştirmek yerine onları versiyonlayabiliriz. Sistemi tasarlarken buna uygun olarak geliştirmek gerekir.  Bunu yapmanın farklı yöntemleri olsa da önemli olan temel mantık olduğu için ayrıntılara girmiyoruz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kontrakların iyi tasarlanması (DTO), yukarıda da berilttiğimiz gibi DTO'lardan herhangi bir alan silinmesi, bir alanın zorunlu hale getirilmesi buna sebebiyet verir. Buna çözüm olarak yeni alanların eklenirken varsayılan olarak değer atanması, zorunlu olmayan alanların eklenmesi ya da kullanılmayan alana "deprecated" demek doğru olan yöntemlerdendir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tolerant Reader, istemci tarafından alınan bir önlemdir. Gelen veride beklediğinin dışında alanlar eklenmiş olsa da eski istemciler doğru bir şekilde çalışmaya devam edebilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Feature Flag, yeni eklenen özellik (feature) hayata alındıktan sonra o özelliği kapatıp açılabilmesine denir. Yapılan testlerden dahi kaçsa ortaya çıkan sorun sonrası bu flag'ı kapatarak sistemin eskisi gibi çalışması hedeflenir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A/B testleri, hayata geçirdiğimiz bir özelliği, bütün kullanıcılara/istemcilere açmak yerine öncelikle belirli bir gruba açmayı hedefler. Her şey yolunda gittiyse yavaş yavaş tüm herkese açılır. Bir aksilik olursa geri dönüş planları hayata alınır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tüm bu çözümler kulağa hoş gelse de tahmin edeceğiniz üzere bunların da birlikte getirdiği maliyetler oluyor. Bunlardan bazılarını ele alacak olursak;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Eski ve yeni sürümler nedeniyle test süreçleri ve buradaki maliyetler artmaktadır. Doğal olarak kodun kendisi de karmaşıklaşmaktadır, bunun da bakım maliyeti artmaktadır. Sürüm yönetimi de zorlaşmaktadır.Feature flag'ların bakımı yapılmadığı takdirde kodun okuması zorlaşmaktadır (Bunu birebir yaşıyoruz. Belirli aralıklarla kontrol etmekte fayda var. İkinci madde ile de direkt bağlı. Ayrıca testleri yaparken ff açık mı kapalı, test ve prod ortamları senkron mu gibi konuları da ihmal etmemek lazım.).
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle önerilen çözümlerin faydası olsa da bunları belirli bir standartta yaparak ve gerektiğinde bunlar refactor ederek veya kullanılmayan yapıları kaldırarak burada oluşabilecek maliyetleri de düşürmenin faydaları olacaktır. Ayrıca yukarıda da belirttiğimiz gibi "Deprecated" attribute, dokümanları güncel tutarak ve semantic versiyonlama yaparak oluşabilecek maliyetleri indirgeyebiliriz.
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerim ve hadis-i şerif ile bitirelim


> "Onların işleri, aralarında şûra (danışma) iledir." (Şûrâ Suresi, 42:38)

> "Akıllı kişi, nefsini kontrol eden ve ölümden sonrası için çalışandır. Aciz kişi ise, nefsinin hevasına uyan ve Allah’tan (hiçbir gayret göstermeden) temennilerde bulunandır." (Tirmizî, Kıyamet, 25; İbn Mâce, Zühd, 31)

### 10. Documenting Contracts
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin onuncu bölümünde dokümantasyon ve uri tasarımı konularını ele alacağız. Diğer konulara oranla az önemli gibi gözükse de büyüyen projelerde bu konu beklediğimizden çok daha önemli hale gelmektedir. Özellikle farklı takımların sürekli senkron veya asenkron bir iletişim sürdürmesi yerine bu konuya eğilmek çok daha kıymetli olacaktır. Ayrıca sonradan projelere katılacak olan arkadaşlara da can simidi olabilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bugünkü konumuz da diğer konular gibi mikroservise has bir konu değildir, ancak yapı büyüdükçe bu yapılan işlerin önemi daha iyi anlaşılacaktır. Belirli bir standardın dışına çıkıldı mı bunları yönetmek oldukça zorlaşıyor. Ekipler arası geçişler, değişimler olsa da aslında bütün projelerin tek bir ekipten çıkıyormuşçasına düzenli görünmesi o işteki başarımızı da artırmaktadır.
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;İyi bir Uri tasarımında öncelikle tutarlılık olmalıdır. Uçlarda nasıl bir isimlendirme takip edeceğiniz ya da fiiller ile başlamak yerine kaynakların isimlerini baz alacağınız gibi kurallarınızın olması önemli. Bahsedilen konuda "best practice"ler zaten mevcut. Onları takip etmekte de fayda var. Bir önceki yazımızda bahsettiğimiz konulardan biri olan versiyonlama yine çok önemli bir nokta. HTTP metodlarını doğru şekillerde kullanmak da önemli noktalardan biridir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;API spesifikasyonu dediğimiz API uçları dokümante etmek çok önemli. Open API bunları belirli bir standarda getirip Swagger gibi araçlarla bunu hızlıca çözebiliriz. Neredeyse tüm projelerin vazgeçilmezi olması ise mutluluk verici. Ayrıca sadece Rest api için değil, GraphQL ve hatta gRPC için farklı araçlarla bunları bize sağlayabiliyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Önceki bölümde ele aldığımız "back compatibility" ve CDC testleri ile önceki versiyonlara ait uçları bozmamak, istemcilerin doğru bir şekilde iletişimlerine devam etmeleri açısından önemlidir. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dokümanları yazmak çoğu geliştiricinin ihmal ettiği ve belki de sıkıldığı bir şey olsa da daha da zoru maalesef o dokümanı güncel tutabilmektir. Güncel olmayan doküman bazen olmayan dokümandan daha can sıkıcı olabiliyor. Çünkü bizler onu doğru kabul edip bazı yorumlarda veya çıkarımlarda bulunarak yanlışlığa sebebiyet verebiliriz. Geliştirici yazdığı kodun testini, dokümantasyonunu yazmadan ve onu canlıya göndermeden işinin bitmediğini sürekli hatrında bulundurmalıdır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bir önemli nokta da yazdığımız dokümanları yazıyor olmak için yazmamak. Eğer böyle yapıyorsak belki de hiç yazmamak daha iyidir mi demeliyiz yoksa kötü de olsa bir yerden başlayıp onu alışkanlık haline mi getirmeliyiz kısmını sizin yorumlarınıza bırakıp iyi dokümanın bazı özelliklerine kısaca göz atalım.

* Tüm uçlar detaylı olarak alınmalı, gönderilen parametreler ve cevap anlatılmalıdır.
* Uçların hangi durumlarda hangi status kodlarını da döneceği önemlidir.
* Varsa hata kodları ve bu kodlarının ne anlama geldiği ve hangi koşullarda karşılaşıldığı belirtilmeli.
* Auth sistemlerinin gereksinimleri belirtilmelidir.
* Belirli isteklerden sonra rate limit koşulları varsa bunları da belirtmek iyi olur.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle iyi ve tutarlı bir dokümantasyon sadece geliştiricilerin değil, tüm ekibin en önemli işlerinden biri olmalıdır. Bunu şirketin veya en azından ekibin kültürü haline getirdiğinizde ne kadar başarılı işler ortaya çıkardığınızı ileride çok daha net bir şekilde kendiniz de göreceksiniz. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerim ve hadis-i şerif ile bitirelim.

> “Hiç bilenlerle bilmeyenler bir olur mu? Ancak akıl sahipleri öğüt alır.” (Zümer Suresi, 9. Ayet)

> "Bir kimse ilim öğrenmek için bir yola girerse, Allah ona cennete giden yolu kolaylaştırır." Davud, İlim, 1; Tirmizi, İlim, 2)

### 11. Centralized Logging 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin on birinci bölümünde loglama konusunu ele alacağız. Loglama küçümsediğimiz ama başımız belaya girdiğinde kıymetini anlamaya başladığımız can simidi bir konu. Monolit sistemlerde de önemlidir ancak log yazılması, logu takip etmesi ve gerektiğinde debug (iyi developer debug yapar, daha iyi developer log okur) yapması daha kolaydır. Ancak sistem büyüdükçe bu işlemi yapmak dahi bir soruna dönüşebiliyor. Özellikle servisler arası istekler gidip geliyorsa bunu takip etmek daha da zorlaşıyor. Bunlar için ne gibi çözümler var merak ediyorsak buyurun başlayalım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Monolit sistemlerde logları daha kolay bir şekilde tutabiliyorken, mikroservis yapıda bütün servislerden toplayıp bunu merkezileştirmek neredeyse bir zorunluluk. Aksi halde bu işi yönetmek çok zorlaşıyor, hatta imkansızlaşır. O yüzden de logları merkezileştirmek lazım. Merkezileştirilen logları görüntülemek ve aradığını bulmak da ayrı bir zorluk tabii ki :) Mantık bu şekilde olsa da bunu yapmanın farklı şekilleri var. Bunu yapmanın en yaygın yöntemlerinden biri ELK( Elastic, Logstash ve Kibana).
 - Elastic Search, toplanan verileri depolayan ve arama yapabildiğimiz bir araçtır. Aramayı hızlandırmak için indeksler kullanır. Kendi içinde oldukça geniş bir dünyası var.
 - Logstash, servislerden gelen logları uygun formata getirerek Elastic'e iletir.
- Kibana, toplanan verilerin görselleştirilmesini sağlar.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Önemli olan bir diğer konu ise tracing dediğimiz izleme olayıdır. Yukarıda da bahsettiğimiz servisler arası devam eden isteklerin takibi oldukça önemlidir. Hata veya problem nereden geldi, nereye gitti, nerede ne olduğu kısımları çok önemli oluyor. Özellikle bu tarz durumlarda debug yapmak da oldukça zordur, ki aynı durumu tekrarlamak da her zaman mümkün olmayabilir. Önceki yazımızda da bahsettiğimiz OpenTelemetry gibi araçlar var. Bunun için bir araç kullanmak istemezseniz veya özelleştirme gibi bir ihtiyacınız olursa "CorrelationID" konusunu hayatınıza almanız gerekecektir. OpenTelemetry gibi araçlar bunu sizin yerinize yapar.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mikroservis sistemlerde log seviyesi gibi bir konu bile çok önemli hale gelmektedir. Piyasada iyi bilinen bir şirket için "assignment" yapmıştım, bana logun tipiyle ilgili bir soru sorduklarında, kendi kendime, kocaman bir proje yapmışız, üzerine hiç düşünmediğim log tipini mi soruyorlar demiştim. Büyük sistemlerde daha aktif çalışmaya başlayınca ne kadar haklı olduklarını daha net gördüm. Yoğun istek alan sistemlerde her şeyi logladığınızda veya uygun olmayan tiplerle logladığınızda bu da sizin başınıza iş açabiliyor. Bulmak istediğiniz log için çırpınıp durabiliyorsunuz. Bu konuya da dikkat etmekte fayda var.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Önemli konulardan biri de logların yapısal olarak tutulması. Json yapısında olması önemli bir avantaj sağlayacaktır. Hem sorgulama yaparken hem parçalarken hem de analiz ederken işleri kolaylaştırmaktadır. Bunlar artık neredeyse varsayılan olarak gelen çözümler olsa da hatırlatmakta fayda var.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Logların saklama süreleri bile önemli olabilmektedir. Monolit servislerde yıllarca saklanan loglara bile denk gelmiştim, ama mikroservis sistemlerde bunların hepsi maliyet ve logların saklanma süreleri olmalıdır. En azından kritik olmayan noktaların saklanma süresini kısa tutmak, belki de çok kritik olan logların belirli bir süre sonra arşivlemek bile çözüm olabilir ama mümkün ise bunları bir standarta oturtmak güzel olur. Özellikle IoT sistemlerde cihazlardan gelen istek ve cevapları logluyorsanız bunlar çok kısa sürelerde çok büyük rakamlara ulaşabilmektedir. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Loglama başlı başlına kritik bir konu ancak özellikle tekrar etmekte (repro) zorlanacağınız konularda elini ayağınız oluyor. Bizim architect olan abiye (Gökhan Demir) herhangi bir soru sorduğumuzda "loglar ne diyor" cümlesi benim bu konuya olan bakış açımı ciddi manada değiştirdi. Arkadaşlar da bana bir şey sorduğunda veya ben kendim bir problemle karşılaştığımda varsayılan olarak soruyorum. Çünkü elinizde log yoksa konuşacaklarınız varsayımdan öteye geçmeyebilir. Öncelikle logla, hatadan emin ol sonra da çözüm üzerine çalış bizim temel prensimiz olmalı.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle basit gibi görünen bazı konular bile mikroservislerle çalışmaya başladıkça ne kadar zor olduğunu daha net görüyorsunuz. Yazdığımız bir kod parçasıyla ilgili bir problem yaşandığında onunla ilgili loglara baktığımda bir şeyler anlayabiliyorsam veya en azından problemi saptayabiliyorsam doğru yolda olduğumuzun göstergesidir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Not: Şu şaheser [yazıyı](https://medium.com/bili%C5%9Fim-hareketi/da%C4%9F%C4%B1t%C4%B1k-uygulamalar-d%C3%BCnyas%C4%B1nda-i%CC%87zleme-merkezi-log-sistemi-ve-i%CC%87z-s%C3%BCrme-8e62c138023b) okumanızı naçizane tavsiye ederim.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yazıyı birer ayet-i kerim ve hadis-i şerif ile bitirelim.


> "Kim zerre miktarı hayır işlerse onu görür. Kim de zerre miktarı şer işlerse onu görür." (Zilzâl Suresi, 7-8. Ayetler)

> "İlim yazıyla kayıt altına alınır." (Darimî, Mukaddime, 42)

### 12. Cloud-Based Infrastructure

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin on ikinci bölümünde bulut tabanlı sistemleri konuşuyor olacağız. Bu yazıyla birlikte biraz daha devops konuları hakkında konuşmaya başlıyor olacağız. Mikroservis sistemlerde platform/devops ekibiniz olmadan bu işlerle uğraşmak zor/yorucu olabilir. Monolit sistemlerde bu işleri nasıl yapıyorduk da neden şimdi böyle bir ihtiyacımız var? Hazırsanız cevap bulmaya çalışalım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Her sistemde olduğu gibi monolit sistemlerde de canlıya çıkmak çok stresli bir durum, hatta mikroservisten daha stresli bir durum olduğunu düşünüyorum. Çünkü tek bir proje var ve bir hata bütün projenin patlamasına sebebiyet verebilir. Böyle bir durumda da geriye dönmek (rollback) gerekir ve bunun da kendisine göre elbette maliyetleri oluyor. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Her ne kadar tüm sistemi etkileme açısından çok daha sancılı olsa da bir projeyi canlıya almak birçok servisi canlıya almaktan elbette daha kolaydır. Tabi bunu nasıl yaptığınıza göre de değişir. Eğer projeleriniz IIS veya kendi sunucularınız üzerinde manuel olarak deploy ediyorsanız bu süreç hata yapmaya çok açık ve maalesef bunu yapan hala çok şirket var. Bu işler tabii ki ihtiyaca göre değişir ama en azından bu süreci otomatize etmek gerekir diye düşünüyorum.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mikroservis sistemlerde yine aynı yöntem kullanılamaz mı? Tabii ki kullanılabilir ama çok yorucu ve yönetmesi imkansız bir duruma dönüşebilir. Özellikle servisler arttıkça buradaki ihtiyaçlar artacak, servislerin kolayca ölçeklenmesi ihtiyacı olacak, bir problem olduğunda çok hızlı bir şekilde geri alınması gerekecek veya geçişlerde kesintinin minimum olması gibi durumlar ortaya çıkıyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bulut tabanlı sistemler, bu soruların birçoğunu bizim yerimize çözüyor. Birçok farklı hizmet ve destekleri oluyor. Yaptığımız işler oldukça kolaylaşıyor, ama her şey gibi bunun da bir maliyeti var. Her ne kadar "kullandığın kadar öde" ile yola çıkılsa da kısa vadede faturalar beklediğinizden fazla gelebilir. Bu tarz durumlarda ya danışmanlık alınması gerekiyor ya da buna bakan bir ekibiniz olması kaçınılmaz oluyor. Bunlar da işin duygusal boyutu ama her zaman dediğimiz gibi biraz ihtiyaç meselesi...

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bulut tabanlı sistemleri daha etkili kullanmak için container (en bilinen aracı Docker) ve orkestrasyon (en bilinen aracı kubernetes) konularından da bahsetmememk olmaz. Sektörün standardı haline gelmiş bu araçlar sayesinde Docker ile uygulamaların taşınabilirliği sağlanırken, k8s ile container'lerin ölçeklenmesi ve yönetimi sağlanır. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Buralar gerçekten derya deniz, ben de devops kaynaklı biri olmadığım için bu konulara bir devopsu kadar hakim olmasam da son dönemlerde hem AWS hem GCP hem de Huwaei ile çalışan ekiplerde ayrı ayrı geliştirmeler yapıp aşina oldum. Buradaki rahatlıklara şahit olduğumuz kadar farklı konulardaki sıkıntılara, yüksek gelen faturalara ve bunlara harcanan mesailere de elbette denk geliyoruz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bulut bilişimlerinin kendine ait birden fazla kategorisi var. Belki birkaçını duymuşsunuzdur, ancak biz yine de kısaca bir açıklayalım.
![As a Service](Images/as-service.png)

- IaaS (Infra as a Service): Alt yapının bir hizmet olarak sunulması. Buradaki bütün sorumluluk sizde oluyor. Daha esnek ve kontrol daha fazla sizde oluyor, ancak yönetim maliyeti de size kalıyor. Büyük sistemler için daha uygun fiyatlı ve tercih edilebilir.
- Paas (Platform as a Service): Platform hizmetinin sunulması. Siz istediğiniz özellikleri belirtiyorsunuz, gerisine çok karışmıyorsunuz. Yönetimi ve bakımı kolay, ancak maliyeti küçük ve orta boyutlu sistemlerde daha kullanışlı olabilir.
- FaaS (Function as a Service): Platformun bir tık ötesi :) Siz fonksiyonunuzu yazıyorsunuz, etliye sütlüye karışmıyorsunuz. İleride buralar değerlenecek deniliyor.
- BaaS (Backend as a Service), DaaS (Data as a Service), CaaS (Container as a Service), SaaS (Software as a Service) gibi farklı farklı kategoriler de mevcut. Her birinin kendine göre kullanım alanları, avantaj ve dezavantajları var. Şuraya(üstteki resim de aynı siteden) göz atmakta fayda var.
    Yukarıdaki resmi dikkatli incelediğimizde aslında birçok soruya da cevap almış oluyoruz. Ekibin, projenin, isterlerin ihtiyacına göre bizler mi bu işi yönetmeliyiz yoksa araçlara mı devretmeliyiz kararını en doğru şekilde vermekte fayda olabilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle monolit sistemlerde bazı konuları kendiniz yönetseniz bile mikroservis tabanlı projelerde, bunu yapmak çok da mümkün değil. Görünen de kontrolü yavaş yavaş araçlara verdiğimiz. Şahsi fikrim de bunun daha mantıklı olduğu yönde. Asıl işimize odaklanmak ve her iş için tekerliği yeniden icat etmemek daha mantıklı gibi duruyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerim ve hadis-i şerif ile bitirelim.
> "Şüphesiz Allah, size emanetleri ehline vermenizi ve insanlar arasında hükmettiğinizde adaletle hükmetmenizi emrediyor." (Nisa Suresi, 4:58) 
> "Kolaylaştırınız, zorlaştırmayınız; müjdeleyiniz, nefret ettirmeyiniz."(Buhari, İlim, 11; Müslim, Cihad ve Siyer, 6)

### 13. Deployment Automation

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin on üçüncü bölümünde otomatik deployment süreçlerinden bahsetmeye çalışacağız. Önceki bölümde de bu konuya ufaktan değinmiştik. Şimdi ise daha detaylı bakmayı deneyeceğiz. Monolit sistemlerde olursa güzel olur dediğimiz yapı, mikroservis sistemlerde bu süreç zorunluluk haline geliyor. Mikroservis mimarisinin avantajlarından biri de gün içinde sık sık ve küçük paketler halinde canlıya çıkabilmektedir. Bunu yapabilmeniz için de bu süreçler kaçınılmaz oluyor. Hazırsak başlayalım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Monolit uygulamalarda manuel deployment zor olur diye belirtmiştik, bunu yapmanın farklı şekilleri var. IIS üzerinden dll kopyalarak yapan da var, FTP ile dosya atan da var, bu iş zor oluyor diyerek otomatik deployment (prod ortam için tetikleyerek olabilir, çünkü monolit yapı tek bir commit ile çalışmaz hale gelebilir) yapan da oluyor. Ancak mikroservis dünyasında bu bir seçenek olmaktan çıkıp zorunluluk haline gelmektedir.
    Konunun temelini CI (Continuous Integration) ve CD (Continuous Deployment/Delivery) süreçleri  oluşturur. Zaman zaman birbirlerine de karıştırıldıkları da oluyor. Yukarıda bahsettiğimiz kodun sık aralıklarla sürüm kontrol (Git gibi) versiyonlama sistemlerine gönderilmesine denilirken, CD ise bu kodun her zaman deploy edilmeye hazır bulunmasına denir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu sürecin bize ne gibi faydaları olur derseniz, kodu sık sık canlıya göndermek olabilecek problemlerin saptamasını hızlandırır. Ekipler arası kod entegrasyonu karmaşıklığı azalır. Testleriniz de varsa gönderilen kodu kontrol ettiği için kod kalitesini artırır. Bunların sağladığı yararlarla birlikte kod her zaman deploy edilmeye hazır bir halde olur. Geliştirilen işler hızlı bir şekilde canlıya çıkarak müşteriyi de memnun etmiş olursunuz, kendinizi de memnun etmiş olursunuz (sizleri bilmem ama yazdığım bir kod farklı sebeplerden bloklanıp uzun süre bekleyip canlıya gitmediğinde stres oluyorum :) )...
    
![https://www.turing.com/kb/top-cicd-tools-you-should-learn-in-2022](Images/as-service.png)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peki bunları nasıl ayarlarız derseniz ilk akla gelen araç Jenkins olur herhalde. Açık kaynaklı, çok esnek her türlü taklayı atabileceğiniz bir araç, ancak konfigürasyon, yapılandırma gibi kısımları öğrenme açısından zor olabilir. Bununla ilgilenen bir ekibiniz yoksa bunu kullanmak yorabilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Gitlab CI/CD ve Github Actions yine bu konularda sizlere yardımcı olan araçlardan. Bizler projeleri Github üzerinde tuttuğumuz için bizim için Github Actions kullanmak oldukça pratik bir durum oldu. Kendiniz de yeni bir akış oluşturmak istediğinizde size bir template sunuyor ve kolaylıkla konfigürasyonları yapılandırabiliyorsunuz. Daha sonra otomatik veya elle tetikleme veya farklı ortamlar için farklı süreçleri ele alabiliyorsunuz. Bunun dezavantajı ise yeterince esnek olmayabilir ve daha çok kendi repolarındaki projelere yöneliktir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Circle CI, TeamCity, Bamboo yine bilinen araçlardan. Bununla birlikte bulut tabanlı servislerin de kendi çözümleri bulunmaktadır. Azure DevOps, AWS CodePipeline de bunlara örnek çözümlerdir. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle her bir çözümün kendine göre avantaj ve dezavantajları tabii ki vardır. Buradaki çözüm ekibiniz yetkinliklerine ve projenin isterlerine göre kendinize en uygun olanı aracı seçmeniz gerekmektedir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerime ve hadis-i şerif ile bitirelim.

> "İş konusunda onlarla istişare et. Kararını verdiğin zaman ise artık Allah’a tevekkül et. Şüphesiz Allah, tevekkül edenleri sever." (Âl-i İmrân Suresi, 3:159)

> "İşlerin en hayırlısı, az da olsa devamlı olanıdır." (Buhârî, Rikak 18; Müslim, Müsâfirîn 217)

### 14. Configuration Management

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin on dördüncü bölümünde mikroservis sistemlerin ayar yönetimi kısmına odaklanıyor olacağız. Sistemlerin dayanıklı, ölçeklenebilir ve bağımsız olarak dağıtılabilmesi için gerekli ayarların nasıl tutulması gerektiği konusuna değineceğiz. Bunun için ne gibi yöntemler mevcut, kullanılan araçlar nelerdir gibi bazı sorulara da cevap arayacağız. Hazırsak başlayalım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Diğer yazılarımızda olduğu gibi öncelikle monolit sistemlere bakalım. Uygulamaların farklı ortamlarda doğru bir şekilde ayağa kalkması her proje için kritik bir nokta ve bunun böyle olmadığı projelere sanırım denk gelmiyoruz artık. Daha önce de değindiğimiz gibi monolit sistemlerde meydana gelen tek hata sistemin tek başına çökmesine sebep olabilir. Bu yüzden belki de bazı ayarlar ve konular monolit sistemde çok daha önemli ve kritik olabiliyor. Ortamların tutarlı olması, dağıtım konularındaki risklerin azalması gibi faydalar sağlar.
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Araya girip bir anımı paylaşmak istiyorum. Üzerinde çalıştığımız mikroservis projesini canlıya çıkmak zorundaydık ve uygulamayı başka bir şirketten teslim almamız da gerektiği için bulut üzerinde sadece prod ortamımız vardı. Bu süreç yaklaşık 15 gün sürdü, ancak o dönemlerdeki stresi hatırladıkça karnım ağrıyor. Ekibin yaptığı bütün geliştirmeleri tek tek inceliyor, çok kontrollü bir şekilde canlıya çıkmamız gerekiyordu, ama sonuç olarak kod maalesef canlı ortamda test ediliyordu. Hem bizim geliştirme hızımızı düşürüyor, hem test ekibi tarafından test edilmeyen kodun canlıya gitmesine sebep oluyor hem de bize ağır sorumluluk biniyordu. Bu konunun varlığının nasıl bir nimet olduğunu tekrar hatırlamış olduk. Acı bir gülümsetti yine :)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Şimdi de mikroservis tarafına geçecek olursak, sistemde birçok servis olacağından en kolay işler bile zorlaşıyor diyebiliriz. O yüzden bu tarz ihtiyaç durumlarında ilk akla gelen şey bunların nasıl merkezileştirilmesi. Merkezileştirme dediğimizde de kendi çözümlerimizle birlikte bu konuda ortaya çıkan birçok araç vitrinlerdeki yerini almış oluyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bulut tabanlı sistemler kullanıyorsanız her birinin kendine ait çözümleri var. Genelde "secret manager" olarak geçmektedir. Ayrıca Github'un kendi çözümü de mevcut. Proje veya kuruluş nezdinde bu değerleri verebiliyoruz. Ayrıca Vault ve Consul gibi bağımsız araçlar ile de bu hassas verileri yönetebilirsiniz. Özellikle prod ortamları için hiçbir hassas veriyi konfigürasyon dosyalarında tutmuyoruz, pipeline aracılığıyla bunları eziyoruz. Projenin hiçbir yerinde bu veriler tutulmamış oluyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dev, test, preprod ve prod ortamlarının olması monolit sistemlerde olduğu gibi mikroservis yapıda da kritik bir nokta. Farklı olarak bunu her projede yönetebildiğimiz gibi merkezi olarak da yönetebiliriz. Her iki yöntemin de kendine göre avantaj ve dezavantajları var. Global bilgileri merkezi olarak tutup, yerel verileri proje bazlı tutuyoruz. İhtiyaçlarınıza göre birini seçebilir veya hibrit çözüm geliştirebilirsiniz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Konfigürasyon dosyalarında tutulan bilgiler değiştirildiğinde bunların projede algılanması için servislerin yeniden çalıştırılması gerekmektedir. Özellikle bulut sistemler geçişlerde kesintiyi minimize etse de bu bazen istenilen bir durum olmaktan çıkıyor. O yüzden "hot reload" dediğimiz bir yapı ile servisler yeniden başlatılmadan ayarların algılanıp değişikliğin yansıtılması da istenebilir. Bahsettiğimiz araçların bazıları buna yapabilmektedir. Direkt bu konuyla alakalı değil ancak YARP (reverse proxy) hot reload çalışarak konfigürasyonda yapılan değişikliğin servisleri yeniden başlatılmaya ihtiyaç duymadan algılar ve bunu hayata alır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle konfigürasyonların tutulması ve kullanılmasının farklı yöntemleri olsa da mikroservislerde bunları merkezileştirmenin önemi üzerinde durmaya çalıştık. Ayrıca farklı ortamlarda yapılan geliştirmelerin de süreçleri nasıl daha dayanıklı kıldığını görmüş olduk.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerime ve hadis-i şerif ile bitirelim.

> "İyi amelleri en güzel şekilde yapın." (Müminun, 23:51)

> "Bir grup insan, lider olmadan bir araya gelirse, şeytan onlara hükmeder." (İbn Mace, Hadis No: 3942)

### 15. Service Registry & Discovery

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin on beşinci bölümünde servislerin birbiriyle iletişim kurarken dinamik bir şekilde bunu yapmanın yoluna değineceğiz. Monolit sistemlerde böyle bir ihtiyaç genel itibariyle bulunmazken, mikroservis sistemlerde servislerin çokluğu nedeniyle önümüze çıkmaktadır. Hazırsak başlayalım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Öncelikle registry ve discovery kavramlarını ele alalım. Registry, kayıt olma anlamına gelir. Bununla birlikte olarak da servislerin sisteme kaydedilme kısmını ele alıyor. Discovery ise keşfetme anlamına gelir. Kaydedilmiş bilgileri dinamik olarak istenilen servise döner.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu işlemleri neden dinamik olarak yapma ihtiyacı ortaya çıkıyor dediğimiz noktada,

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kalabalık servis yapısında IP değişse dahi var olan adresler doğru bir şekilde gelmelidir. (Bunu "magic string" konusuna benzetiyorum. Her yerde string ifadeyi kullanmak yerine belki onu bir sabit (const) değişkene atayıp birçok yerden kullanmak ve gerektiğinde sadece bir yerden değişmesi yeterli olur. Mikroservis sistemlerde merkezileştirmek çok önemli bir nokta).
Gelen yükü birden fazla instance sahibi olan servislerde uygun olana yönlendirir (Bunun da farklı şekilleri vardır. Meraklısı şu yazımıza göz atabilir).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bağımsızlık ve esneklik yine mikroservis sisteminin temel konularından ve bu şekilde servisler arası bağımlılığı azaltmış oluruz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu işleri yapan bazı araçlar Consul, Eureka ve Zookeeper olarak karşımıza çıkmaktadır. Bu araçlar birçok dil için kullanılsa da  Eureka ve Zookeeper daha çok java ile anılıyor iken Consul daha çok dotnet dünyasında kendi adından bahsettiriyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bahsettiğimiz konular arasında açıkçasını söylemek gerekirse en az ihtiyaç duyacağımız konu olabilir. Buna rağmen bazı durumlarda adresleri değiştirmek istediğimizde ilgili projelerde tek tek değişiklikleri yaparak deploy işlemlerini yapmak ve bunu manuel olarak ilerletmenin zorluğunu yaşadık. Tabii biraz da attığın taşın ürküttüğün kuşa değer mi konusunu da göz önünde bulundurmanın faydalı olacağını düşünüyorum.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Belki kabaca bir tabir ile gelen servislerin kaydedilmesi (post) ve daha sonra ihtiyaç halinde bu verilerin çekilmesi (get) olarak ele alabiliriz. Tabii bununla birlikte yukarıda da bahsettiğimiz farklı kolaylıklar da sağlıyor, ancak genel mantığı anlayabilmek açısından bunu da söylemek istedim.
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle servislerin dinamik bir şekilde kaydedilip ihtiyaç halinde bunların istendiğinde dinamik ve merkezi yapılar kurmak projelerdeki esnekliği ve tek elden yönetimi sağlayarak elimizi oldukça güçlendiriyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerim ve hadis-i şerif ile bitirelim.

> "Her şeyin hazineleri yalnızca bizim yanımızdadır. Biz, onu ancak belli bir ölçüye göre indiririz." (Hicr Suresi, 21)

> "Allah, işinde maharet sahibi olan kulunu sever." (Beyhakî, Şuabü’l-İman, 4/334)

### 16. Monitoring
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mikroservis serimizin son bölümü olan on altıncı yazımıza geldik. Bugünkü konumuz monitoring. Bir problem ile karşılaştığımızda, hatta bazen karşılaşmadan bizi yönlendirecek/uyaracak sistemlerin olması çok önemlidir. Canlı çalışan sistemlerin 7/24 ayakta olması gereken durumlarda bu konu daha da öne çıkmakta ve uykusuz gecelerin sayısını oldukça azaltmaktadır diye düşünüyorum :) Hazırsak başlayalım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Monitoring her sistemde önemli olacak bir konudur. Sistemin sağlıklı bir şekilde ayakta olması en temel konu olsa gerek. Monolit sistemlerde bunu tespit etmek elbette çok daha kolaydır. Tek bir proje, muhtemelen tek bir veritabanı vardır. Bunun da tabii ki bazı metriklerinin takip edilmesi gerekiyor olsa da buradaki parametreler daha az olduğundan takibi de doğal olarak daha kolaydır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mikroservis sistemlerde onlarca yüzlerce servis ve birçoğunun da kendine has veri tabanları var. Bununla birlikte kuyruk yapıları, cache'leme ve daha birçok araç ve bunların birden çok instance'leri gibi konuları ekleyince konu tahmin ettiğimizden çok daha karmaşık hale gelebiliyor. Doğal olarak bunların takip edilmesi de bir o kadar zor oluyor. Bu yüzden bu işi, birçok yazıda bahsettiğimiz üzere,  merkezileştirme ve otomatize etme üzerine adımlar atmalıyız.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Monitoring'in neden gerekli olduğunu anlatmaya çalıştık. Biraz da öneminden bahsedelim.
- Sistemin her daim ayakta olup olmadığını bilmemizi sağlar.
- Hata tespiti ve çözümü konusunda bize yarar sağlar.
- Tüm sistemi tek bir elden yönetilmesini sağlar.
- Gecikme, dar boğaz gibi konuların tespitini sağlar.
- Olası problemleri görüp önceden çözümler üretilmesini sağlar.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Monitoring ile birden çok metrik takip edilebilir. Bunlardan bazıları; istek süreleri, hata oranları, CPU ve bellek kullanımı, trafik yoğunluğu, gecikmeler, hata loglarıdır. Bunlar temel metrik olsa da her sistemin kendine göre ihtiyaçları oluyor. Sizin sistemler için gerekli metrikleri de listeye eklemeniz faydalı olacaktır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Neredeyse her merkezi yapıda olduğu gibi burada da birbirinden değerli araçlar var. Bunlardan en çok duyulanlardan bazıları; Prometheus + Grafana ikilisi, ELK (önceki yazımızda konuşmuştuk), OpenTelemetry (Jeager + Zipkin), New Relic ve bulut tabanlı sistemlerin kendi araçları bunlara örnek olarak verilebilir. Her birinin kendine göre kullanım alanı ve avantajları var. Biz şu an New Relic (ücretli versiyon) kullanıyoruz, servisler arası çağrılarda servislerin nereden geçtiği, nerelerde tıkandığı bilgisi bizim için çok önemli. Özellikle de legacy olan bazı sistemlerimiz için tespiti açısından bize çok faydası dokunuyor. Bununla birlikte OpenTelemetry kullandığımız yerler de mevcut.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tüm bu metrikler belirli araçlarla toplanır dedik, ancak bunları anlamlı/kullanılabilir hale getirmek de lazım. Bunun için de alarmlar kuruyoruz. Örneğin son 1 saat içerisinde 1000'den fazla OTP sms atıldıysa burada bir atak yiyor olabiliriz veya kuyrukta 500'den fazla bekleyen IoT komutu varsa orada bir sorun var gibi alarmlar kurulabilir. Bu alarmları yine belirli yöntemlerle yollayabiliriz. Slack, SMS, e-posta bu seçeneklerden bazılarıdır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bazen yanıltıcı uyarılar da oluşabiliyor. Burada metrikleri de zamanla optimize etmekte fayda var. Ya da beklemediğiniz bir ortamda yüzlerce ya da binlerce aynı hata geldiğinde onu sessize alıp problemi çözdükten sonra açmak da uygulanabilir yöntemlerden. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tüm bu metrikler, alarm kurmak gayet güzel. Ancak belirli dönemlerde farklı ekiplerin görmek istedikleri metrikleri görsel veriye çevirmek de gerekiyor. Örneğin yazılım ekibinin takip ettiği farklı ekranlar var iken, devops ekibi başka metrikleri takip ediyor olabilir. Bu yüzden işleri kolaylaştırmak için farklı dokunuşlar yapmak gerekir. Bizler de özelleştirdiğimiz metriklerle tüm ekibin görüntüleyebileceği arayüzler oluşturduk. Bunları zaman zaman kendimiz de kontrol ediyoruz.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle metrik toplama, bunları anlamlandırıp alarmlar kurma ve daha sonra da görüntüleyebileceğimiz arayüzler kullanmak olursa daha iyi olur diyebileceğimiz işler olmaktan çıkıp çoktan zorunluluk haline gelmiştir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hem yazımızın hem de yazı serimizin sonuna gelmiş bulunmaktayız. Bu işe başladığımda gözümde büyüyen acaba yapabilir miyim, bitirebilir miyim dediğim ve uzun süredir bekleyen bu notlarımı bu şekilde ele alabildiğim için Yüce Allah'a şükürler, siz okuyan değerli arkadaşlara ise teşekkürlerimi borç bilirim. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü ve seriyi birer ayet-i kerim ve hadis-i şerif ile bitirelim.

> "İnsan ancak çalıştığının karşılığını görür." (Necm Suresi, 53:39)

> "Emanet zayi edildiğinde kıyameti bekle." Sahabe sordu: 'Emanet nasıl zayi olur?' Peygamberimiz (sav) buyurdu: 'İş, ehline verilmediğinde kıyameti bekle.'" (Buhari, İlim 2)
