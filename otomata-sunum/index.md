#   Otomata Sunum

.fx: first

Aydın Doyak `<aydintd@bil.omu.edu.tr>`  

http://aydintd.me/

Nisan 2013

---
##  Sunumu Hazırlayanlar

Aydın Doyak `<aydintd@bil.omu.edu.tr>`  

Şeyma Tekin `<seyma.tekin@bil.omu.edu.tr>`  

Gözde Sevinç `<gozde.sevinc@bil.omu.edu.tr>`  

Merve Arslan `<merve.arslan@bil.omu.edu.tr>`  

Mine Öztürk `<mine.ozturk@bil.omu.edu.tr>`  

Koray Tahta `<koray.tahta@bil.omu.edu.tr>`  

---

##  Düzenli Diller İçin Pumping Lemma

.fx: first

Numara  
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
