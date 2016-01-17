---
layout: post
title: '[Java] Gradle - Create Java Project'
date: 2014-11-05 03:18
comments: true
categories: 
---

1. `mkdir first`
2. `cd first`
3. `vim build.gradle`
4. add `apply plugin: 'java'` into build.gradle, then save file and leave.
5. `gradle build`, This will create directory `.gradle` and `build`:
<!--more-->
```
 ~/Desktop/Gradle/first -->gradle build
:compileJava UP-TO-DATE
:processResources UP-TO-DATE
:classes UP-TO-DATE
:jar
:assemble
:compileTestJava UP-TO-DATE
:processTestResources UP-TO-DATE
:testClasses UP-TO-DATE
:test UP-TO-DATE
:check UP-TO-DATE
:build

BUILD SUCCESSFUL

Total time: 3.712 secs
```

上面依序是編譯和打包專案時會做的 tasks，可以用 `gradle tasks` 來查看有哪些 task 可以指定，這裡因為我們指定到 build，所以就依序做到 build

```
 ~/Desktop/Gradle/first -->ll
total 8
drwxr-xr-x  5 veck  staff  170 Nov  5 03:15 .
drwxr-xr-x  6 veck  staff  204 Nov  5 03:13 ..
drwxr-xr-x  3 veck  staff  102 Nov  5 03:15 .gradle
drwxr-xr-x  4 veck  staff  136 Nov  5 03:15 build
-rw-r--r--  1 veck  staff   22 Nov  5 03:14 build.gradle
 ~/Desktop/Gradle/first -->tree
.
├── build
│   ├── libs
│   │   └── first.jar
│   └── tmp
│       └── jar
│           └── MANIFEST.MF
└── build.gradle
```

可以見到，gradle 會自動打包成 jar 檔和建立 MANIFEST.MF 檔，不過正常應該是，要先建立好 java 專案，根據[官方文件](http://www.gradle.org/docs/current/userguide/java_plugin.html#N12119)說明，gradle 預設你的 Java 專案結構長這樣:

```
├── build.gradle
└── src
    ├── main
    │   ├── java
    │   └── resources
    ├── sourceSet
    │   ├── java
    │   └── resource
    └── test
        ├── java
        └── resources
```

我先手動建立，Gradle 好像沒有自動化建立專案的功能(? 或是有工具？應該也可用 maven 去建立？)，建立好以後，我們在 `src/main/java` 下建立 `HelloWorld.java`，簡單的加入 HelloWorld 的程式碼，並且在 `build.gradle` 中加入 `apply plugin: 'java'`，最後的目錄結構會長這樣：

```
 ~/Desktop/Gradle/first -->tree
.
├── build.gradle
└── src
    ├── main
    │   ├── java
    │   │   └── HelloWorld.java
    │   └── resources
    ├── sourceSet
    │   ├── java
    │   └── resource
    └── test
        ├── java
        └── resources

10 directories, 2 files
```

接著在用 `gradle build`:

```
 ~/Desktop/Gradle/first -->gradle build
:compileJava
:processResources UP-TO-DATE
:classes
:jar
:assemble
:compileTestJava UP-TO-DATE
:processTestResources UP-TO-DATE
:testClasses UP-TO-DATE
:test UP-TO-DATE
:check UP-TO-DATE
:build

BUILD SUCCESSFUL

Total time: 4.572 secs 
 ~/Desktop/Gradle/first -->tree
.
├── build
│   ├── classes
│   │   └── main
│   │       └── HelloWorld.class
│   ├── dependency-cache
│   ├── libs
│   │   └── first.jar
│   └── tmp
│       ├── compileJava
│       └── jar
│           └── MANIFEST.MF
├── build.gradle
└── src
    ├── main
    │   ├── java
    │   │   └── HelloWorld.java
    │   └── resources
    ├── sourceSet
    │   ├── java
    │   └── resource
    └── test
        ├── java
        └── resources

18 directories, 5 files
```

但是這樣子還不能夠直接下 `java -jar first.jar` 來執行測試我們的程式，需要在 build.gradle 中加入：

```
jar {
    manifest {
        attributes 'Main-Class': 'HelloWorld'
    }
}
```

然後再 build 一次，最後進到 build/libs 中，就可以執行 `java -jar first.jar` 來執行程式了

``` 
~/Desktop/Gradle/first/build/libs -->java -jar first.jar
Hello World!!!
```

但是這樣很不方便，想要更自動化，可以向 maven 一樣在 pom.xml 中寫 <exec.mainClass>...</exec.mainClass> 的話，Gradle 也可以，只要在 build.gradle 中加入以下的 task：

```
task runJar(dependsOn:jar) << {
  javaexec { main="-jar"; args jar.archivePath } 
}
```

接著每次重新編譯完後，就可以值些輸入 `gradle runjar` 來執行編譯包裝後的 JAR 檔案了

![螢幕快照 2014-11-05 上午9.07.04.png](http://user-image.logdown.io/user/3330/blog/3407/post/241255/PuHqanGQ0GzHRo4zOQiw_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-11-05%20%E4%B8%8A%E5%8D%889.07.04.png)


Note: 在 build.gradle 中加入 `apply plugin: 'eclipse'` 可以產生 eclipse 的專案，可以加在 `apply plugin: 'java'` 後

References:

1. http://www.gradle.org/docs/current/userguide/tutorial_java_projects.html
2. http://www.gradle.org/docs/current/userguide/java_plugin.html#N12119
3. http://blog.denevell.org/gradle-run-jar-file.html