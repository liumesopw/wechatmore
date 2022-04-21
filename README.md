大家都知道，正常情况下，电脑微信客户端只能打开一个微信，如果再次点击是没法打开第二个的。微信是怎么实现，禁止一个客户端打开多个微信的呢？
![image](https://user-images.githubusercontent.com/96330669/164345943-98a9da62-558a-45a2-bdf4-9af628fd41ae.png)
微信每次启动的时候，都调用：OpenMutexA(	)函数，微信有一个自己的互斥体名称，每次调用这个函数，如果函数返回真，则说明找到了，说明微信已经打开一个了。他就不让再打开第二个了。如果没找到，就打开一个新微信，就是这个原理实现的。
![image](https://user-images.githubusercontent.com/96330669/164345958-b1acd584-9cf9-4f2c-8a7f-4d286ec3e83c.png)
在OD中（如下图），用快捷键Ctrl+G ，弹出搜：CreateMuteW（微信是宽字符） ,搜索之后，下断点，
![image](https://user-images.githubusercontent.com/96330669/164345971-bfbc685e-2d6d-425f-b057-de6beef40d0c.png)
断点之后，找到该函数，其中有三个参数：一个是互斥体名称，一个是bool值，一个他写的null
![image](https://user-images.githubusercontent.com/96330669/164346016-9ef9ae4e-9fbb-43be-ade8-e9308041d23c.png)
然后用CE 找他他这个名称，把他的互斥体名称改掉，如下图：
![image](https://user-images.githubusercontent.com/96330669/164346056-594f7aff-042b-42ec-b69e-b535c232b35e.png)
改掉之后，在OD里面把断点取消，然后自动就启动了一个微信。然后在自己电脑上，再点击微信图标，打开，就又打开一个微信。这样就打开了两个微信，实现了多开。

目前已经实现了大部分功能，运行稳定，比如：发各种消息，接收各种消息，群管，下载文件，加好友，检测僵尸粉等等功能，可提供接口，方便二次开发，
Q：2645542961 欢迎技术交流。

![image](https://user-images.githubusercontent.com/96330669/164346147-9e9e22eb-b6b7-4d33-9e58-4069489a4179.png)
