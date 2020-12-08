# Gradle Build Tools

Gradle is an alternative to Ant and Maven build tools for Java.

Has Conventions, but also configurable


2 DSLs (Groovy or Kotlin based) - as opposed to XML (DSL = "Domain Specific Language)
Supports Multi-Project builds
It can build Java, Kotlin and C++





---
## Check Version and available tasks
```sh
$ ./gradlew --version # Shows versions for Gradle, Kotlin, Groovy etc.
$ ./gradlew tasks     # Shows list of tasks
$ ./gradlew tasks --all  # Shows detailed list of tasks
```

brew install gradle

curl -s "https://get.sdkman.io" | bash


## build.gradle
```groovy
task 'hello' {
    doLast {
        println "Hello Gradle"
    }
}
```
```sh
gradle hello
```

```kotlin
tasks.register("hello") {
    doLast {
        println "Hello Gradle"
    }
}
```

gradle.properties
```gradle
# Project-wide Gradle settings.
# IDE (e.g. Android Studio) users:
# Gradle settings configured through the IDE *will override*
# any settings specified in this file.
# For more details on how to configure your build environment visit
# http://www.gradle.org/docs/current/userguide/build_environment.html
```


~/.gradle/gradle.properties


