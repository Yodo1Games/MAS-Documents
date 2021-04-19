We strongly recommend testing your latest app version on a test device before submitting the final version to the app store.


Here are some tips.
## Use The Init Log Helper
> 💡**Before you start**
> The Init Log Helper can only be used with 4.1.0+.

When your integration is complete, check the log print of the call to the init method. The log format is as follows.
```shell
MAS SDK Version: Android-4.1.0
AppKey: xxxx
Bundle ID: com.yourbundle.id
Admob ID: ca-app-pub-xxx~xxx
Init Status: Init successfully (AppKey & Bundle ID & Admob ID Verified)
GAID is: xxxx-xxx-xxx-xxx
Test Device: On
Test Ad: On
```
For the meaning of each of these items you can read [this](https://www.yuque.com/docs/share/bee06de2-078b-4bcb-835c-395fb7aee5dc?# 《Init Log Helper》). TODO add the link to Init Log Helper


The most important thing is to check the **Init Status** item.If it prints Init failed, then you should pay attention to the ErrorCode printed. TODO add the link to ErrorCode
## Use Test ads to review ads feature
MAS Test Ads for apps facilitates the ad implementation and ad content testing process for developers.
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618732729083-ab5d3178-7969-4c84-9818-b1d4202448f9.png#clientId=u7937ca6e-f908-4&from=paste&height=687&id=uaf842f5d&margin=%5Bobject%20Object%5D&originHeight=1374&originWidth=3828&originalType=binary&size=327442&status=done&style=none&taskId=u5064178b-51dc-4a8c-96e7-a21e77b049d&width=1914)
For live app you can test the ads feature by adding test devices.For details, please see [here](https://www.yuque.com/docs/share/7ac840c3-35fb-44cc-9fd8-785fc9c0bd09?# 《Test Devices & Test Mode》). TODO
> When you add an **non-live app** to your MAS account, it will remain in test ads until you set them to live.

