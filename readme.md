# Gradle Script

## Setup guide for android library module

In root project's `build.gradle`, before first using any `rootProject.extensions` variable, add the following block:

```
// Find all .properties file in script folder and import them into rootProject.extensions.
def propertiesFiles = fileTree("$rootDir/script").filter {
    it.isFile() && it.name.endsWith(".properties")
}.files.absolutePath
propertiesFiles.each {
    println("Loading properties from $it")
    def temp = new Properties()
    file(it).withInputStream { temp.load(it) }
    temp.each { k, v -> rootProject.extensions.add(k, v) }
}
```


In library module's `build.gradle`, add the following lines at the end.

```
apply from: "$rootDir/script/pom-optional.gradle"
apply from: "$rootDir/script/dokka-android.gradle"
apply from: "$rootDir/script/publish-android.gradle"
```

## Setup guide for java/kotlin module

In `build.gradle`, before first using any `rootProject.extensions` variable, add the following block:

```
// Find all .properties file in script folder and import them into rootProject.extensions.
def propertiesFiles = fileTree("$rootDir/script").filter {
    it.isFile() && it.name.endsWith(".properties")
}.files.absolutePath
propertiesFiles.each {
    println("Loading properties from $it")
    def temp = new Properties()
    file(it).withInputStream { temp.load(it) }
    temp.each { k, v -> rootProject.extensions.add(k, v) }
}
```


add the following lines at the end of `build.gradle`

```
apply from: "$rootDir/script/pom-optional.gradle"
apply from: "$rootDir/script/dokka.gradle"
apply from: "$rootDir/script/publish.gradle"
```

