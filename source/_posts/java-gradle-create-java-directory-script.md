---
layout: post
title: '[Java] Gradle - Create Java Directory Script'
date: 2014-11-05 09:41
comments: true
categories: 
---
參考良葛格的簡報：http://www.codedata.com.tw/java/groovy-gradle-abc/

在 build.gradle 中可以加入這個 task:
```
task "create-dirs" << {
    sourceSets*.java.srcDirs*.each { it.mkdirs() }
    sourceSets*.resources.srcDirs*.each { it.mkdirs() }
}
```
然後就可以用 `gradle create-dirs` 自動化建立專案目錄
```
~/Desktop/gedo -->gradle create-dirs
:create-dirs

BUILD SUCCESSFUL

Total time: 4.926 secs
~/Desktop/gedo -->tree
.
├── build.gradle
└── src
    ├── main
    │   ├── java
    │   └── resources
    └── test
        ├── java
        └── resources

7 directories, 1 file
```

額外參考討論：https://issues.gradle.org/browse/GRADLE-1289