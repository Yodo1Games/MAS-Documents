# Known Issues Unity

#### 1. Error compiling aab file
Error information: `FileNotFoundException: Temp/gradleOut/launcher/build/utputs/budle/release/laucher.aab does not exist
`
<center class="half">
    <img src="./../resource/known-issues-unity-aaberror.png" width="400"/> 
</center>

The solution is : Added following code in defaultConfig of launcherTemplate (Unity 2019) or mainTemplate (Unity 2018) 

```
tasks.whenTaskAdded {

    task ->
        if (task.name.startsWith("bundle")) {


            def renameTaskName = "rename${task.name.capitalize()}Aab"
            def flavor = task.name.substring("bundle".length()).uncapitalize()
            tasks.create(renameTaskName, Copy) {
                def path = "${buildDir}/outputs/bundle/${flavor}/"
                from(path)
                include "launcher-release.aab"
                destinationDir file("${buildDir}/outputs/bundle/${flavor}/")
                rename "launcher-release.aab", "launcher.aab"
                include "gradleOut-release.aab"
                destinationDir file("${buildDir}/outputs/bundle/${flavor}/")
                rename "gradleOut-release.aab", "gradleOut.aab"
            }

            task.finalizedBy(renameTaskName)
        }
}
```

<center class="half">
    <img src="./../resource/known-issues-unity-aaberror-2.png" width="400"/> 
</center>