---
title: "[JS] Shallow Copy & Deep Copy Trong JavaScript"
date: 2018-12-30T21:11:04+07:00
draft: false
tags: [javascript]
---
---
# 1.Giới thiệu
> Javascript luôn có những điều kì lạ so với các ngôn ngữ khác. `Object` là kiểu đối tượng của JS và ai học JS cũng phải làm việc rất nhiều với nó,
`Object` có thể chứa các thuộc tính, hàm ,... Hầu hết tất cả các đối tượng trong JS đều có kiểu là `Object` (`Array` là một ví dụ).

Tuy nhiên khi thao tác với `Object` về việc copy thì gặp phải một vài vấn đề rắc rối , đó là `shallow copy` và `deep copy`.Những sử dụng các toán tử gán (`=`), nó không tạo ra 
một object mới mà nó chỉ trỏ đến tham chiếu đến địa chỉ cho biến gán....Hmm nói nghe khó hiểu nhỉ:
```javascript
    let hacker ={
        OS : "Kali Linux",
        Skill : "Rip Facebook",
        AGE : 10
    }

 // lúc này hackerClone chỉ trỏ đến địa chỉ của hacker chứ không tạo ra một object mới
    let hackerClone = hacker;       

    hackerClone.AGE = 100;

    console.log(hacker.AGE)                 //100
    console.log(hackerClone.AGE)            //100

```

# 2.Một vài cách copy object trong JS
**1. Loop**

Cách này thuần cơ là tự viết hàm để có thể sao chép object ban đầu thành một object mới
```javascript
    function clone(obj) {
        if (null == obj || "object" != typeof obj) return obj;
        var copy = obj.constructor();
        for (var attr in obj) {
            if (obj.hasOwnProperty(attr)) copy[attr] = obj[attr];
        }
        return copy;
    }
```
**2. Object.assign**

Bạn có thể xem chi tiết về `Object.asign` tại [đây](https://developer.mozilla.org/vi/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
```javascript
    let hacker ={
        OS : "Kali Linux",
        Skill : "Rip Facebook",
        AGE : 10
    }

    let hackerClone = Object.assign({},hacker)  

    hackerClone.AGE = 100;

    console.log(hacker.AGE)                 //10
    console.log(hackerClone.AGE)            //100
```

**3. Spread operator**

ES6 là một thứ tuyệt vời mà JS mang lại , ES6 hỗ trợ "Toán tử 3 chấm"  để copy đơn giản nhất có thể
```javascript
    let hacker ={
        OS : "Kali Linux",
        Skill : "Rip Facebook",
        AGE : 10
    }

    let hackerClone = {...hacker}    

    hackerClone.AGE = 100;

    console.log(hacker.AGE)                 //10
    console.log(hackerClone.AGE)            //100
```

# 3.Vấn đề bắt đầu 🌋
Vậy shallow copy , deep copy là gì ?????? Mình sẽ bắt đầu bằng một ví dụ sau :
```javascript
    let hacker ={
        OS : "Kali Linux",
        Skill : "Rip Facebook",
        AGE : 10,
		GirlFriends : {
			girl1 : "Cháu gái nắng",
			girl2 : "Em gái mưa"
		}
    }

    let hackerClone = {...hacker}
    // let hackerClone = Object.assigin({},hacker)

    hackerClone.GirlFriends.girl1 = "Bà Còng";

    console.log(hacker.GirlFriends.girl1)                 //Bà Còng
    console.log(hackerClone.GirlFriends.girl1)            //Bà Còng
```
Ủa chuyện gì xảy ra ở đây vậy , sao hai Object trên lại cùng thay đổi giá trị 😂.Giải thích đơn giản thì đây chính là bẫy đặt ra 
trong shallow copy.Tuy đối tượng `hackerClone` đã ko còn tham chiếu đến `hacker` , tuy nhiên khi có 1 đối tượng lồng trong 1 đối tượng
khác thì đối tượng con này vẫn tham chiếu đến Object ban đầu. Cụ thể `hackerClone.GirlFriends` đang tham chiếu đến `hacker.GirlFriends` 👏👏
Và đây chính là `shallow copy`

# 4.Giải quyết vấn đề
Sử dụng `Deep Copy`, đây là hình thức copy giá trị biến đến vùng nhớ khác và cắt đứt mọi quan hệ với biến cũ.Trong JS sử dụng thủ thuật

>``JSON.parse(JSON.stringify(object));``

```javascript
    let hacker ={
        OS : "Kali Linux",
        Skill : "Rip Facebook",
        AGE : 10,
		GirlFriends : {
			girl1 : "Cháu gái nắng",
			girl2 : "Em gái mưa",
			haveGirl : true
		}
    }

    let hackerClone = JSON.parse(JSON.stringify(hacker))

    hackerClone.GirlFriends.girl1 = "Bà Còng";

    console.log(hacker.GirlFriends.girl1)                 //Cháu gái nắng
    console.log(hackerClone.GirlFriends.girl1)            //Bà Còng
```
Tuy nhiên =))) sử dụng cách này thì bạn không thể copy những `method` của thuộc tính trong Object 🤣🤣 Ôi JavaScript thật tuyệt zờiiiiiiiii
Vậy `"WHAT IS GOOD WAY TO COPY OBJECT IN JAVASCRIPT??"`. Vấn đề này khá ngặt nghèo, tuy nhiên mình sẽ để lại link cho các bạn tham khảo, mình sẽ trình bày 
ở các bài viết tiếp theo
[https://stackoverflow.com/questions/728360/how-do-i-correctly-clone-a-javascript-object?answertab=active#tab-top](https://stackoverflow.com/questions/728360/how-do-i-correctly-clone-a-javascript-object?answertab=active#tab-top)





