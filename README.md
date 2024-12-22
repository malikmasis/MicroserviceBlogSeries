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

Çok uzun süredir notlarımda olan ve hep yazmak istediğim bir seriye Allah'ın izniyle başlıyorum. Yıllar önce yanlış hatırlamıyorsam Koç sistemin bir videosunda not aldığım 16 başlığı 16 ayrı yazı olarak ele alıyorum. Böyle düşününce gerçekten zor bir hedef gibi görünüyor, ancak birincisine niyet edip başlarsak inşaAllah gerisi de gelir diye düşünüyorum.

Bu yazı girizgah yazısı olacak. Hangi konuları ele alacağımızı belirtip özet mahiyetinde birkaç cümle ile kısa kısa açıklamalar yapacağız. Daha sonra yeni yazıları yazdıkça buradaki linkleri de güncelliyor oluruz inşaAllah. Bazı konular hakkında daha çok bilgi sahibi iken bazı konularda benim de daha fazla okumalar yapmam lazım. Bu yolculuğa bir "assignment" [projesi](https://github.com/malikmasis/TelephoneDirectory) ile başlayıp onu belirli aralıklarla geliştirmeye devam ettim. Bunu zaten daha önce bu [yazımda](https://medium.com/software-development-turkey/mikroservis-maceram-1e070463d0ea) dile getirmiştim. Devam eden süreçte de ayrıca bir yazı yazmadım. Hep bu yazıyı güncelleyerek veya Github projesini geliştirerek devam ettim, ancak bu sefer önüme zorlu da olsa bir hedef koymak istedim. Rabbim utandırmasın.

Mikroservis nedir, ne değildir gibi sorulara girmeyi pek düşünmüyorum açıkçası. Bu yazı serisi biraz daha bu işi bilen ya da en azından merak eden kesime yönelik olacak. Her ne kadar son projemde çok etkin bir şekilde bu yapıları kullansam da konuların derli toplu olması açısından veya projeye dalıp kaçırdığımız noktalar var ise öncelikle kendimi de geliştirmek açısından ele alıyorum. Hata eksik veya fazla olduğunu düşündüğünüz yerler olursa elbette desteklerinize açık olduğumu da belirtmeden geçemeyeceğim.

Mikroservis konusu ile ilgili kendi adıma diyebileceğim en net şey, gerçekten ihtiyaç olduğuna ikna iseniz ve buna da uygun takım ya da takımlarınız var ise bu işe girmenizi naçizane öneriririm. Aksi halde siz ve ekibiniz için çok zorlu bir dönem başlayabilir. Nedenlerini önümüzdeki yazılarda zaman zaman değiniyor oluruz. Ufaktan başlayalım.

---

1. **Bounded Context**: Domain Driven Design ile bağlamı net bir şekilde ortaya koymak gerekir. Bağlam düzgün kurgulandığında birçok şey daha kolay oluyor. Fazla veya eksik olduğunda ise buradaki hatalarınızı gidermek için fazlaca yıpranabilirsiniz. Şahsi fikrim burası işin kalbi...

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

Yukarıdaki 16 konuya ufak ufak bazı notlar yazmaya çalıştık. Önümüzdeki yazıları da her bir konuyu ayrı ayrı olarak ele almayı düşünüyoruz. Niyet bizden, takdir ve başarı Allah'tandır.

Ben bu yazıyı taslak olarak yazarken şu an hala Gazze'deki insanlar açlıktan ölüyor. Rabbim buradaki kardeşlerimize de büyük bir zafer ihsan eylesin. Dualarımı ve bu yazı serisini, niyetleri Allah'ın rızasını kazanmak olan bu koca yürekli insanlara ithaf ediyorum.

**“Ve de ki: ‘Bütün başarı ve zafer, sadece Allah’tandır.’” (Al-i İmran, 3:126)**

