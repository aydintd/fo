#   SSH ve Uygulamaları

.fx: first

Nihan Çaydaş `<nihan.caydas@bil.omu.edu.tr>`	 
Sayfalar : 2-18	

Aydın Doyak `<aydintd@bil.omu.edu.tr>`	
Sayfalar : 19-31

http://aydintd.me/

Şubat 2014

---

## SSH Nedir? 

*   SSH - Secure Shell/Güvenli Kabuk

*   SSH, ağ yoluyla diğer bilgisayarlara erişim sağlamak, uzak bilgisayarlarda komutlar çalıştırmak ve bilgisayarlar arası dosya transferi sağlamak amacıyla oluşturulmuş bir protokol

*   Güvensiz kanallar üzerinden güvenli iletişim(internet gibi)

*   Bir iletişimde SSH, authentication(kimlik denetimi), encryption(şifreleme), integrity(bütünlük) sağlar

---

## SSH'in Çözüm Getirdiği Problemler 

*   IP gizleme veya yönlendirme yöntemiyle yapılan saldırılar

*   Saldırganın, server isimlerinin bulunduğu kayıtları kullanılarak gerçekleştirdiği saldırılar

*   İki bilgisayar arasındaki veri trafiğinin, araya giren başka bir bilgisayar tarafından okunması, değiştirilmesi yoluyla yapılan saldırılar

*   İletişimde olan iki bilgisayar arasındaki herhangibir sunucuda bulunan kötü niyetli kişilerin yapacağı saldırılar

*   X11 sunucusundaki iletişim dinlenerek ve X doğrulaması temel alınarak gerçekleştirilen saldırılar

---

## SSH'dan Önce Kullanılan Çözümler

*   R-komutları : Şifreyi açık şekilde göndermez ancak; "rhosts" mekanizması güvenlik sorunlarına sebep olur

*   Tek Kullanımlık Şifreler : Sadece asıllamayı kontrol eder, veri akışını etmez. Bu yöntem cezbedici olsa bile kullanım kısıtlı, her yerde kullanılmaz 

*   Telnet : Bütün verileri şifrelenmemiş halde gönderirir (Parolalar da dahil!)

---

## SSH'ın Zayıflıkları

*   Kasım 2008' de SSH'ın tüm sürümlerinde teorik bir güvenlik açığı farkedildi

    -   Açık şu şekildeydi: Şifrelenmiş metnin bir bloğundan düz metnin, 32 bit üzerinde bir düz metin dönüşümüne izin veren bir güvenlik açığı

*   SSH'da, kötü niyetli kişi sisteme root kullanıcı hesabıyla giriş hakkı elde ettiği anda, SSH protokolünü rahatlıkla geçer

*   Ayrıca kötü niyetli kişi, home dizinine girdiği anda güvenlik yok olmuş demektir. Bu durum, home dizini NFS(Network File System) ile oluşturulmuş ise sıkça yaşanır

---

## SSH'ın Gelişimi

*   Finlandiya Helsinki Üniversitesinde 1995 yılında araştırmacı olarak görev yapan Tatu Ylönen, şu anda SSH-1 olarak bilinen protokolün ilk tasarımını yapmıştır 

*   Temmuz 1995'te ücretsiz olarak piyasaya sürülmüş, hızla yayılmıştır. 1995 sonlarında 50 farklı ülke, 20000 kullanıcı

*   Aralık 1995'te Ylönen, SSH Communications Security'yi pazarladı ve SSH'ı geliştirdi

*   SSH yazılımının orjinal sürümü, özgür yazılımların çeşitli parçalarında kullanıldı(GNU libgmp gibi). Ylönen, sonraki sürümlerde SSH Secure Communications'ı gittikçe artan patentli bir yazılım olarak geliştirdi

---

## SSH Özgür Yazılım Olarak Gelişimi

*   1999'a gelinildiğinde geliştiriciler, orijinal SSH'ın özgür yazılım olan halini tercih ettiler ve SSH 1.2.12 sürümüne geri döndüler
SSH 1.2.12 --> Özgür yazılım olarak ortaya çıkmıştır

*   Björn Grönvall, SHH 1.2.12 kod tabanıyla OSSH'ı geliştirdi

*   OpenBSD geliştiricileri, Grönvall'ın kodunun üzerinde çalışarak OpenSSH'ı oluşturdu ve OpenSD 2.6 sürümüyle birlikte çıkarıldı

*   2006 yılında protokolün gözden geçirilmiş bir sürümü olan SSH-2 standart olarak kabul edildi

*   SSH-2 ile Diffie-Helman anahtar değişimi ve mesaj üzerinden yetkilendirme kodları ile güçlü bir bütünlük kontrolü sağlandı

*   Günümüzde yaygın olarak SSH-2 kullanılmaktadır

---

## SSH İstemcisi Nasıl Kurulur?

*   Uçbirim açılır ve aşağıdaki komutlar yazılır :

        $ sudo apt-get install openssh-client

---

## SSH Anahtar Üretimi

*   SSH sistemlerde RSA ve DSA olarak iki farklı anahtar üretim seçeneği mevcuttur

*   Aralarındaki fark, anahtar üretim algoritmalarındaki farklılıklar

*   RSA algoritması ile örnek anahtar üretimi

        $ ssh-keygen -t rsa -C "nihan.caydas@bil.omu.edu.tr"

*   Mail - Kimlik. Oluşturulan açık anahtarın sonunda gösterilir

---

## Oluşturulan Anahtarlara Bakış

*   Anahtar oluşturulduktan sonra, sistemde beklenen iki farklı dosya

        id_rsa
        id_rsa.pub

*   id_rsa: Oluşturulan gizli(özel) anahtar

*   id_rsa.pub: Oluşturulan açık(genel) anahtar

---

## Parolasız Giriş Ve Gnome Keyring

*   Önce id kopyalanır ve giriş sorgusu atlanır

        $ ssh-copy-id user@server

*   Id kopyalama sırasında güvenlik amaçlı, bir kez şifre sorgusu yapılır ve ardından sorgusuz girişler başlar

*   Gnome Keyring: Şifre tutan bir program. Sunucuya istek sırasında devreye girer, şifreleri gönderir

*   Tutulmakta olan şifreleri göster :

        $ seahorse

---

## Karşı Sunucuda Komut Çalıştırma

*   Önemli Nokta: Komutlar tek tırnak içerisinde -> 'command'

*   Karşı sunucuya komut gönder

        $ ssh -t user@server 'command'

*   Önemli: Root sorgularda, root şifresi sorulur

---

## Kabuk Oturumunun Ayarlanması

* TODO 

---

## Farklı Kullanıcı Girişleri

*   Uzaktaki bir makineye farklı kullanıcılarla bağlanmak için,

        !sh
        $ ssh user@remote-server     # user kısmına bağlanmak istediğiniz kullanıcıyı girin

*   Uzak-sunucuya bir kullanıcıyla bağlanmanız için, o sunucuda, kullanıcının hali hazırda kullanıcı hesabının olması gerekir. Aksi taktirde makineye bağlanamazsınız

*   Bir kullanıcı, birden çok uzak makineye aynı makineden bağlanıyorsa bunu kendi kullanıcısı için istemci ayarlarını özelleştirebilir :

        !sh
        $ sudo cp /etc/ssh/ssh_config /home/user/.ssh/config
        $ vim /home/user/.ssh/config
---

## Tek Bir Ayar Dosyası

*   Örnek bir `config` dosyası içeriği :

        // default for all //
        Host *
        ForwardAgent no
        ForwardX11 no
        ForwardX11Trusted yes
        User nixcraft
        Port 22
        Protocol 2
        ServerAliveInterval 60
        ServerAliveCountMax 30
 
        //override as per host //
        Host server1
        HostName host_adı
        User nixcraft
        Port 4242
        IdentityFile /nfs/shared/users/nixcraft/keys/server1/id_rsa

---

## Port Girişleri

*   Öntanımlı port -> 22.port Farklı porta erişim

        $ssh user@server -p portnumarası

*   Kullanıcıya özel port tanımı, bir önceki slayttaki port numarasını isteğe göre güncelle

---

## İstemci Yapılandırması

*   `/home/user/.ssh/config` ayar tablosu listeler

*   Uçbirimde

        $ cat /etc/ssh/ssh_config

*   Ayarları değiştirmek için root izinlerine sahip olmalı

*   İstenilen ayar seçimi

---

## Temel Yapılandırma Ayarları

*   RSAAuthentication: Rsa key sorgulaması yapılıp yapılmayacağı

*   PasswordAuthentication: Sunucu parolası sorulup sorulmaması

*   HostbasedAuthentication: SSH'ı belirli gruplara veya kişilere sınırlandırma

*   ConnectTimeOut: Sunucuda bir şey yapılmadığı takdirde bağlı kalınacak süre

*   Port: Öntanımlı gelen 22.portu değiştirme ayarı


---

## SSH Sunucusu Ne İş Yapar?

*   SSH sunucusu, sunucu makinelere ssh protokolü üzerinden	
uzaktan erişim özelliği kazandırmak amacıyla kurulur

*   Bu sayede SSH ile güvensiz bir ağda, güvenli bir şekilde ilgili	
makineye uzaktan erişim sağlanıyor

*   SSH protokolü, telnet rlogin vb. gibi protokollerden farklı olup tüm iletişim	
güçlü kriptografik yöntemlerle şifrelenir

*   Bu nedenle kullanıcılar tarafından en çok tercih edilen uzaktan	
erişim protokollerinden biri

---

## İstemci/Sunucu Farkı

*   Bana göre bir servisin çalışma prensibini anlamak, o servisin istemcisinin ve		
sunucusunun ayrı ayrı hangi problemlere çözüm getirdiğini araştırmakla başlamalı

*   Sistem yöneticisi olarak benim çok özenli davranmaya çalıştığım noktalardan birisi bu	

*   Karşılaşılacak muhtemel problemi sınıflandırmayı, kategorize etmeyi çok kolaylaştırır	
Böylece çözüm için bakacağınız yeri önceden tahmin edebilirsiniz 
 
*   SSH İstemcisinin çözdüğü problemler özetle; güvenli iletişim isteğini sunucuya gönderme,	
kimliklendirme (gizli ve açık anahtarlar ile)		 

*   SSH Sunucusu ise, kurulduğu makineye ssh protokolü ile şifreli bir tünel üzerinden	
uzaktan erişilebilme özelliği kazandırır

---

## SSH Sunucu Kurulumu

*   Ubuntu/Debian türevi sistemlerde SSH sunucusunu aşağıdaki şekilde kurulur 

        !sh
        $ sudo apt-get install openssh-server 

*   Kurulum sırasında farkettiyseniz, sunucuyla beraber `openssh-client` paketi de sisteminize kuruluyor

*   Aşağıdaki komut çıktısı, kurduğunuz SSH sunucusunun ismini ve sürümünü size söyleyecek	

        !sh
        $ ssh -V

---

## SSH Sunucusunun Ayarlanması

*   Herşeyden önce, uzaktan erişilecek sunucuya gerçekten ssh portu üzerinden ulaşabilmek gerekiyor	

*   Makineniz muhtemel bir firewall arkasında çalışıyorsa aşağıdaki gibi bir kuralı güvenlik duvarında girmeniz gerek	

        !sh
        $ sudo iptables -A INPUT -i eth0 -p tcp --dport 22 -j ACCEPT 

*   **dport** kısmına dikkat! Ssh protokolü öntanımlı olarak 22 portunu kullanıyor 
Ön tanımlı portlar için bkz :

        !sh
        $ cat /etc/services

*   Ancak şart değil, hatta tehlikeli

---

## SSH Sunucusunun Kontrolü

*   SSH Sunucusunun sistemde çalışır halde olup olmadığını aşağıdaki şekilde kontrol edebiliriz :

        !sh
        $ ps ax | grep ssh
        2345 ?		Ss 0:00 /usr/sbin/sshd

*   Sistemde sunucu **sshd** yani ssh daemon servisi olarak görüntüleniyor

*   SSH sunucunuzun gelen bağlantıları dinleyip dinleyemediğini aşağıdaki şekilde kontrol edebiliriz :

        !sh
        $ sudo netstat -ap | grep ssh
        tcp        0      0 *:ssh                         *:*                     LISTEN      2345/sshd       
        tcp6       0      0 [::]:ssh                      [::]:*                  LISTEN      2345/sshd

*   Ya da direkt olarak yerelde port taraması yapabilirsiniz :

        !sh
        $ nc -v -z 127.0.0.1 22
        localhost [127.0.0.1] 22 (ssh) open

---

## Sunucunun Temel Yapılandırma Ayarları

*   Ubuntu/Debian sistemlerde SSH Sunucusunun ayar dosyası `/etc/ssh/sshd_config` dosyası altında tutulur

*   Temel ayarlamaları bu dosyayı düzenleyerek yapmak gerekiyor 

*   Sadece SSH için değil, hangi servis olursa olsun, eğer ilk ayarları bir şekilde modifiye edecekseniz servisin ayar dosyasının bir yedeğini almanız önerilir

        !sh
        $ sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
        $ sudo chmod a-w /etc/ssh/sshd_config.orig

*   Linux sistemlerde servis ayarlarının tutulduğu dosyalar, ayar dosyası olmakla beraber iyi birer kullanım kılavuzu özelliği de barındırırlar

*   Bu yüzden fabrika ayarlarıyla gelen dosyayı sadece okunur şekilde izinlerini ayarlıyorum, ancak	
şart değil

---

## Temel Yapılandırma Ayarları - Port

*   Ayar dosyasını bir metin editörüyle açıp, içeriğine göz atalım

        !sh
        $ sudo vim /etc/ssh/sshd_config

*   Bizi ilk başta, SSH Port ayarı karşılıyor. Bu port öntanımlı olarak 22 şeklinde ayarlandığını görüyoruz

*   22 portu, çalışan makineniz hakkında yabancı bir saldırganın, makineniz üzerinde sızma girişiminde bulunacağı ilk kapılardan biri

*   Bir çok yöntemle bu port saldırganlar tarafından deneniyor, makinenizin güvenliğini bir ölçüde artırmak için ssh portunu değiştirebiliriz

*   Çoğu karşılaştığım yerde 2222, 1234 gibi bir çok farklı ssh portları kullanılmakta, dikkat etmeniz gereken tek şey tayin ettiğiniz porta erişimi
(eğer kullanıyorsanız) güvenlik duvarında izin vermek

---

## Temel Yapılandırma Ayarları - Anahtarlar

*   SSH Sunucunuzun açık ve gizli anahtarlarının dosya yolu bilgisi ve ilgili ayarlar kısmı

*   SSH sunucunuzu kurduğunuzda, `/etc/ssh` dizini altında sunucunun açık ve gizli anahtarları üretilir

*   Bu dosyaların izinlerinin açık anahtarlar için **611**, gizli anahtarlar için kesinlikle **600** olarak ayarlandığından emin olun

---

## Temel Yapılandırma Ayarları - Loglama

*   SSH loglarının nerede tutulduğunu şu şekilde öğrenebiliriz :

        !sh
        $ sudo grep -lri sshd /var/log
        /var/log/auth.log
        /var/log/apt/term.log

*   auth.log içeriğine bakacak olursak, sunucu üzerindeki ssh aktivitelerini gözlemleyebiliriz

        !sh
        $ sudo tail -300 /var/log/auth.log

*   *sshd_config*'de Loglama ile alakalı ayarlar bulunuyor. Bu ayarlar sistemin log sunucusunun kullanılması ve loglama seviyesi

*   Sunucunuzda detaylı loglama yapmak istiyorsanız aşağıdaki **INFO** girdisini **VERBOSE** olarak değiştirin :

        !sh
        # Logging
        SyslogFacility AUTH
        LogLevel INFO           # VERBOSE 
---

## Temel Yapılandırma Ayarları - Güvenlik

*   Sunuculara uzaktan erişirken, SSH ile sunucunuzun güvenliğini önemli ölçüde artırabiliyoruz

*   Sunuculara **root** kullanıcısıyla ulaşımı engellemek, saldırganın **root** kullanıcısını kullanarak sisteminize sızmaya çalışmasını engeller :

         !sh
         PermitRootLogin yes       # no

*   Parola kullanarak sunucuya erişim özelliğini kaldırmak da, saldırganların ssh sunucunuza rastgele parola deneyerek sızma ihtimalini ortadan kaldırır :

        !sh
        PasswordAuthentication yes     # no

*   Peki parola kullanılmayacaksa sunucuya nasıl erişilecek?

---

## Ortak Anahtarlarla Sunucuya Erişim 

*   Erişim için doğrudan bir parola olmadan, kullanıcının ve sunucunun ortak anahtarlarının aralarında paylaşılması ve güvenli bağlantının oluşturularak kimlik kontrolünün yapılması şeklinde olur

*   Bu sunucunun güvenliğini yadsınamaz şekilde artırarak, çok bitlik çözülmesi imkansız bir anahtar yardımıyla sunucuya erişim sağlanır

*   Ssh istemcisi aşağıdaki şekilde sunucuya açık anahtarını gönderir :

        !sh
        $ ssh-copy-id user@remote-server
	
        /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
        /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
        user@remote-server's password: 

        Number of key(s) added: 1

        Now try logging into the machine, with:   "ssh 'user@remote-server'"
        and check to make sure that only the key(s) you wanted were added.

---

## Ortak Anahtarlarla Sunucuya Erişim

*   İstemci eğer sunucuda kayıtlı bir kullanıcı hesabına sahipse anahtarını sunucuya gönderebilir.

*   İstemciden gönderilen anahtar, uzak sunucudaki istemcinin kullanıcısının ev dizinine kopyalanır

        !sh
        $ cat /home/user/.ssh/authorized_keys      # @uzak-sunucu	

*   Şeklinde anahtara bakıldığında, istemcinin açık anahtarıyla aynı olduğu görülür. Böylece parolasız, ortak anahtarlar yardımıyla
sunucuya erişim sağlanır

---

## SSH Kullanıcı İzinleri ve Banner Ayarları

*   `sshd_config` dosyasında yapılabilecek son ayarlar sunucuya kimin erişip kimin erişmeyeceği bilgisini SSH'a geçirmek olabilir

*    Aşağıdaki satırları `sshd_config` dosyasının sonuna ekleyin :
 
        AllowUser can, ecylmz                 # İzin ver
        DenyUser 1CrazyGirL9, bilal           # İzin verme

*    Ve son olarak, SSH'la bağlanmaya çalışan kullanıcılara bir mesaj görüntületebilirsiniz :

        !sh
        #Banner /etc/issue.net      # Yorum satırını kaldırıp, /etc/issue.net dosya içeriğini görüntülenecek mesajla değiştir

*    Tüm bu ayarların aktive olması için sshd servisini yeniden başlatmak gerekiyor :

        !sh
        $ sudo service ssh restart

---

## Sıkça Karşılaşılan Problemler

*   Senaryo :

Sunucuda hesabı olmayan kullanıcının kendi kullanıcısıyla bağlanmaya çalışması

Eğer uzak sunucuda kendinize ait bir kullanıcı hesabınız yoksa, oraya zaten ssh'la bağlanamazsınız

Ancak genelde bir sunucuya bağlanılmak istendiğinde aşağıdaki komut yazılır :

         !sh
         $ ssh uzak-sunucu-ipsi    # ya da domaininin adı

Bu komut aynen şöyle işler

         !sh
         $ ssh istemci-makine-kullanicisi@uzak-sunucu-ipsi

Komutu çalıştırdığınız kullanıcının eğer uzak sunucuda hesabı yoksa sunucuya bağlanamazsınız

Yapmanız gereken şey, sunucudaki kullanıcınızla, istemcinizdeki kullanıcınızın aynı olmasını sağlamak ya da kullanıcı adı belirterek makineye bağlanmaktır

---

## Sıkça Karşılaşılan Problemler

*   Dosya izinleri de problem çıkarabilir

OpenSSH sunuculardaki `~/.ssh` dizinini `700` , `~/.ssh/authorized_keys` dosyasını da `600` olarak ayarlamanızı önerir

        !sh
        $ chmod go-w ~/.ssh ~/.ssh/authorized_keys

*   Eğer öngöremediğiniz bir problemle karşı karşıya olduğunuzu düşünüyorsanız, SSH sunucunuzu debug modda çalıştırıp, istemci tarafında logları gözlemleyebilirsiniz

Sunucu tarafında :

        !sh
        $ /usr/sbin/sshd -d -p 2222      # Sunucuyu debug modda 2222. port üzerinde çalıştır

İstemci tarafında :

        !sh
        $ ssh -vv -p 2222 user@remote-server   # Sunucu-istemci bağlantı çıktılarını izle

---

## Sunum Sonu

- Sorular ?

