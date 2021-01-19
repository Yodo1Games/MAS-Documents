# Android Manifest Merging Errors

## Unity 2020
No special setup required

## Unity 2019

<center class="half">
    <img src="./../resource/manifest-merging-errors-queries-1.png" width="200"/><img src="./../resource/manifest-merging-errors-queries-2.png" width="200"/>
</center>

* Find `File -> Build Setting -> Player Settings -> Publishing Settings -> Build` as shown above in figure 1 and select the options indicated by the arrow
* Open the `baseProjectTemplate.gradle` file in the `Assets/Plugins/Android/` directory and change `gradle android` version, e.g. 3.4.3
* Change the version of Gradle used by Unity to match the plugin version modified above, as shown in figure 2
* Click `Assets -> External Dependency Manager -> Android Resolver -> Force Resolve`


## Unity 2018

<center class="half">
    <img src="./../resource/manifest-merging-errors-queries-3.png" width="200"/><img src="./../resource/manifest-merging-errors-queries-4.png" width="200"/>
</center>

* Find`File -> Build Setting -> Player Settings -> Publishing Settings -> Build` as shown above in figure 1 and select the options indicated by the arrow
* Open the `mainTemplate.gradle` file in the `Assets/Plugins/Android/` directory and change `gradle android` version, e.g. 3.4.3
* Change the version of Gradle used by Unity to match the plugin version modified above, as shown in figure 2
* Click `Assets -> External Dependency Manager -> Android Resolver -> Force Resolve`

## Unity 2017

<center class="half">
    <img src="./../resource/manifest-merging-errors-queries-5.png" width="200"/>
</center>

* Find`File -> Build Setting -> Player Settings -> Publishing Settings -> Build` as shown above and select the options indicated by the arrow
* Open the `mainTemplate.gradle` file in the `Assets/Plugins/Android/` directory and chenge `gradle android` version, e.g. 3.4.3，
* Add the following information to the `mainTemplate.gradle` file

    ```
    multiDexEnabled true
    ```
    ```
    compileOptions {

        sourceCompatibility JavaVersion.VERSION_1_8

        targetCompatibility JavaVersion.VERSION_1_8

    }
    ```
 * Click `Assets -> External Dependency Manager -> Android Resolver -> Force Resolve`
