#   Sanal Makinelere Dayalı İş Akışı

.fx: first

Aydın Doyak `<aydintd@bil.omu.edu.tr>`

http://aydintd.me/

Bitirme Projesi Sunumu	

Haziran 2014
 
---

##   Projenin Çıkış Noktası

Günümüzde hem yazılım geliştirme hem de sistem yönetiminde sanal makineler her yerde kullanılmakta

-   Geliştiriciler için test veya geliştirme ortamları olarak

-   Sistem yöneticileriyse hizmetini verdikleri ürün servisleri sunuculardaki sanal makinelerde konuşlandırmakta

Ancak bu süreç çoğunlukla **kendini tekrar** içeren, standart bir iş akışına tabi olmayan, çoğu zaman ağrılı bir süreç

Ayrıca günümüzde bir çok yeni sanallaştırma teknolojisi ve sanallaştırmaya dayalı platform servisleri bulunmakta

---

##   Projenin Tanımı

Bu proje kapsamında günümüzde yer alan sanallaştırma teknolojileri kullanılarak

-   Yazılım Geliştirme

-   Sistem Yönetimi

süreçlerini bir iş akışı modeli olarak tasarlayıp, gerekli ve etkili altyapının oluşturulması amaçlandı

---

##   Varolan Problemler

Proje geliştirme kısmında

-   Belirli bir standart yok, kurulum şekline bağlı büyük problemler geliştirme aşamasında doğabiliyor

-   Sonu gelmez bir tekrarlılık var, aynı şeyler sürekli elle yapılmak zorunda

-   Proje geliştirme aşamasında zaman kaybına yol açıyor

---

##   Varolan Problemler

Sunucu bilgisayarlarda kullanımı kısmında

-   Sistem yöneticisi her uygulama için aynı işi tekrarlamak zorunda

-   Her defasında daha önceden belirlenmiş standartları elle uygulamak zorunda

-   Geliştiricinin geliştirme ortamıyla, sunuculardaki ortam uyuşmayabiliyor

---

##   Problemlere Getireceği Çözümler

Bu proje temelde iki farklı amaca hizmet etmek için yapıldı

-   Kullanılacak sanal makinelerin standart bir otomatik kurulum ve verimli kullanım sürecine oturtulması

-   Sunucu sistemler tarafında daha merkezi ve kullanışlı yeni bir sanallaştırma teknolojisi altyapısı tasarımı

Bu iki iş akış modeliyle proje geliştirme ve sistem yönetimi süreçlerinin daha verimli ilerlemesi hedeflenmekte
 
---

##   Sanal Makine Fabrikası

Sanal makinelerin tamamen otomatik ve standarda oturtulmuş bir şekilde üretimini yapan fabrika

-   Arka planda sanal makine inşasını VirtualBox yapıyor

-   Üretimi otomatikleştiren ve standarda oturtan yazılım ise Packer

Fabrika temelde bu iki aracı kullanarak test-geliştirme-ürün olarak kullanılacak sanal makine imajlarının otomasyonunu yapıyor
 
---

##   Sanal Makine Fabrikası - Ürünler

Fabrikada toplamda 4 sanal makine imajı .ova formatında ve Vagrant .box formatında üretiliyor

-   Debian 7.0 testing (jessie) Headless

-   Debian 7.0 Wheezy + GNOME Desktop

-   Ubuntu 14.04 LTS (Trusty Tahr) Headless

-   Ubuntu 14.04 LTS (Trusty Tahr) + LXDE Desktop

Görsel arayüzlü makineler geliştirme ortamları, headless makineler sunucu makinelerde kullanılacak sanal makineler olarak tasarlandı

---

##   Sanal Makine Fabrikası - Üretim

Fabrika arka planda hypervisor olarak Virtualbox kullanmakta, Packer ise Virtualbox'a üretimi yapılacak makineler için tanımladığımız bilgileri besliyor

Bilgileri tanımladığımız yer : **template.json** dosyası

-   Makinenin inşa aracının ne olacağı bilgisi

-   Makineye kurulacak işletim sistemi ISO'sunun URL'i ya da dosya yolu

-   Makineyi Virtualbox'da boot edecek komut bilgisi

-   Makinenin kullanıcısı ve parola bilgisi

-   Makine kurulumu bittikten sonra makinelere karekter kazandıracak betiklerin bulunduğu dosya yolu ve nasıl olacağı bilgisi 

-   Sanal makinenin host makineden öntanımlı ne kadar RAM veya CPU tüketeceği bilgisi

gibi bir çok bilgi bu dosya altında tanımlanıyor ve Virtualbox'a http protokolü üzerinden besleniyor

---

##   Sanal Makine Fabrikası - Üretim

Fabrikada üretilecek makinelerin işletim sistemlerine özel ayarların da kurulum esnasında Virtualbox'a beslenmesi gerek

Bu özel ayarların tanımlandığı yer : **template.preseed** dosyası

-   İşletim sisteminin locale ve timezone bilgisi

-   Öntanımlı klavye dili bilgisi

-   Kullanacağı paket deposu bilgisi

gibi standart bir Linux işletim sistemi kurulumu esnasında kullanıcıya sorulan soruların standart cevapları bulunuyor

---

##   Sanal Makine Fabrikası - Standardizasyon

Kurulum bittikten sonra içi boş linux sanal makineler üretiliyor

Fabrika bu makineleri standart hale getirmek için yazdığımız shell betiklerini makine içerisinde çalıştırarak makinelere karekteristik kazandırıyor

Shell betikleri makinelere ön tanımlı vim text editör, ruby programlama dili yorumlayıcısı gibi bir çok paket program kurarak makineleri kullanıma hazır hale getiriyor

Böylece geliştirici veya sistem yöneticisi kendisi sanal makine kurmakla uğraşmadan direkt bu imajları istediği şekilde kullanabiliyor

---

##   Platform as a Service

Bu projede yapılan ikinci çalışma ise bölümümüzde kullanılmak üzere bir Platform as a Service altyapısı tasarımı

Platform as a Service günümüzde Heroku, Openshift gibi firmaların insanlara sunduğu platform servislere verilen genel ad

Web uygulama geliştiricilerini, sistem yönetimi kısmıyla uğraşmadan fiziksel sunucu makinelere uygulamalarını konuşlandırabilme imkanı sunan servis

Bu projede bu servisin bölümümüz özelinde, açık kaynaklı Dokku sistemiyle gerçeklenmesi üzerine çalışmalar yapıldı

---

##   Dokku - Platform as a Service

Dokku arka planda aşağıdaki yazılımları kullanıyor :

-   Docker Linux Konteynır Sanallaştırma Motoru

-   Açık Kaynaklı Heroku Buildpackleri

Dokku, Heroku Buildpack'leri sayesinde Rails, PHP, Java EE, Python ve Node JS uygulamaları sisteme konuşlandırılabiliyor

Her uygulama Docker sayesinde izole bir konteynır içerisinde sisteme konuşlandırılıp, nginx web sunucusu yardımıyla internete çıkarılıyor

---

##   Dokku - Konuşlandırma

Konuşlandırma aşaması aşağıdaki şekilde ilerliyor :

-   Geliştirici, Dokku sistemde uygulama konuşlandırabilmesi için SSH açık anahtarını sisteme yüklüyor

-   Daha sonra konuşlandırmak istediği proje dizini altında git aracıyla uygulamasını Dokku'ya push ediyor

-   Dokku, Buildpackleri çalıştırarak kendisine gönderilen uygulamanın hangi dille yazılmış olduğunu çözüyor

-   Uygulama sistem tarafından tanınırsa, Docker uygulama için bir sanal konteynır oluşturuyor

-   Bu sanal konteynır içerisine uygulamanın gereksinim duyduğu kütüphaneler ve kitaplıklar kuruluyor ve gönderilen proje dizini konteynıra konuşlandırılıyor

-   Son olarak nginx web sunucusu ayarları otomatik olarak yapılıyor ve kullanıcıya uygulamanın çalıştığı bir URL döndürüyor

Böylece geliştirici uygulamasını internet ağına açmış oluyor

---

##   Dokku - Eklentiler

Web uygulamalarının çoğu veritabanına ihtiyaç duyar

Dokku sistemlerde veritabanına ihtiyaç duyan uygulamalar da konuşlandırılabiliyor

Bu Dokku'nun açık kaynaklı eklentileri ile yapılıyor

Veritabanı olarak mevcut desteği bulunan eklentiler :

-   MySQL

-   PostgreSQL

-   MariaDB

Ayrıca Redis, Memcached gibi cache'leme eklentileri de Dokku sistem için mevcut

---

##   Dokku - Veritabanı Konuşlandırma

Veritabanı konuşlandırma aşaması ise aşağıdaki şekilde ilerliyor :

-   Kullanıcı uygulamasını sisteme gönderdikten hemen sonra, uygulamasıyla aynı isimde, desteği mevcut veritabanlarından birini seçip, ssh ile uzaktan komut çalıştırarak sisteme veritabanını ekliyor

-   Sistem veritabanı konteynırını oluşturup, içerisine ilgili veritabanını kurup ayarlamasını yapıyor

-   Sonrasındaysa uygulamada kullanılması için veritabanı bilgileri geliştiriciye ekran çıktısı olarak gönderiliyor

-   Geliştirici bu bilgileri kullanıp web uygulamasında veritabanı ayarlamasını yapıp uygulamasını tekrar gönderdiğinde, uygulama veritabanıyla haberleşebilir hale geliyor

Bu şekilde çoğu web uygulaması Dokku sistemlerde sorunsuz konuşlandırılıyor

---

##   Dokku'nun Avantajları

Geliştiricilere kazandırdığı avantajlar

-   Heroku Buildpack'in desteklediği dillerden herhangi biriyle yazılmış web uygulamasını internete çıkarmak için bir host makine satın alması gerekmiyor

-   Uygulamasının doğru çalışması için ayrıca sistem yönetimi işleriyle uğraşmak zorunda kalmıyor

Sistem yöneticilerine kazandırdığı avantajlar

-   PaaS hizmetini verdiği tüm uygulamalar merkezi tek bir yerde konuşlandırılıyor

-   Her uygulama için ayrı sanal makinelerle uğraşmak zorunda kalmadan sist emi yönetebiliyor

---

##   Sonuç

Bu proje kapsamında, sanal makinelere dayalı iki altyapı çalışması olan

-   Sanal Makine Fabrikası

-   Platform as a Service - Dokku sistemi

Ondokuz Mayıs Üniversitesi Bilgisayar Mühendisliği Bölümü özelinde kullanılmak üzere tamamlanmış ve istenilen hedeflere ulaşılmıştır.

---

##   Demo

Ubuntu 14.04 LTS işletim sistemi üzerinde aşağıdaki projelerin demoları

*   Sanal Makine Fabrikası

*   Dokku

---

##   Sorular ?

*   Dinlediğiniz için teşekkürler.
