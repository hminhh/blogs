---
title: "[hackthebox.eu] Web Challenge"
date: 2019-01-15T20:02:08+07:00
draft: false
tags: [CTF,hackthebox.eu]
---
---
# #.LIST OF CHALLAGE
|ID| Challgenge  | Done  |
|------------| ------------ | ------------ |
|**1**|[**[30 Points] HDC**](#1)|✅|
|**2**|[**[50 Points] I know Mag1k**](#2)|✅|
|**3**|[**[70 Points] Grammar**](#3)|✅|
|**4**|[**[20 Points] Lernaean**](#4)|✅|
|**5**|[**[30 Points] Cartographer**](#5)|✅|

---
<a name="1"></a>
# 1.HDC [by Thiseas]
> **Description** : We believe a certain individual uses this website for shady business. Can you find out who that is and send him an email to check, using the web site's functionality? Note: The flag is not an e-mail address.

Mở đầu Chall là hai ô input nhập vào username/password
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/hdc1.jpg" class="img-responsive">
Tuy nhiên khi view-source thì thấy 2 input type `hidden` 👀 khá đáng ngờ , check tiếp hàm `doProcess()` trong `myscript.js`
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/hdc3.jpg" class="img-responsive">
Chả có gì đặc biệt...Chỉ là hàm submit form bình thường , loay hoay debug bằng `DevTools` cũng chưa thấy gì đặc biệt.
Lúc này có hai ô input type `hidden` check các kiểu thì thấy form k sử dụng 2 thằng này, mò một hồi thì thấy trong lib jquery có 1 hàm 
`doProcess()` nữa 
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/hdc4.jpg" class="img-responsive">
Sử dụng username/password được set trong hàm này submit form thì login thành công ^^
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/hdc2.jpg" class="img-responsive">
Bấm lung tung một hồi cũng chưa kiếm được cái mail chall yêu cầu, check lại burpsuite thì thấy có link lạ `/main/secret_area_/`.
Mở ra thì có `mail.txt`. Lúc này k phải 1 mail nữa mà là cả 18 cái mail để test :| Không thích lắm nhưng bruteforce thôi.
Tiến thành bruteforce bằng form gửi mail, setup với burpsuite cho lẹ khỏi phải code :D
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/hd5.jpg" class="img-responsive">
DONE! Có Flag submit!!

---
<a name="2"></a>
# 2.I know Mag1k [by rkmylo]
> **Description** : Can you get to the profile page of the admin? 

<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Mag1k1.jpg" class="img-responsive">
Mới vào chall mình ngộp hẳn :| mình k có kinh nghiệm mấy trong khai thác `sqlinjection` lắm, đc hint từ một người bạn thì mình biết
bài này dạng `decrypt` và sử dụng `padbuster`.<br>
Tạo một acc rồi login vào xem cookie của trang cấp là gì
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Mag1k2.jpg" class="img-responsive">
Ok tìm ra cookie có tên là `iknowmag1k`
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Mag1k3.jpg" class="img-responsive">
Có hint rồi là dùng luôn `padbuster` rồi thì chơi thôi :D 
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Mag1k4.jpg" class="img-responsive">
:) đệt quá trình lâu hơn mình nghĩ cuối cùng cũng decrypt ra đc session
```json
{"user":"admin","role":"user"}
```
Tiến hành dùng `padbuster` một lần nữa để tạo ra session fake `{"user":"admin","role":"admin"}` (username mình tạo là admin nhé ^^) 
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/mag1k5.jpg" class="img-responsive">



- **Note**: [Padding Oracle Attacks](https://www.owasp.org/index.php/Testing_for_Padding_Oracle_(OTG-CRYPST-002))

---
<a name="3"></a>
# 3.Grammar [by forGP]
> **Description** : When we access this page we get a Forbidden error. However we believe that something strange lies behind... Can you find a way in and retrieve the flag?

Dựa vào gợi ý và kinh nghiệm chơi khi thấy đầu chall và hint là `Forbidden error` thì nghĩ ngay đến đổi method của request
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Grammar0.jpg" class="img-responsive">
Bằng một số biện pháp fuzz nhẹ thì phát hiện trang `index.php`, đổi method thành `POST` và pass thành công 
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Grammar3.jpg" class="img-responsive">
Trang này cũng k có gì đặc biệt , thử submit form cũng ko có gì thay đổi
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Grammar1.jpg" class="img-responsive">
Lướt sơ vô session, thì thấy tên session khá lạ, thường session của PHP thường là `PHPSESSID` mà ở đây lại là `ses` 🍌
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Grammar2.jpg" class="img-responsive">
basecode64 thôi
```javascript
"eyJVc2VyIjoic2FkZGVhbiIsIkFkbWluIjoiRmFsc2UiLCJNQUMiOiI0NjFiOWUwNGRmOTQwY2NlMWUyMDhlMjNiOTFjYzAxYSJ9=="
//output: {"User":"saddean","Admin":"False","MAC":"461b9e04df940cce1e208e23b91cc01a"}

//change json: `{"User":"saddean","Admin":"True","MAC":"461b9e04df940cce1e208e23b91cc01a"}`
"eyJVc2VyIjoic2FkZGVhbiIsIkFkbWluIjoiVHJ1ZSIsIk1BQyI6IjQ2MWI5ZTA0ZGY5NDBjY2UxZTIwOGUyM2I5MWNjMDFhIn0="
```
Đời không như mơ 😂
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Grammar4.jpg" class="img-responsive">
Nhìn thoáng thì trong đoạn decode còn 1 tham số MAC, chắc có vẻ dùng để matching với server, Nếu ai hay viết API cho `ReactJS` thì chắc ko lạ gì với cái này nữa.
Cụ thể `MAC` kia giống như một `integrity key` để kiểm tra tính đúng đắn của json, khó để mà tạo lại cái `MAC` đó vì có thể có `secret key`....Tuy nhiên với một người theo chủ nghĩa ko thích `PHP`
như mình vì nó đôi khi có một số lỗi rất kì lạ nên mình tìm thử lỗi bypass nó.<br>
-- Sau quá trình search thì mình thấy có slide này khá hữu ích [LINK1](https://hydrasky.com/network-security/php-string-comparison-vulnerabilities/) [LINK2](https://www.owasp.org/images/6/6b/PHPMagicTricks-TypeJuggling.pdf)

Cụ thể: Nếu bạn nhìn kỹ MAC đang là dạng `String`, có thể trong source code đang dùng hàm stcmp hoặc == để so sánh. Một ví dụ nhỏ:
```php
    TRUE: “0000” == int(0)
    TRUE: “0e12” == int(0)
    TRUE: “1abc” == int(1)
    TRUE: “0abc” == int(0)
    TRUE: “abc” == int(0)       --> LỖI XUẤT PHÁT CHỖ NÀY NÈ MẤY BẠN
--------------------------------------------------------------------
    "7a5c2...45dsd" == int(7)
    "68f66...8dsdw" == int(68)
    "092dcs...54de3" == int(92)
    --> Có thể đoán và pass được hash_mac dựa vào số đầu
```
Giải thích đơn giải đây là lỗi so sánh giữ String và Int. Với trường hợp bài này, thì các bạn nhìn thấy `MAC` trong json là kiểu `String` áp dụng thay đổi MAC bằng `0` kiểu Int thôi 
```php
{"User":"saddean","Admin":"True","MAC":0}
//output basecode64: eyJVc2VyIjoic2FkZGVhbiIsIkFkbWluIjoiVHJ1ZSIsIk1BQyI6MH0=
```
Tiến hành request lên bằng session mới hoii, kết quả thu được flag
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Grammar5.jpg" class="img-responsive">





---
<a name="4"></a>
# 4.Lernaean [by Arrexel]
> **Description** : Your target is not very good with computers. Try and guess their password to see if they may be hiding anything! 

Mới vô chall thì mình nghĩ là `sqlinjection` để bypass auth, sau một hồi test thì bị cuốn vô injection cả tiếng mãi ko ra 🤣😂 Bình tĩnh view-source thì thấy vài câu nói có vẻ là hint `Please do not try to guess my password!`. Brute-force thôi, recommend sử dụng seclist top 1000 là đủ rồi. [LINK](https://github.com/danielmiessler/SecLists/blob/master/Passwords/darkweb2017-top1000.txt) --> chờ đợi ra pass thôi.<br>
Nhập pass và 💣:<br>
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Lernaean1.jpg" class="img-responsive">
<br>
Ez , tắt javascript trên browser đi thôi :D <br>
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/Lernaean2.jpg" class="img-responsive">

---
<a name="5"></a>
# 5.Cartographer [by Arrexel]
> **Description** : Some underground hackers are developing a new command and control server. Can you break in and see what they are up to? 

Lại là đăng nhập 👀<br>
Mới zô phang thử sqlinjection ai ngờ được luôn 🍌🍌
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/carto1.jpg" class="img-responsive">
- **Payload:** `username=admin%27+union+select+1--+-&password=1`
Chall này thư giãn hơn so với cái trước, nhìn vô đoán luôn đc
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/carto2.jpg" class="img-responsive">
Chuyển `Home` thành `flag` là có được flag luôn
<img src="https://raw.githubusercontent.com/saddean/blogs/master/static/img/hackthebox/carto3.jpg" class="img-responsive">