## IDFA for iOS device
Currently, Apple does not surface the IDFA by default on iOS devices.Here are some ways to help you get IDFA.
First you need to confirm the 'Tracking' feature is ON.
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618734255370-34df92e0-0135-4207-bde8-11b01b834efe.png#clientId=u16b26564-ef35-4&from=paste&height=629&id=u74412d4a&margin=%5Bobject%20Object%5D&originHeight=1258&originWidth=976&originalType=binary&size=465149&status=done&style=none&taskId=u6bb74c65-7f79-466f-baa3-e84034a80b6&width=488)
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618734327680-7c3d879c-0120-4435-b093-88780162a5c3.png#clientId=u16b26564-ef35-4&from=paste&height=289&id=u2b82a8f3&margin=%5Bobject%20Object%5D&originHeight=578&originWidth=986&originalType=binary&size=175157&status=done&style=none&taskId=u5e220cd6-3dfc-465f-9aba-3f1a4a9c569&width=493)
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618734340741-d29d0831-4223-4e21-80d1-ba60b07d313f.png#clientId=u16b26564-ef35-4&from=paste&height=337&id=u5cda7e40&margin=%5Bobject%20Object%5D&originHeight=674&originWidth=988&originalType=binary&size=332229&status=done&style=none&taskId=u2baf6e3e-ecf6-4fdc-925a-00f4fa43f90&width=494)
### MAS Init Log Helper
The MAS SDK provides an easy way to verify that you’ve successfully integrated.then you can find IDFA through the output. please read [this](https://www.yuque.com/docs/share/bee06de2-078b-4bcb-835c-395fb7aee5dc?# 《Init Log Helper》). TODO
### Programmatically
please read [this](https://developer.apple.com/documentation/adsupport/asidentifiermanager).
### IDFA issues on iPhone 12
We noticed that on some iPhone 12 devices the tracking feature is not able to be turned on, resulting in the acquired IDFA will be **000000-0000-0000-0000-000000000000** This is an iOS system bug.
You can still turn it on with the following settings, but this is more dangerous and it is recommended that you back up your device first.
1.Settings
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618734554667-b40c7319-a8dc-459e-80d9-a3bd553f68d7.png#clientId=u16b26564-ef35-4&from=paste&height=806&id=u0ce4a766&margin=%5Bobject%20Object%5D&originHeight=1612&originWidth=978&originalType=binary&size=324453&status=done&style=none&taskId=u2d8a83e3-82d3-4c68-abf4-c69aef60a0d&width=489)
2.Reset
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618734593968-22dbabb2-993c-4b6d-85fb-edbd0730e615.png#clientId=u16b26564-ef35-4&from=paste&height=425&id=ufea0bd4f&margin=%5Bobject%20Object%5D&originHeight=850&originWidth=978&originalType=binary&size=333299&status=done&style=none&taskId=ub1d7c61c-152a-4f1a-b531-86202495394&width=489)
Once reset completed you can turns the 'Tracking' ON.
## GAID for Android devices
### MAS Init Log Helper
please read [this](https://www.yuque.com/nicky-eqdct/fv2rkc/ed3dda).
### Android Device Setting
On Android devices, you can find your GAID in your device settings. Navigate to Settings, click Google, and then Ads
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618734829406-88ecc1da-7eab-4454-aef6-52e3f71a8067.png#clientId=u16b26564-ef35-4&from=paste&height=608&id=u8ca4587c&margin=%5Bobject%20Object%5D&originHeight=1216&originWidth=1052&originalType=binary&size=278655&status=done&style=none&taskId=u8ec47405-9ced-404e-845e-8eddf8ecd7c&width=526)
### Programmatically
please read [this](https://developer.android.com/training/articles/ad-id).
