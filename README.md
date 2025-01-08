# Selamün Aleyküm Arkadaşlar,

![Free Palestine](Images/free-palestine.jpg)


Bu seride toplamda 16 yazı bulunmaktadır (giriş yazısı hariç). Yazılarda eksik fazla olduğunu düşündüğünüz noktalar için geri dönüşleriniz ve PR'larınızı bekliyoruz!


**Giriş: Index[0]**

Çok uzun süredir notlarımda olan ve hep yazmak istediğim bir seriye Allah’ın izniyle başlıyorum. Yıllar önce izlemiş olduğum [bu videoda](https://www.youtube.com/watch?v=a3ehu_Yv96U&t=2671s&ab_channel=MustafaVarank) not aldığım 16 başlığı 16 ayrı yazı olarak ele alıyorum. Sadece başlıkları buradan almış olup içeriği özgün olarak oluşturmaya gayret ettim. Böyle düşününce gerçekten zor bir hedef gibi görünüyor, ancak birincisine niyet edip başlarsak inşaAllah gerisi de gelir diye düşünüyorum..

Bu yazı girizgah yazısı olacak. Hangi konuları ele alacağımızı belirtip özet mahiyetinde birkaç cümle ile kısa kısa açıklamalar yapacağız. Daha sonra yeni yazıları yazdıkça buradaki linkleri de güncelliyor oluruz inşaAllah. Bazı konular hakkında daha çok bilgi sahibiyken bazı konularda benim de daha fazla okumalar yapmam lazım. Bu yolculuğa bir "assignment" [projesi](https://github.com/malikmasis/TelephoneDirectory) ile başlayıp onu belirli aralıklarla geliştirmeye devam ettim. Bunu daha önce bu [yazımda](https://medium.com/software-development-turkey/mikroservis-maceram-1e070463d0ea) dile getirmiştim. Devam eden süreçte de ayrıca bir yazı yazmadım. Hep bu yazıyı güncelleyerek veya Github projesini geliştirerek devam ettim, ancak bu sefer önüme zorlu da olsa bir hedef koymak istedim. Rabbim utandırmasın.

Mikroservis nedir, ne değildir gibi sorulara girmeyi pek düşünmüyorum açıkçası. Bu yazı serisi biraz daha bu işi bilen ya da en azından merak eden kesime yönelik olacak. Her ne kadar son projemde çok etkin bir şekilde bu yapıları kullansam da konuların derli toplu olması açısından veya projeye dalıp kaçırdığımız noktalar var ise öncelikle kendimi de geliştirmek açısından ele alıyorum. Hata, eksik veya fazla olduğunu düşündüğünüz yerler olursa elbette desteklerinize açık olduğumu da belirtmeden geçemeyeceğim.

Mikroservis konusu ile ilgili kendi adıma diyebileceğim en net şey, gerçekten ihtiyaç olduğuna ikna iseniz ve buna da uygun takım ya da takımlarınız var ise bu işe girmenizi naçizane öneriririm. Aksi halde siz ve ekibiniz için çok zorlu bir dönem başlayabilir. Nedenlerini önümüzdeki yazılarda zaman zaman değiniyor oluruz. Ufaktan başlayalım.

---

1. **[Bounded Context](#1-bounded-context)**: Domain Driven Design ile bağlamı net bir şekilde ortaya koymak gerekir. Bağlam düzgün kurgulandığında birçok şey daha kolay oluyor. Fazla veya eksik olduğunda ise buradaki hatalarınızı gidermek için fazlaca yıpranabilirsiniz. Şahsi fikrim burası işin kalbi...

2. **[Async Messaging](#2-async-messaging)**: Asenkron iletişim mikroservis sisteminin olmazsa olmazıdır. Hem servisler arası iletişimde hem de uzun süren işlemlerde ilaç gibi gelir.

3. **[Composing Microservice](#3-composing-microservice)**: Gelen isteğin cevabını birçok servisten toplayarak farklı kanallar üzerinden toplayarak bunu cevap olarak döner. Bu konunun hızlıca anti-pattern'a dönme ihtimali var. Bunun için de bazı çözümler öneriliyor.

4. **Achieving Data Consistency**: Mikroservis konusunun şahsımca en zor konusu bu olabilir. Veri tutarlığını sağlamak için bir sürü pattern olsa da bunu tam anlamıyla mükemmel uygulamak gerçekten kolay bir şey değil. Burası ne kadar sorunlu olursa o derece operasyon maliyeti artıyor.

5. **Centralizing Access**: Dışarıdan gelen tüm isteklerin nerelere nasıl yönlendirileceğini ele alır. Birbirine benzeyen ve çok karıştırılan 3 yapıya da değineceğiz. Özetle kalenin giriş kapıları olarak düşünebiliriz.

6. **Separated DBs**: En sık düşülen hatalardan veya monolit yapılardaki geçişlerde en zorlanılan konulardan biridir. Her bir servisin ayrı bir veritabanı olmalıdır. Aksi halde veri tabanındaki herhangi bir hatada bütün sistem de çökmüş olacaktır.

7. **Arch Api-based**: Api tabanlı iletişimi ele alır. Bunu sağlamanın birden çok yolu var. Her birinin de kendine göre avantaj ve dezavantajları var.

8. **Resiliency**: Bir servise yapılan çağrıların belirli bir sebepten dolayı cevap vermemesi sonucu orada bağlantıyı keserek bütün sisteme yük binmesine engel olur. Belirli dönemlerde buradaki problem düzelip düzelmediğini kontrol eder, düzelmiş ise tekrar bağlantıya izin verir.

9. **Backward Compatibility**: Eskiye yönelik servislerin çalışırlığını ele alır. Bunun için versiyonlama kullanılan genel çözümlerden biridir. Aksi halde yaptığınız radikal bir değişiklik (breaking change) burayı kullanan eski istemcileri olumsuz etkileyecektir.

10. **Documenting Contracts**: İstemci ve sunucu arasında bir protokol, anlaşma diyebiliriz. Interface'ler ile yazılımda nasıl bazı konular için el sıkışıyorsak bunu da öyle anlayabiliriz desek yanlış ifade etmiş olmayız herhalde. Open Api gibi standartlarla bunları ele alabiliriz.

11. **Centralized Logging**: İlk başta çok önemsenmese de servisler arttıkça hatalar oldukça loglamanın önemini çok daha iyi anlıyorsunuz. Özellikle debug yapmanın zor olduğu böyle bir ortamda bu çok daha kıymetli olmaktadır.

12. **Cloud Based Infrastructure**: Bu başlık itibariyle biraz daha devops tarafına girişmeye başlıyoruz. Fiziksel sunucular yerine buluttaki hizmetleri ele almayı önerir. Birçok güzelliği olsa da elinizi verdiğinizde kolunuzu kaptırma ihtimaliniz de var :)

13. **Deployment Automation**: Bu işe girişmeyi düşünüyorsanız manuel deployment'i hayatınızdan çıkarmış olmanız gerekiyor. Servisleriniz her birinin otomatik olarak sunuculara gitmesi gerekmektedir. Hatta gün içinde istediğiniz anda bu işi de yapabiliyor olmalısınız.

14. **Configuration Management**: Dev test prod gibi farklı ortamlarınızın olması gerekir. Bu aslında monolit yapılarda da olan bir konu ancak bazen gün içinde birden fazla deployment hedeflenen sistemlerde olmazsa olmaz durumuna dönüşüyor.

15. **Service Registry & Discovery**: Servislerin birbiriyle iletişim kurduğu durumları ele alır. Özellikle dinamik olarak ölçeklenme, dağıtılma gibi konularda daha da önemi artmaktadır. Yine birçok konudaki gibi bunu da yapan bazı araçlar mevcut.

16. **Monitoring**: Birden fazla servisiniz varsa bunları yönetmek de doğal olarak zorlaşabiliyor. Bunlardan herhangi birinde bir problem olduğunda kullanıcıdan önce sizin haberiniz olmalı. Hem durumları takip edebileceğimiz hem de bize alarm durumlarını önceden haber etmeye olanak sağlar.

---

**Sonuç:**

Yukarıdaki 16 konuya ufak ufak bazı notlar yazmaya çalıştık. Yazının devamında her bir konuyu ayrı ayrı olarak ele almayı düşünüyoruz. Niyet bizden, takdir ve başarı Allah'tandır.

Ben bu yazıyı taslak olarak yazarken şu an hala Gazze'deki insanlar açlıktan ölüyor. Rabbim buradaki kardeşlerimize de büyük bir zafer ihsan eylesin. Dualarımı ve bu yazı serisini, niyetleri Allah'ın rızasını kazanmak olan bu koca yürekli insanlara ithaf ediyorum.

**“Ve de ki: ‘Bütün başarı ve zafer, sadece Allah’tandır.’” (Al-i İmran, 3:126)**

### 1. Bounded Context

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özette de belirttiğimiz gibi bu işin kalbi bana göre sınırları doğru çizebilmek. Sınırları doğru ve net belirlediğimizde geriye kalan işler kolaylaşacaktır. Monolit yapılarda veritabanı tasarımının projedeki en önemli kısım olduğunu düşündüm hep. İyi bir veri tabanı iyi bir backend yazılımına, o da iyi bir arayüze ve günün sonunda iyi bir uygulama vesile olur. Mikroservis mimarisinde ise aynı şeyi "bounded context" için düşünüyorum. Hazırsak başlayalım.

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
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin ikinci bölümünde asenkron iletişimi ele alacağız. Servisler arası iletişimde temelde iki yöntem var. Bu yöntemlerden biri senkron (rest api, grpc) ve diğeri asenkron olarak ele alabiliriz. Birbirilerine göre avantaj ve dezavantajları olsa da servislerin birbirine olan bağımlılıkları en aza indirgemek için asenkron iletişim bu işin temel parçalarından biri haline geliyor. Hazırsak başlayalım.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bir mikroservis sistemi tasarımında mümkün mertebe servisleri birbirinden izole olmasını isteriz. Bunun sebeplerinden bir tanesi o servisle ilgili herhangi bir olumsuzlukta sistemin ayakta kalmaya devam etmesidir. Örneğin, kampanyalar servisiniz düştü ancak kullanıcı hala alış-verişini yapmaya devam edebilmeli. Kampanya servisi düştüğü için bütün sistemin çalışılmaz hale gelmesine gerek yoktur.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Servislerin birbirine gevşek bağımlı hale gelmesini peki nasıl sağlarız? Bunun çözümlerinden biri, iletişimin asenkron olmasıdır. Senkron olan iletişimde servislerinden biri çöktüğünde diğer servis oradan gelecek cevabı bekleyecektir ve bu da sistemde bir gecikmeye sebep olacaktır (tabii ki bunun da çözümleri mevcut. Circuit breaker, timeout, fallback vb), ancak iletişim asenkron olduğunda bu problemler oldukça azalır (tabii ki farklı problem çıkabilir :) ).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peki her servis çağrısında asenkron iletişim mi kullanmalıyız? Bunun için mümkün olduğunca sistemi esnek tutabilmek açısından evet ama bazen diğer servislerden gelen cevabı beklememiz gerekiyorsa o zaman senkron iletişim kaçınılmaz hale geliyor. Ancak bazen de verilerin her iki servisin veri tabanında da tutulması konusu gündeme gelebilir. CDC (Change Data Capture) konusuna önümüzdeki yazılarda değiniyor olacağız.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asenkron mesajlaşmanın daha da önemli hale geldiği konulardan bazıları; uzayan veya hemen işlenmesi çok kritik olmayan konular. Eposta, sms veya bildirim atmak, log işlemleri bunlara örnek olarak gösterilebilir. Bu tarz işlemler için bu konu daha da önemli hale gelebilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asenkron mesajlaşmada kullanılan birçok araç var. Bu araçlardan en göze çarpanları rabbitmq, kafka veya bulut çözümlerin kendi ürünleri de mevcut (amazon sqs, azure service bus). Bu araçların birbirlerine göre fiyat, performans gibi birçok artı ve eksi yönleri var. Dotnet dünyasında özellikle Rabbitmq'nin çok kullanıldığına şahit oluyorum ve onu implemente eden açık kaynaklı proje olan MassTransit ile birlikte kullanımı daha da kolay hale gelebiliyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Asenkron mesajlaşmayı çok övdük de hiç mi eksik yanı yok derseniz, tabii ki her hastalığa aynı ilacı vermek söz konusu olamaz. Yukarıda da bahsettiğimiz gibi cevap bekleyen durumlarda veya basit sistem tasarımlarında bunu kullanmak sistemi daha karmaşık hale getirecektir. Öğrenmesi, yönetmesi ve takip etmesi gibi bazı zorlukları getirir. Verilerin doğru bir şekilde işlenmesi, iletilmesi, bazı durumlarda çoklanması gibi farklı zorluklar ortaya çıkmaktadır (veri tutarlığı konusuna ileride değiniyor olacağız). İlk başlarda bu zorlukları aşmak da çok kolay olmuyor.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle, asenkron mesajlaşma mikroservis mimarisinde bir zorunluk olmasa da önemli yapı taşlarından biridir. Genel sistem içerisinde tabii ki senkron ve asenkron iletişimin birlikte kurgulanabilir, hatta kurgulanmalı. Nereden hangisini kullanılacağını tespit edip ona göre işlemleri devam ettirmek en doğrusu olacaktır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bölümü birer ayet-i kerim ve hadis-i şerif ile bitirelim.

> "Ve yardım edin birbirinize takvada ve takvaya davette, günah ve düşmanlıkta ise yardım etmeyin." (Mâide, 5:2)

> "Dil bir kılıç gibidir, onunla ya kurtulursun ya da helak olursun." (İbn Mâce, Zühd, 19)

 ### 3. Composing Microservice

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Serinin üçüncü bölümünde "composing microservice" konusunu ele alacağız. Birden çok servisten gelen cevapları toplayarak yanıt olarak istemciye (client) geri döner. Mikroservisin bağımsızlık ilkesine ters olsa da iş modelinin isterlerine göre kaçınılmaz olabiliyor. Bu durum, genel tasarıma zarar verebileceğinden burayı tasarlamak ilerideki birbirine bağımlı servislerin oluşmasına engel olmak açısından çok önemlidir. Hazırsak detaylarına inelim.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Genel itibariyle çok fazla servisimiz olduğunu varsayalım. Her birinin yaptığı işler belli, ancak gerçek hayattaki isterler tahmin edebileceğiniz üzere çok karmaşıklaşabiliyor. Bazen birden çok servisten bilgiyi toplayarak bir yanıt dönmemiz gerekiyor. Böyle durumlarda başvuracağımız yöntemlerden biri de bu servislerden gelen cevapları alarak toplu bir yanıt dönmek olacaktır. Bunun bazı yöntemleri var:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Api üzerinden bu verileri toplayarak gerekli cevaplar dönebiliriz, bununla birlikte Orchestration dediğimiz merkezi bir yapı ile bunu yapabiliriz. Servisleri sırasıyla çağırıp cevapları birleştirerek iletir. Choreography denilen diğer bir yapı ise merkezi bir yapı olmadan servislerin kendi arasında haberleşerek bu işi yapmasıdır. Servis sayısı veya karmaşıklık az ise bu yöntem daha uygun olabilir.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu yöntemlerin hepsi genel itibariyle aynı probleme çözüm araralar ama beraberinde de bazı zorluk ve sıkıntılara sebebiyet verebilirler. Veri tutarsızlığı (sonraki konumuz), performans problemleri, hataların yönetimi gibi zorlukları da beraberinde getirir. Bunlara önlem olarak tabii ki çözümler üretmek mümkün. Ancak bu problemlere bulaşmadan bu işleri çözebilir miyiz sorusu da insanın aklına gelmiyor değil.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bunlara alternatif bazı yöntemler elbette var ancak her birinin de kendisiyle birlikte getirdiği zorluklar oluyor. CQRS, GraphQL, veri çoklama(duplicate) ve bağlamların doğru bir şekilde tasarlanması örnek verilebilir. Dediğimiz gibi her birinin de beraberinde getirdiği zorluklar olsa da burada problemi doğru tespit edip bizlere hangi çözümün daha uygun olduğunu ortaya koymak işin teknik zorluğu diye düşünüyorum.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu arada bu çözümlerin birini kullandık diye diğerlerinden vazgeçmek zorundayız anlamına gelmez. Bunların birlikte kullanılması da mümkün. Örneğin bir servisten diğerine çağrıda bulunuyorsunuz ve sadece bir veriyi almanız gerekir, böyle bir durumda veri çoklama (Data Repliction) çözüm olabilir, ancak gittiğiniz servisten birçok önemli veriyi almanız gerekiyordur ve bütün bu verileri kendi tarafınıza taşımak doğru değil ise o zaman da isteği yapıp gelen veri kullanabilirsiniz. Bazen de  birçok servisten cevap almanız gerekiyordur o zaman da bunu gateway seviyesinde yapabilirsiniz. Dediğimiz gibi her birinin artı ve eksi yönleri olsa da bunun doğru veya yanlış bir cevabından ziyade size uygun olan cevabı önemli olur.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Özetle iş ihtiyaçlarına göre bazı konularda farklı çözümler bulmamız gerekebilir. Çözümleri uygularken artı ve eksilerini iyi düşünüp kendi yapımıza uyarlarken, bunların eksi olan yöntemlerini nasıl sıfıra indirgeyebiliriz diye düşünüp o çözümleri de uygulamak genel manada güzel olur diye düşünüyorum.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yazıyı bir ayet-i kerime ve her probleme ayrı bir çözüm sunan Peygamber Efendimiz(s.a.v.) ile ilgili olan bir hadis yorumu ile bitirmek istiyorum.

> "Rabbinin yoluna hikmetle ve güzel öğütle çağır ve onlarla en güzel şekilde mücadele et. Şüphesiz ki Rabbin, yolundan sapanları da en iyi bilendir; hidayete erenleri de en iyi bilendir." (Nahl, 16/125)

> “Ey Allah’ın Resûlü! Hangi amel daha faziletlidir?” diye sorduğunda, farklı sahabilere farklı cevaplar verdiği görülür. 
- Örneğin: Biri için “Namazı vaktinde kılmak” 
- Bir başkası için “Ana babaya iyilik etmek” 
- Bir diğeri için ise “Allah yolunda cihad etmek” cevabını vermiştir. 
> Bu hadis, insanların durumlarına, ihtiyaçlarına ve önceliklerine göre çözüm sunmanın İslam’da önemli bir ilke olduğunu gösterir. (Buhârî, Edeb 1; Müslim, İman 137)


