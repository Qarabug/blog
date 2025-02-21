---
slug: /
title: 2FA/OTP Bypass
---

İki faktorlu autentifikasiyadan yan keçmək

### Direct bypass

2FA-nı boş verin, sadəcə növbəti son nöqtəyə birbaşa daxil olmağa çalışın (növbəti son nöqtənin yolunu bilməlisiniz). Bu işləmirsə, Referrer başlığını sanki 2FA səhifəsindən gəlmiş kimi dəyişməyə çalışın.

### Tokenin təkrar istifadəsi

Ola bilsin ki, identifikasiya etmək üçün hesabda artıq istifadə edilmiş token-I yenidən istifadə edə bilərsiniz.

### İstifadə edilməmiş tokenlərin paylaşılması

Hesabınız üçün bir token əldə edə bildiyinizi yoxlayın və başqa hesabda 2FA-dan yan keçmək üçün ondan istifadə etməyə çalışın.

### Sızdırılmış Token

Token veb tətbiqindən verilən cavabda sızdırılıbmı?

### Sessiya icazəsi

Eyni seansdan istifadə edərək hesabınızdan və qurbanların hesabından istifadə edərək axına başlayın. Hər iki hesabla 2FA nöqtəsinə çatdıqda, hesabınızla 2FA-nı tamamlayın, lakin növbəti hissəyə daxil olmayın. Bunun əvəzinə qurbanların hesabı ilə növbəti addıma daxil olmağa çalışın. Arxa tərəf yalnız seanslarınızda 2FA-dan uğurla keçdiyinizi bildirən bir boolean təyin edərsə, siz qurbanın 2FA-nı keçə biləcəksiniz.

### Parol sıfırlama funksiyası

Demək olar ki, bütün veb proqramlarda parol sıfırlama funksiyası sıfırlama proseduru tamamlandıqdan sonra istifadəçini avtomatik olaraq proqrama daxil edir.

Şifrəni sıfırlamaq üçün poçtun linklə göndərildiyini yoxlayın və parolu istədiyiniz qədər sıfırlamaq üçün həmin linkdən təkrar istifadə edə bildiyinizi yoxlayın (qurban e-poçtunu dəyişsə belə).

### OAuth

Etibarlı OAuth platformasında istifadəçinin hesabını poza bilsəniz

### Brute Force

### Tarif limitinin olmaması

Sınaya biləcəyiniz kodların miqdarında hər hansı bir məhdudiyyət var, buna görə də ona sadəcə brute force edə bilərsiniz. Mümkün "səssiz" tarif limiti ilə diqqətli olun, zəifliyi təsdiqləmək üçün həmişə bir neçə kodu, sonra isə real kodu sınayın.

### Re-send limitini sıfırlayın

Tarif limiti var, lakin siz "kodu yenidən göndərdiyiniz" zaman eyni kod göndərilir və tarif limiti sıfırlanır. Sonra, kodu yenidən göndərərkən onu brute force edə bilərsiniz ki, tarif limitinə heç vaxt çatmasın.

### İstifadəçi hesabında tarif limitinin olmaması

Bəzən hesabınız daxilində bəzi hərəkətlər üçün 2FA-nı konfiqurasiya edə bilərsiniz Bununla belə, siz daxil olmağa çalışdığınız zaman tarif limitinin mövcud olduğu hallarda belə, bu hərəkətləri qoruyan heç bir tarif limiti yoxdur.

### SMS vasitəsilə kodun yenidən göndərilməsi üçün tarif limitinin olmaması

Siz 2FA-dan yan keçmək istəyirsiniz, lakin şirkətin pulunu israf edə biləcəksiniz.

### Sonsuz OTP bərpası

Əgər siz sonsuz yeni bir OTP yarada bilsəniz, yaradılan OTP üçün 4 və ya 5 tokeni sınaya bilərsiniz, sadəcə olaraq hər dəfə eyni 4 və ya 5 tokeni sınayın və istifadə etdiyinizlərə uyğun gələnə qədər OTP-lər yaradın.

### CSRF/Clickjacking

2FA-nı söndürmək üçün CSRF və ya Clickjacking zəifliyinin olub olmadığını yoxlayın.

### Təxmin edilən kuki

Əgər “məni xatırla” funksiyası təxmin edilə bilən kodu olan yeni kukidən istifadə edirsə, onu təxmin etməyə çalışın.

### IP ünvanı

Əgər "məni yadda saxla" funksiyası sizin IP ünvanınıza əlavə olunubsa, siz _X-Forwarded-For_ başlığından istifadə edərək qurbanın IP ünvanını tapmağa və onu təqlid etməyə cəhd edə bilərsiniz.

## Köhnə versiyalar

### Subdomenlər

Giriş funksiyası ilə bəzi "sınaq" subdomenləri tapa bilsəniz, onlar 2FA-nı dəstəkləməyən köhnə versiyalardan istifadə edə bilər (buna görə də birbaşa yan keçilir) və ya bu son nöqtələr 2FA-nın həssas versiyasını dəstəkləyə bilər.

### Əvvəlki sessiyalar

2FA aktivləşdirildikdə, əvvəlki yaradılmış sessiyalar sona çatmalıdır. Bunun səbəbi müştəri hesabının oğurlanması zamanı o, 2FA-nı aktivləşdirərək onu qorumaq istəyə bilər, lakin əvvəlki seanslar bitməsə, bu onu qoruya bilməz.

### Ehtiyat kodlara səhv giriş nəzarəti

Yedək kodlar 2FA aktivləşdirildikdən dərhal sonra yaradılır və bir sorğu ilə mövcuddur. Sorğuya hər növbəti zəngdən sonra kodlar bərpa oluna və ya dəyişməz qala bilər (statik kodlar). Əgər CORS səhv konfiqurasiyaları/XSS zəiflikləri və ehtiyat kod son nöqtəsinin cavab sorğusundan ehtiyat kodları “çəkməyə” imkan verən digər səhvlər varsa, o zaman təcavüzkar kodları oğurlaya və istifadəçi adı və parol məlum olarsa 2FA-dan yan keçə bilər.

### Məlumatın Açıqlanması

2FA səhifəsində əvvəllər bilmədiyiniz bəzi məxfi məlumatlar (telefon nömrəsi kimi) görünürsə, bu, “məlumatların açıqlanması zəifliyi” hesab edilə bilər.

### Parol-Sıfırlama == disable 2fa

*   Hesab yaradın və 2FA-nı yandırın.
    
*   Həmin hesabdan çıxın.
    
*   İndi _Parolun Sıfırlanması_ səhifəsinə keçin.
    
*   Şifrənizi dəyişin.
    
*   İndi daxil olmağa çalışın.
    
*   Əgər sizdən 2FA kodu daxil etməyiniz tələb olunmursa, Siz hesabat verə bilərsiniz.
