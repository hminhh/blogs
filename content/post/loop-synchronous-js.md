---
title: "[JS] Loop Synchronous JS - Tạo Vòng lặp đồng bộ trong JS"
date: 2019-01-24T18:26:14+07:00
draft: false
tags: [javascript]
---
---
# 1.Vòng lặp bất đồng bộ

Đây là vấn đề muôn thưở cho ai code JS, đặt vấn đề với trường hợp sau đây:

<iframe height="500px" width="100%" src="https://repl.it/@saddean/CaseLoopAsyn?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Trường hợp này, vòng lặp sẽ được chạy `setTimeOut` với time ngẫu nhiên và tất nhiên kết quả trả về không theo thứ tự của vòng lặp(0-9) 😊. Đây là một cách để JS xử lí nhanh hơn các ngôn ngữ khác, tuy nhiên ở một số trường hợp bạn cần dữ liệu được `loop` theo một cách đồng bộ thì lại khá bất tiện. Đây là một số cách mình tìm hiểu để giải quyết vấn đề này.


# 2.For kết hợp với Promise.resolve()

```javascript
    for (let i = 0, p = Promise.resolve(); i < 10; i++) {
        p = p.then(_ => new Promise(resolve =>
            setTimeout(function () {
                console.log(i);
                resolve();
            }, Math.random() * 1000)
        ));
    }
```

# 3.Async/Await

```javascript
    (async function loop() {
        for (let i = 0; i < 10; i++) {
            await new Promise(resolve => setTimeout(resolve, Math.random() * 1000));
            console.log(i);
        }
    })();
```

```javascript
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));

    (async function loop() {
        for (let i = 0; i < 10; i++) {
            await delay(Math.random() * 1000);
            console.log(i);
        }
    })();
```


