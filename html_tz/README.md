# html通知
这个网站可以通过点击按钮发送通知。
</br>
发送通知是通过JavaScript实现的。同时，你也可以随便打开一个网站，按F12进入控制台输入以下代码也可以实现。
```javascript
notify()
function notify() {
    if (!("Notification" in window)) {
    alert("抱歉，此浏览器不支持桌面通知！");
    }
    Notification.requestPermission().then(function (result) {
    if (result === "denied") {
        console.log("用户拒绝");
        return;
    }
    if (result === "default") {
        console.log("用户未授权");
        return;
    }
    // 同意通知
    sendMesg();
    });
}

function sendMesg() {
    let notification = null;
    const title = "通知测试";
    const options = {
    dir: "auto", // 文字方向
    body: "制作者:haloged", // 通知主体
    data: {
        originUrl: `https://github.com/haloged`,
    },
    requireInteraction: true, // 不自动关闭通知
    image:
        "https://static.codemao.cn/coco/player/unstable/BkDRSFYcs.image/jpeg?hash=FqA1bpy-_GYbPGR4ERAo6RL1ciat",
    icon: "https://haloged.github.io/haloged1/logo001.ico", // 通知图标
    };
    notification = new Notification(title, options);
    //setTimeout(notification.close.bind(notification), 4000);
    notification.onclick = ({ currentTarget: { data } }) => {
    notification.close();
    window.focus();
    window.location.href = data.originUrl;
    };
}
```
