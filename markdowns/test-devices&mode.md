You can set specific devices that will receive test ad content to evaluate and check integration. All your apps can use the test device and you can operate switch to control the display of test ads at any time.
## Test Devices
To use this feature, follow these steps:
### 1.Go to 'Developer Center' and select 'Integration Testing'
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618726584411-fb50f698-6a28-4cd7-91b3-3e1cf5f0095b.png#clientId=u1555ff49-08e2-4&from=paste&height=606&id=ucb241d78&margin=%5Bobject%20Object%5D&originHeight=1212&originWidth=3828&originalType=binary&size=305925&status=done&style=none&taskId=u67eb3f16-9698-4ec8-9464-d4f957610d5&width=1914)
### 2.Click '+Add' button to add a new device
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618726767074-7dbd3dfe-fb2f-489b-ae76-0ece9976de47.png#clientId=u1555ff49-08e2-4&from=paste&height=527&id=ubd46c393&margin=%5Bobject%20Object%5D&originHeight=1054&originWidth=3310&originalType=binary&size=173063&status=done&style=none&taskId=uda1ad6e2-f0f0-42e8-ae93-d81a6d309e1&width=1655)
### 3.Enter Name and Device ID(IDFA for iOS or GAID for Android)
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618727376047-6bba4e80-06dd-4eef-94e4-f93b1dabe211.png#clientId=u1555ff49-08e2-4&from=paste&height=377&id=ub217f1b5&margin=%5Bobject%20Object%5D&originHeight=754&originWidth=1386&originalType=binary&size=52893&status=done&style=none&taskId=ufc598844-9b25-42ad-ac65-378c0638575&width=693)
If you are not sure how to fill in IDFA/GAID please refer [here](https://www.yuque.com/docs/share/d5c0e34a-e03e-4db7-917c-816dbbce37c8?# 《How to get IDFA/GAID》). TODO


### 4.Once you've successfully added a test device, you will see it on the under list and the Test Mode will set to ON status by default.
![](https://cdn.nlark.com/yuque/0/2021/png/319925/1618727436808-1e2a8ea3-3b96-48e6-8bb7-51f8ea0b9342.png#clientId=u1555ff49-08e2-4&from=paste&height=560&id=u06a8f8b3&margin=%5Bobject%20Object%5D&originHeight=1120&originWidth=3250&originalType=binary&size=187443&status=done&style=none&taskId=u0f8ea719-6824-4c9d-a9fd-bcbf1b006c8&width=1625)
## Test Mode
Test mode is a kind of status management for test devices.When the test mode is ON state witch means the test device can receive test ads.you can toggle the state any time.


Once you toggle the state it will take some time(about 10 mins),then you need rebot your app to accept the new state.


About the Test Ads you can read [this](https://www.yuque.com/docs/share/d5c0e34a-e03e-4db7-917c-816dbbce37c8?# 《How to get IDFA/GAID》). TODO add the link to Test Ads
### Relationship about Test ads/Test mode/Store status
✅ Test ads will show
❌ Test ads will not show
| **Store Status** | **Test Mode ON** | **Test Mode OFF** |
| --- | --- | --- |
| live | ✅ | ❌ |
| non-live | ✅ | ✅ |

You can also check the logs from the init method to confirm whether the device is a test device(
**Test Device**) and whether receive test ads(**Test Ad**). For details please read [this](https://www.yuque.com/docs/share/bee06de2-078b-4bcb-835c-395fb7aee5dc?# 《Init Log Helper》).TODO add the link to Init log helper
