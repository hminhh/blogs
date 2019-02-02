---
title: "[hackthebox.eu] Hackthebox Invite Code"
date: 2019-01-19T09:13:54+07:00
draft: false
tags: [hackthebox.eu]

---
---
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/invi1.jpg" class="img-responsive">

Một số cty nước ngoài kiếm email phỏng vấn cũng bằng cách này, thường chỉ khai thác ở client , nên cứ bem theo `view-source` mà chơi thôi 🤞Tuy vậy HTB có một vài
thủ thuật *gài* (mặc dù k đáng kể) như để canvas để chuột phải ko thể view-source hoặc view-source được thì đã minify cho xấu đi =)))

<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/invi2.jpg" class="img-responsive">

Có hai file JS đáng nghi vấn, mở lên xem thử:

`https://www.hackthebox.eu/js/calm.js`
```javascript
console.log(`%c
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
.                                                                                 .
.                      uuuuuuu                                                    .
.                  uu$$$$$$$$$$$uu                                                .
.               uu$$$$$$$$$$$$$$$$$uu                                             .
.              u$$$$$$$$$$$$$$$$$$$$$u                                            .
.             u$$$$$$$$$$$$$$$$$$$$$$$u                                           .
.            u$$$$$$$$$$$$$$$$$$$$$$$$$u                   K E E P  C A L M       .
.            u$$$$$$$$$$$$$$$$$$$$$$$$$u                                          .
.            u$$$$$$"   "$$$"   "$$$$$$u                        A N D             .
.            "$$$$"      u$u       $$$$"                                          .
.             $$$u       u$u       u$$$                        H A C K            .
.             $$$u      u$$$u      u$$$                                           .
.              "$$$$uu$$$   $$$uu$$$$"                         T H I S            .
.               "$$$$$$$"   "$$$$$$$"                                             .
.                 u$$$$$$$u$$$$$$$u                             B O X             .
.                  u$"$"$"$"$"$"$u                                                .
.       uuu        $$u$ $ $ $ $u$$       uuu                                      .
.      u$$$$        $$$$$u$u$u$$$       u$$$$                                     .
.       $$$$$uu      "$$$$$$$$$"     uu$$$$$$                                     .
.     u$$$$$$$$$$$uu    """""    uuuu$$$$$$$$$$                                   .
.     $$$$"""$$$$$$$$$$uuu   uu$$$$$$$$$"""$$$"                                   .
.      """      ""$$$$$$$$$$$uu ""$"""                                            .
.                uuuu ""$$$$$$$$$$uuu                                             .
.       u$$$uuu$$$$$$$$$uu ""$$$$$$$$$$$uuu$$$                                    .
.       $$$$$$$$$$""""           ""$$$$$$$$$$$"           HackTheBox v0.9.3       .
.        "$$$$$"                      ""$$$$""           info@hackthebox.eu       .
.          $$$"                         $$$$"                                     .
.                                                                                 .
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .`,"color:#9acc14; background:black; font-family: monospace");
```
Đơn giản file này chỉ là `console.log` ra cho màu nè đầu lâu thôi 💀

Ngược lại file này đáng nghi hơn `https://www.hackthebox.eu/js/inviteapi.min.js`
```javascript
eval(function(p,a,c,k,e,d){e=function(c){return c.toString(36)};if(!''.replace(/^/,String)){while(c--){d[c.toString(a)]=k[c]||c.toString(a)}k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}('1 i(4){h 8={"4":4};$.9({a:"7",5:"6",g:8,b:\'/d/e/n\',c:1(0){3.2(0)},f:1(0){3.2(0)}})}1 j(){$.9({a:"7",5:"6",b:\'/d/e/k/l/m\',c:1(0){3.2(0)},f:1(0){3.2(0)}})}',24,24,'response|function|log|console|code|dataType|json|POST|formData|ajax|type|url|success|api|invite|error|data|var|verifyInviteCode|makeInviteCode|how|to|generate|verify'.split('|'),0,{}))
```
Thứ nhất code đã bị `obfuscation` và minify, tuy nhiên bạn hãy để ý hàm `eval` kia sẽ thực thi đoạn script bên trong, cụ thể hơn hàm eval này chạy sẽ tạo ra 1 đoạn code bình thường.Bỏ hàm eval và pretty lại code
```javascript
(function(p, a, c, k, e, d) {
    e = function(c) {
        return c.toString(36)
    };
    if (!''.replace(/^/, String)) {
        while (c--) {
            d[c.toString(a)] = k[c] || c.toString(a)
        }
        k = [function(e) {
            return d[e]
        }];
        e = function() {
            return '\\w+'
        };
        c = 1
    };
    while (c--) {
        if (k[c]) {
            p = p.replace(new RegExp('\\b' + e(c) + '\\b', 'g'), k[c])
        }
    }
    return p
}('1 i(4){h 8={"4":4};$.9({a:"7",5:"6",g:8,b:\'/d/e/n\',c:1(0){3.2(0)},f:1(0){3.2(0)}})}1 j(){$.9({a:"7",5:"6",b:\'/d/e/k/l/m\',c:1(0){3.2(0)},f:1(0){3.2(0)}})}', 24, 24, 'response|function|log|console|code|dataType|json|POST|formData|ajax|type|url|success|api|invite|error|data|var|verifyInviteCode|makeInviteCode|how|to|generate|verify'.split('|'), 0, {}))
```
Chạy luôn trong Chorme Dev-Tool là ra kết quả 
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/invi3.jpg" class="img-responsive">

```javascript
function verifyInviteCode(code) {
    var formData = {
        "code": code
    };
    $.ajax({
        type: "POST",
        dataType: "json",
        data: formData,
        url: '/api/invite/verify',
        success: function(response) {
            console.log(response)
        },
        error: function(response) {
            console.log(response)
        }
    })
}

function makeInviteCode() {
    $.ajax({
        type: "POST",
        dataType: "json",
        url: '/api/invite/how/to/generate',
        success: function(response) {
            console.log(response)
        },
        error: function(response) {
            console.log(response)
        }
    })
}
```

Đến đây nhìn vô là biết `ajax` để gọi đến các api get code. Dùng `postman` gọi đển theo phương thức POST `https://www.hackthebox.eu/api/invite/how/to/generate`

<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/invi4.jpg" class="img-responsive">

```javascript
    atob("SW4gb3JkZXIgdG8gZ2VuZXJhdGUgdGhlIGludml0ZSBjb2RlLCBtYWtlIGEgUE9TVCByZXF1ZXN0IHRvIC9hcGkvaW52aXRlL2dlbmVyYXRl")
    // "In order to generate the invite code, make a POST request to /api/invite/generate"
```

Theo gợi ý, tiếp tục gọi đển theo phương thức POST `https://www.hackthebox.eu/api/invite/generate`

<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/invi5.jpg" class="img-responsive">

```javascript
    atob("QVpUU0EtSkJZUk8tQlpXUVYtV1VaTkYtVlJITVQ")
    //"AZTSA-JBYRO-BZWQV-WUZNF-VRHMT"
```

Đến đây là code code rồi, submit rồi reg acc vào chiến thôi!!
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/invi6.jpg" class="img-responsive">
