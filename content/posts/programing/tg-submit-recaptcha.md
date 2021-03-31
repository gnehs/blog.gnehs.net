---
title: '發送 XHR 時驗證 reCAPTCHA'
date: Sun, 05 May 2019 04:08:28 +0000
draft: false
categories: ['js','web','node']
---

reCAPTCHA 是眾所皆知的工人 OCR 驗證系統，在 v3 中，直接由分數判斷是否是機器人，因此也不需要核取方塊了。

最近在幫 [Telegram 蒐集君](https://tg.gnehs.net) 寫提交工具，因為驗證碼很麻煩，自己也懶得打所以直接拿 reCAPTCHA 來用了，由於使用 XHR 提交資料，因此 reCAPTCHA 的部分需要稍稍改寫才能夠正常運作。

始步：在 reCAPTCHA 註冊新的網站
---------------------

要使用 reCAPTCHA，必須要先到 Google 註冊才能夠使用，以下是註冊流程。

註冊新網站：[](https://www.google.com/recaptcha/admin/create)[https://www.google.com/recaptcha/admin/create](https://www.google.com/recaptcha/admin/create)

標籤：填入自己方便記憶的名稱即可  
類型：選 v3  
網域：輸入自己要用的網域，如果你要在本地測試，可以再加上 localhost

![](https://i.imgur.com/LfFj8pL.png)

全部輸入完成後按下下方的「提交」即可

![](https://i.imgur.com/O5g0iGl.jpg)

註冊完成後，你會拿到兩串金鑰，請好好保存，其中密鑰不能給他人知道。

加入 reCAPTCHA 到前端頁面吧！
--------------------

把下面的程式碼貼到你的網頁中吧！別忘了將 reCAPTCHA\_site\_key 換成你的網站金鑰

```
<script src="https://www.google.com/recaptcha/api.js?render=reCAPTCHA_site_key"></script>

<script>
grecaptcha.ready(function() {
    grecaptcha.execute('reCAPTCHA_site_key', {action: 'homepage'}).then(token => {
       //這裡拿到的 token 要在 XHR 請求時也發給伺服器驗證
    });
});
</script>
```

![](https://i.imgur.com/BeJYwd8.png)

完成後，應該就能在網頁右下角看見 reCAPTCHA 的標誌了

完成後端驗證
------

發送請求的方式百百種，因為我的後端語言用 node.js 所以就拿 [request-promise](https://github.com/request/request-promise) 來送請求。  
_\*請自行修改程式碼以符合需求_

```
const rp = require("request-promise")
let result = await rp({
    method: 'post',
    uri: "https://www.google.com/recaptcha/api/siteverify",
    qs: {
        secret: reCAPTCHA_secret_key, //你的密鑰
        response: token //前端送來的 token
    },
    transform: x => JSON.parse(x)
})
// 驗證失敗
if (!result.success) return res.json(result)
```

提交工具也有在 GitHub 上開源，尼也可以參考其中的程式碼  
[](https://github.com/gnehs/tg-submit)[https://github.com/gnehs/tg-submit](https://github.com/gnehs/tg-submit)