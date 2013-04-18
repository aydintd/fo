#   Otomata Sunum

.fx: first

Aydın Doyak `<aydintd@bil.omu.edu.tr>`  

http://aydintd.me/

Nisan 2013

---
##  Sunumu Hazırlayanlar

Mine Öztürk `<mine.ozturk@bil.omu.edu.tr>`  

Merve Arslan `<mervearslan@bil.omu.edu.tr>`

Şeyma Tekin `<seyma.tekin@bil.omu.edu.tr>`  

Aydın Doyak `<aydintd@bil.omu.edu.tr>`  

Koray Tahta `<koray.tahta@bil.omu.edu.tr>`  

Gözde Sevinç `<gozde.sevinc@bil.omu.edu.tr>`  

---

##  Düzenli ifadelerin NFAya Dönüşümü

.fx: first

Numara  
Merve Arslan

---

##  Düzenli ifadelerin NFAya Dönüşümü

*   Düzenli ifadelerin NFAya dönüştürülmesi **Thompson Algoritması** yardımıyla
    gerçekleştirilir.

*   Gösterimler şu şekildedirler :

`1- Boş eleman ε :` ![merve1](media/merve1.png)

`2- a :` ![merve2](media/merve2.png)

`3- a | b :` ![merve3](media/merve3.png)

---

##  Gösterimler

`4- ab :` ![merve4](media/merve4.png)

`5- a* :` ![merve5](media/merve5.png)

---

##  Örnekler

*   Örnek 1: `a*b*` ifadesini NFA'ya dönüştürelim. Üretilebilecek en kısa
    dizgi (string) `ε` yani boş küme olacaktır. Çünkü yıldız işleminin üreteceği
    sonuçlar arasında boş küme de bulunmaktadır.

İkinci dizgimiz `ab` olacaktır ve bu üretme işlemi
`aab, abb, aabb, aaab, abbb` şeklinde devam edecektir.

![merve6](media/merve6.jpg)

---

##  Örnekler

*   Örnek 2: `L = ab U a*` sözcüğünü NFA'ya çevirin.

![merve7](media/merve7.png)

![merve8](media/merve8.png)

---

##  Örnekler

![merve9](media/merve9.png)

---

##  Düzenli Diller İçin Pumping Lemma

.fx: first

10060314  
Koray TAHTA

---

##  Pumping Lemma Şartları

*   `W = xyz`  W stringi üç parçaya ayrılabilmeli

*   `Her i >= 0; x yⁿ z  E   L`

*   `|y| > 0`  Orta kısım boş olamaz, y != NULL

*   `|xy| <= p` Pumping ilk p sembol için meydana gelir

---

##  Pumping Lemma Şartları

*   Bir dilin düzenli (regular) olmadığını ispatlamak için kullanılan
    bir kanıtlama yöntemidir

*   L düzenli bir dil olsun. Bu dil için pumping number isimli bir "p" sayısı
    mevcuttur. Bu dil içerisinden seçilen herhangi bir "w" stringin uzunluğu, p
    sayısına eşit veya daha büyük olmak zorundadır

![koray1](media/koray1.png)

*   L dili düzenli bir dil ise;
    `x, y (y != null) ve z üç adet string olmak üzere; xyⁿz (n = 1,2,3,...)`
    biçimindeki stringler de L dilinin elemanıdır. Aksi halde incelenen dil
    düzenli bir dil değildir.

---

![koray2](media/koray2.png)


*   w = bbbababa
    x = bb
    y = bba
    z = baba

*   b bba bba baba ε L olmalıdır

*   b bba bba bba baba ε L olmalıdır

*   x yⁿ z ε L olmalıdır

---

##  Pumping Lemma Geliştirilmiş Versiyon

*   Örnek : Palindrome dilinin düzgün olmayan bir dil olduğunu ıspatlayınız.

*   Çözüm : N = 77 durum olduğunu varsayınız.
    w = xyz = a⁸⁰ba⁸⁰ olsun.  

    |w| = 161 ve 161 > 77 olduğuna dikkat ediniz.

*   |x + y| < 77 olacak şekilde parçalarsak;

    a⁷⁵ a a⁴ba⁸⁰ >> x = a⁷⁵, y = a, z = a⁴ba⁸⁰ 


    x yⁿ z = a⁷⁵aa..a a⁴ba⁸⁰ ε Palindrome olmalıdır  
    Fakat, a⁸¹ba⁸⁰ !ε Palindrome olduğundan bu dil düzensiz bir dildir.

