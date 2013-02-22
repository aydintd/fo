#   Vagrant 2

.fx: first

Aydın Doyak `<aydintd@bil.omu.edu.tr>`

http://aydintd.me/

Şubat 2013

---

##  İçerik

Bu folyoda detaylı şekilde aşağıdaki konular hakkında bilgiler verilecek

*   Temel Kutuların çalışma mantığı

*   İstenilen işletim sistemiyle, yazılım geliştirme
    araçlarını barındıran kendinize özel bir Vagrant temel kutusu
    hazırlamak

---

##  Başlarken

Dört önemli konu üzerinde duracağız

*   Temel kutu hazırlama şartları

*   VirtualBox Misafir Eklentilerinin kurulumu

*   Vagrant kullanıcısının doğrulanması için anahtar tabanlı SSH

*   Ruby, rubygems kurulumu ve chef-solo, puppet kurulumu(isteğe bağlı)

---

##  Şartlar

Seçtiğimiz işletim sistemini ilk önce VirtualBox da oluşturacağız

*   İşletim sisteminin ne olacağı tamamen size kalmış

*   Sürüm hakkında gereken tek şart 32bit işletim sistemi tercih etmeniz

*   Kullandığınız işletim sisteminin operatörlüğünü iyi yapabilmeniz önemli

---

##  VirtualBox Imajı

Temel Kutu hazırlamak için VirtualBox şart

*   VM imajınız için ayırdığınız alan önemli

*   Dinamik olarak ayarlanabilir 40 GB disk alanı neredeyse her şey için yeterli

*   Belleğin çok olmamasına dikkat! Tercihen 360 MB başlangıç için iyi

*   1 GB ın üzeri bellek kullanan kutular fazla tercih edilmiyor

*   Kullanmayacaksanız ses ve usb kontrollerini devre dışı bırakın, çoğu
    uygulama ses gereksinimi duymuyor

---

##  VirtualBox Imajı

*   Ağ Kontrol Mekanizmasının NAT olarak ayarlı olması çok önemli

*   Imajınızın internete çıktığından emin olmanız gerek aksi takdirde
    kutunuz çalışmayacaktır

Şimdi işletim sisteminizi .iso olarak ya da DVD den VM üzerinde boot edin

---

##  İşletim Sistemi Kurulumu

Kutunuzun son büyüklüğü çok önemli

*   Ortamınızın fazlalıklardan arınması gerek

*   Örneğin 5 GB lık kutunuz indirilmek ve her defasında boot etmek için
    kullanışlı değil

*   Fazlalıklar için uygulayabileceğiniz bir kaç yöntem var

---

##  Yöntemler

*   İşletim sisteminizi GUI olmadan kurun. Örneğin Debian Wheezy işletim
    sisteminde sistemin kendisi görsel arayüz olmadan kurulduğunda 1 GB lık bir
    alandan feragat ediyorsunuz

*   Kutunuzun sistem önbelleklerine ve tmp dosyalarına ihtiyacı olmayacak, UNIX
    tabanlı çoğu sistem için önbelleği

        !sh
        $ sudo apt-get clean

    ile kaldırabilirsiniz

*   RubyGems kurulumu yaparken dokümantasyon dosyalarına da ihtiyacınız
    olmayacak

        !sh
        $ sudo apt-get install rubygems --no-rdoc --no-ri

    ile dokümantasyon dosyalarını filtreleyip sisteminize kurabilirsiniz

---

##  Konvansiyonlar

*   Vagrant da neredeyse her şey değiştirilebilir

*   Ancak başlangıç için bir kaç konvansiyon gerekiyor

*   Bu konvansiyonlardan biri de makine adı ve kullanıcı adının ne olacağıyla
    alakalı

*   İşletim sisteminizi kurarken aşağıdaki kabulleri yapmanızı öneriyoruz

        Hostname: vagrant-host-name ör: vagrant-debian-wheezy
        Domain: vagrantup.com
        Root Şifresi: vagrant
        Ana kullanıcı adı: vagrant
        Kullanıcı şifresi: vagrant

*   Vagrant, kutunuzda yukarıdakileri öntanımlı olarak alıyor

*   Eğer kullanıcı adı veya şifrede değişiklik yaptıysanız bunu ilerde
    Vagrantfile da tanımlamanız gerekecek aksi takdirde kutunuz çalışmayacaktır

---

##  Kutu Konfigurasyonu

Sanal makinenizin kurulumu bittikten sonra yapmanız gereken bir kaç
konfigürasyon var

*   Bunlardan ilki kullanıcının şifresiz sudo haklarına erişimi

*   Vagrantın çalışabilmesi için bu hakkı sanal makinenizdeki ana kullanıcıya
    sağlamanız gerekiyor

Peki bunu nasıl yapacağız?

---

##  Şifresiz sudo erişimi

        !sh
        $ su

Bu komuttan sonra root şifreniz istenecek ve makinenizde root olacaksınız

        !sh
        $ visudo

Bu sudo nun dosya ayarı, sadece root iken giriş yapabileceğiniz bir ayar dosyası

*   Bazı kemik sistemlerde sudo sisteminize kurulu olmadan yüklenir eğer
    sisteminizde sudo kurulu değilse root olup

        !sh
        $ aptitude install sudo

    ile kurabilirsiniz

---

##  Visudo

Bu dosya sudo izinlerinin kime verileceğini tanımlayabildiğiniz bir ayar dosyası
Aşağıdaki satırları dosyaya sırasıyla ekleyin

        Defaults env_keep="SSH_AUTH_SOCK"

*   Visudo dosyasında sıra önemli o yüzden diğer değişkenlerin bulunduğu kısmın
    hemen altına env_keep değişkenini ekleyin

*   Şimdi admin grubuna şifresiz erişim hakkını vermemiz gerekiyor

        %admin ALL=NOPASSWD: ALL

    satırını %sudo satırının hemen altına ekleyin ve %sudo satırını
    commentleyin.

---

##  Visudo

Dosyaya admin grubunu ekledik ama sistemimizde admin diye bir grup yok
Şimdi bu grubu oluşturalım ve kullanıcımızın gruplarına ekleyelim

        !sh
        $ groupadd admin
        $ usermod -aG admin vagrant

*   Tüm bu ayarların aktive olması için sistemimizi yeniden başlatmamız
    gerekiyor

*   Sistem tekrar açıldığında

        !sh
        $ sudo which sudo
        >/usr/bin/sudo

    gibi bir çıktıyı şifre girmeden görmemiz gerekiyor

*   Buraya kadar her şey normalse Virtual Box Misafir Eklentileri kurulumuna geçebiliriz

---

##  VirtualBox Guest Additions

Vagrant a tüm gücü şifresiz erişim hakkıyla verdik

Şimdi yapmamız gereken paylaşılan dosyalar ve port yönlendirmeleri için
VirtualBox un bize sunduğu misafir eklentilerini kurmamız gerekecek

Aşağıdaki işlemleri sırasıyla yapalım

        !sh
        $ sudo apt-get install linux-headers-$(uname -r) build-essential

*   Misafir eklentileri imajını VirtualBox penceresindeki Araçlar kısmında
    Install Guest Additions a tıklayarak yerleştirelim ve

        !sh
        $ sudo mount /dev/cdrom /media/cdrom
        $ sudo sh /media/cdrom/VBoxLinuxAdditions.run

    diyerek misafir eklentilerini kuralım

*   Eğer ortamı GUI olmadan kurmuşsanız Guest Additions kurulumun sonunda
    Pencere Sistem Sürücüleri veya OpenGL eksikliği hakkında uyarı verecektir
    bu uyarıları görmezden gelebilirsiniz

---

##  Yazılımların Kurulumu

Vagrantın çalışması için gereken yazılımlar şu şekilde

*   Ruby ve Rubygems

        !sh
        $ sudo apt-get install ruby rubygems

    Daha önceleri bahsettiğimiz gibi chef ya da puppet Vagrant kutusu için
    hayati değil

*   SSH Sunucusu

---

##  SSH Konfigürasyonu

*   SSH Sunucusunu sistemimize kuralım

        !sh
        $ sudo apt-get install ssh
        $ echo 'UseDNS no' >>/etc/ssh/sshd_config

*   /home dizinimiz içinde .ssh dizinini oluşturup Vagrantın bize sağladığı
    ssh anahtarını authorized_keys dosyası içine kopyalamamız gerekiyor

        !sh
        $ mkdir .ssh
        $ wget --no-check-certificate -0 .ssh/authorized_keys
        https://raw.github.com/mitcellh/vagrant/master/keys/vagrant.pub
        $ chmod 700 .ssh
        $ chmod 600 .ssh/authorized_keys

        $ sudo apt-get clean
        $ sudo poweroff

*   Bütün ayarlar bitti artık imajımızın son halini paketleyip kutu haline
    getirebiliriz

---

##  Kutu Hazırlama

*   Imajı kutu haline getirmek için yapmamız gereken tek şey .vbox uzantılı
    dosyayla aynı dizin içersinde aşağıdaki komutu yazmak

        !sh
        $ vagrant package --base kutu_adi

*   Kutunun hazırlanma süreci bir kaç dakika kadar sürebilir, işlem bittiğinde
    bulunduğunuz dizin içinde package.box u göreceksiniz 

*   Kutuya bağlanmak için aşağıdaki komutları sırasıyla verin

        !sh
        $ vagrant box add kutu_adi package.box
        $ mkdir test_ortami
        $ cd test_ortami
        $ vagrant init kutu_adi
        $ vagrant up
        $ vagrant ssh

Eğer buraya kadar her şeyi doğru yapmışsanız hazırladığınız imaja Vagrantla
ulaşabileceksiniz

İşte her şey bu kadar!

---

##  Kaynak

![vagrant-logo](media/vagrant-logo.png)

*   http://docs.vagrantup.com/v1/docs/index.html
