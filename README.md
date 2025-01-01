# Selamün Aleyküm Arkadaşlar,

![Free Palestine](Images/free-palestine.jpg)


Bu seride toplamda 16 yazı bulunmaktadır (giriş yazısı hariç). Geri dönüşleriniz ve PR'larınızı bekliyorum!

## Blog Serisi Konuları:

- Bounded Context
- Async Messaging
- Composing Microservice
- Achieving Data Consistency
- Centralizing Access
- Separated DBs
- Arch Api-based
- Resiliency
- Backward Compatibility
- Documenting Contracts 
- Centralized Logging
- Cloud-Based Infrastructure
- Deployment Automation
- Configuration Management
- Service Registry & Discovery
- Monitoring



**Giriş: Index[0]**

Çok uzun süredir notlarımda olan ve hep yazmak istediğim bir seriye Allah’ın izniyle başlıyorum. Yıllar önce izlemiş olduğum [bu videoda](https://www.youtube.com/watch?v=a3ehu_Yv96U&t=2671s&ab_channel=MustafaVarank) not aldığım 16 başlığı 16 ayrı yazı olarak ele alıyorum. Sadece başlıkları buradan almış olup içeriği özgün olarak oluşturmaya gayret ettim. Böyle düşününce gerçekten zor bir hedef gibi görünüyor, ancak birincisine niyet edip başlarsak inşaAllah gerisi de gelir diye düşünüyorum..

Bu yazı girizgah yazısı olacak. Hangi konuları ele alacağımızı belirtip özet mahiyetinde birkaç cümle ile kısa kısa açıklamalar yapacağız. Daha sonra yeni yazıları yazdıkça buradaki linkleri de güncelliyor oluruz inşaAllah. Bazı konular hakkında daha çok bilgi sahibiyken bazı konularda benim de daha fazla okumalar yapmam lazım. Bu yolculuğa bir "assignment" [projesi](https://github.com/malikmasis/TelephoneDirectory) ile başlayıp onu belirli aralıklarla geliştirmeye devam ettim. Bunu daha önce bu [yazımda](https://medium.com/software-development-turkey/mikroservis-maceram-1e070463d0ea) dile getirmiştim. Devam eden süreçte de ayrıca bir yazı yazmadım. Hep bu yazıyı güncelleyerek veya Github projesini geliştirerek devam ettim, ancak bu sefer önüme zorlu da olsa bir hedef koymak istedim. Rabbim utandırmasın.

Mikroservis nedir, ne değildir gibi sorulara girmeyi pek düşünmüyorum açıkçası. Bu yazı serisi biraz daha bu işi bilen ya da en azından merak eden kesime yönelik olacak. Her ne kadar son projemde çok etkin bir şekilde bu yapıları kullansam da konuların derli toplu olması açısından veya projeye dalıp kaçırdığımız noktalar var ise öncelikle kendimi de geliştirmek açısından ele alıyorum. Hata, eksik veya fazla olduğunu düşündüğünüz yerler olursa elbette desteklerinize açık olduğumu da belirtmeden geçemeyeceğim.

Mikroservis konusu ile ilgili kendi adıma diyebileceğim en net şey, gerçekten ihtiyaç olduğuna ikna iseniz ve buna da uygun takım ya da takımlarınız var ise bu işe girmenizi naçizane öneriririm. Aksi halde siz ve ekibiniz için çok zorlu bir dönem başlayabilir. Nedenlerini önümüzdeki yazılarda zaman zaman değiniyor oluruz. Ufaktan başlayalım.

---

1. **[Bounded Context](#1bounded-context)**: Domain Driven Design ile bağlamı net bir şekilde ortaya koymak gerekir. Bağlam düzgün kurgulandığında birçok şey daha kolay oluyor. Fazla veya eksik olduğunda ise buradaki hatalarınızı gidermek için fazlaca yıpranabilirsiniz. Şahsi fikrim burası işin kalbi...

2. **Async Messaging**: Asenkron iletişim mikroservis sisteminin olmazsa olmazıdır. Hem servisler arası iletişimde hem de uzun süren işlemlerde ilaç gibi gelir.

3. **Composing Microservice**: Gelen isteğin cevabını birçok servisten toplayarak farklı kanallar üzerinden toplayarak bunu cevap olarak döner. Bu konunun hızlıca anti-pattern'a dönme ihtimali var. Bunun için de bazı çözümler öneriliyor.

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

### 1.Bounded Context

Özette de belirttiğimiz gibi bu işin kalbi bana göre sınırları doğru çizebilmek. Sınırları doğru ve net belirlediğimizde geriye kalan işler kolaylaşacaktır. Monolit yapılarda veritabanı tasarımının projedeki en önemli kısım olduğunu düşündüm hep. İyi bir veri tabanı iyi bir backend yazılımına, o da iyi bir arayüze ve günün sonunda iyi bir uygulama vesile olur. Mikroservis mimarisinde ise aynı şeyi "bounded context" için düşünüyorum. Hazırsak başlayalım.

Konuya bir anı ve ardından gelen bir soru ile girmekte fayda olabilir. Girdiğim bir mülakatta konu DDD'ye gelmişti. Ben de projemi bu yaklaşıma uygun geliştirdiğimi söylemiştim. Buna karşılık mülakatı yapan kişi bana peki DDD sadece yazılımcı için olan bir konu mu demişti?

Dürüst olmak gerekirse öyle bir soruyu hiç beklemiyordum. Daha önce de yaptığım bazı okumalarla birlikte yazılımcı bunun önemli bir parçası ama her şeyi değil demiştim. Gerçekten de bu ekipçe aynı dili, terminolojiyi kullanmaktan geçer. Ekip dediğim sadece yazılımcılardan bahsetmiyorum. Bunlarla birlikte ürüncü, testçi, analist ve artık daha kimler varsa. Özetle bu işin altına elini sokmuş tüm arkadaşlar diyebiliriz.

Genel manada her bir bağlam (bounded context) bir mikroservisi teslim eder, edebilir. Muhtemelen çokça karşılaşmışsınızdır. Order, Payment, Product gibi servis isimleri geçer. Mikroservis teknolojisinin öncülüğünü bizim ülkede e-ticaret siteleri yaptığı için (ya da onlar daha önce çıkardığı için de olabilir) genelde örnekler de hep buradan geliyor. Farklı domainlerde çalışıyorsanız oturup biraz daha düşünmeniz veya kendi yoğurt yiyişinize göre sistemi tasarlamanız gerekebilir.

Şu an ben mobilite sektöründe çalışıyorum. Bu yüzden bizim kapsamlar baya farklı. Bağlamları belirlerken Rental (kiralama süreci), Vehicle (araç ve iot), Branch (bölge yönetimi) diye bizim birbirinin içine giren ama aslında farklı olabilecek 3 domainimiz vardı (diğerlerini net bir şekilde belirledik). Bunları ayrı birer bağlam mı yoksa hepsini tek bağlam altında toplama konusunda kararsızlık yaşadık. Benim şahsi fikrim bunları ayırmanın daha doğru olacağı yönündeydi, ancak bunları birlikte ele alarak devam ettik.

Geliştirmeler tüm hızla devam ediyor. 10 kişilik yazılım ekibi aynı projede geliştirmelerini sürdüyor (aslında 3 takım, her takımın, ayrıca yazılımcı olmayan üyeleri de var tabii ki). Zamanla kapsamlar birbirine yaklaştıkça toplantılar yaparak problemleri gidererek yolumuza hızlı bir şekilde devam ettik. Kapsamları birleştirmeye ilk başta çok sıcak bakmasam da zamanla tabii ki sıkıntılar çıksa da bunun çok daha iyi olduğunu anladım. En azından bizim için iyi olduğunu anladım.

Ayağı yere daha iyi basan veya daha oturmuş ekiplerle, daha uzun vadeli bir geliştirme yapılıyor olsa belki hala bu bağlamları ayrı ayrı ele almak iyi olacaktı. Ancak alınan kararlar göre değişkenlik gösterebiliyor. Teknik olarak doğrusu yanlışından ziyade bu işin size neler getirip sizden neler götüreceğini iyi tespit etmek lazım. Yoksa öteki türlü her çözüm her yere uygulanabilir olsaydı bu sektör belki de buralara gelmeyecekti...

Başka bir projede de yaşadığım başka bir tecrübeden bahsetmek istiyorum. Bu işe sonradan dahil olduğum için, yapılan işi ve hangi sıkıntılarla karşılaştığımızdan bahsedeceğim. Yaklaşık 13-15 mikroservisli bir var ve bazıları mikroservis değil [nanoservis](https://nanoservices.io/docs/docs/concepts/nanoservice/) seviyesine gelmiş. Tablolar birbiriyle direkt ilişkili. A servisinden veriyi B servisine senkron olarak çekip oradan gelen veriye göre iş yapılıyor. Bu 1-2 defa yapılan bir iş değil bütün kurgu maalesef bu şekilde. Yani her ayrı olan kavramı ayrı birer mikroservis olarak ele almışlar, ancak orada "over engineering" oluşmuş ve günün sonunda ekipçe oturup bu servislerin bazılarını birleştirelim diye karar aldık.

2 ayrı örnekte de belirttiğim gibi, bu işin doğrusu yanlışından ziyade uygulanabilirliği önemli diye düşünüyorum. Her şeyi servislere bölmek de yanlış bir seçim, bütün her şeyi de tek bir servis altında toplamak zaten ayrı bir yanlış seçim olabilir. Bu işin dengesini ve kararını iyi verebilmek lazım. Orada düşünüp vereceğimiz bir karar inanın bütün projenin geliştirme sürecini çok derinden etkileyecektir. O yüzden kervan yolda düzülür gibi kararlardan naçizane sıyrılmanızı tavsiye ederim. Projeyi canlıya bile almadan her yeri yamalanmış bir proje ile karşı karşıya kalabilirsiniz veya daha kötü canlıya bile çıkmadan yolun sonuna gelmiş olabilirsiniz...

Özetle projenin isterlerini ve gereksinimlerini iyi analiz ederek kapsamları doğru bir şekilde ortaya koymak projenin en kritik noktası olabilir. Bu yüzden başlangıç noktasında çok acele etmeden çok da "over engineering" yapmadan size uyacak en doğru kararı vermeniz duasıyla.

Bu bölümü birer ayet-i kerim ve hadis-i şerif ile bitirelim.

> "Biz her şeyi bir ölçüye göre yarattık." (Kamer, 54/49)

> "Muhakkak ki Allah, her işte ihsanı (en iyi şekilde yapmayı) emretmiştir." (Müslim, Sayd, 57; Ebû Davud, Edahi, 11)

