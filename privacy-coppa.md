# COPPA

## 1. What is COPPA?
COPPA is an American legal framework for protecting children's privacy. For details, check [this blog post](https://www.privo.com/blog/what-is-coppa). Both the App Store and Google Play have rules in place to make sure games comply with COPPA.

## 2. What are the App Store's rules?
If an app is designed specifically for children under 13, it must NOT include SDKs related to advertising. Please do not use MAS if your audience is children under 13.

## 3. What are Google Play's rules?
Developer submitting games and applications meant for children and or for a general audience (including children) under 13 MUST comply with Google Play's [Designed for Families](https://play.google.com/about/families/) policy. Otherwise, **your application will be disabled on Google Play**. 

## 4. COPPA Settings for MAS
>*Note*: If your game is only for audiences over 13, no action is needed to comply with COPPA.

**For apps meant only for children 13 and under, include the following code per platform:**

>**IMPORTANT! Please add the relevant code below BEFORE initializing the MAS SDK.**

**Unity**

```c#
Yodo1U3dMas.SetCOPPA(true);
```

**Android**

```java
Yodo1Mas.getInstance().setCOPPA(true);
```

**iOS**

```obj-c
[Yodo1Mas sharedInstance].isCOPPAAgeRestricted = Yes;
```

**For apps meant for all ages, including 13 and under, complete the following process:**

1) Create an Age Verification Pop-up to collect the user's age. Here are some examples:
<center class="half">
    <img src="../resource/privacy-coppa-sample-1.png" width="200"/><img src="../resource/privacy-coppa-sample-2.png" width="200"/><img src="../resource/privacy-coppa-sample-3.png" width="200"/>
</center>

2) Use the age to trigger one of the following methods in the MAS SDK:

If age is greater than 13
>IMPORTANT! Please add the relevant code below BEFORE initializing the MAS SDK.

**Unity**

```c#
Yodo1U3dMas.SetCOPPA(false)
```

**Android**

```java
Yodo1Mas.getInstance().setCOPPA(false);
```

**iOS**

```obj-c
[Yodo1Mas sharedInstance].isCOPPAAgeRestricted = NO;
```

If age is 13 or lower
>IMPORTANT! Please add the relevant code below BEFORE initializing the MAS SDK.

**Unity**

```c#
Yodo1U3dMas.SetCOPPA(true)
```

**Android**

```java
Yodo1Mas.getInstance().setCOPPA(true);
```

**iOS**

```obj-c
[Yodo1Mas sharedInstance].isCOPPAAgeRestricted = YES;
```

