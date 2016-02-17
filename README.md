# MyKotlin

###1、Kotlin介绍
     [Kotlin](https://kotlinlang.org/)
     Kotlin是一门基于JVM的编程语言，它正成长为Android开发中用于替代Java语言的继承者。Java是世界上使用最多的编程语言之一，当其他编程语言为更加便于开发者使用而不断进化时，Java并没有像预期那样及时跟进。

　　Java缺失的很多特性在最新的修订版中逐渐覆盖到了，但Android开发者暂时还没能够使用它们。这就使得类似Kotlin这样的语言有了用武之地了：在旧的开发环境中使用现代语言的特性。

　　Kotlin是什么？

　　Kotlin是由JetBrains创建的基于JVM的编程语言，IntelliJ正是JetBrains的杰作，而Android Studio是基于IntelliJ修改而来的。Kotlin是一门包含很多函数式编程思想的面向对象编程语言。

　　Kotlin生来就是为了弥补Java缺失的现代语言的特性，并极大的简化了代码，使得开发者可以编写尽量少的样板代码。
###2、配置工程
 新建一个Project "MyKotlin"
 在项目的build.gradle上添加kotlin版本号

```
// Top-level build file where you can add configuration options common to all sub-projects/modules.
ext.kotlin_version = "1.0.0-rc-1036"
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:1.3.0'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

```
在module中的build.gradle添加kotlin的依赖
```
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}
```
再添加对android的支持
```
apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'
apply plugin: 'kotlin-android-extensions'
```
再添加java的编译路径，在main下创建kotlin目录 并在gradle文件写上
完整的build.gradle如下
```
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}

apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'
apply plugin: 'kotlin-android-extensions'

android {
    compileSdkVersion 23
    buildToolsVersion "23.0.1"

    defaultConfig {
        applicationId "com.example.mykotlin"
        minSdkVersion 14
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }

    sourceSets {
        main.java.srcDirs += 'src/main/kotlin'
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
}

```
代码如图所示
![这里写图片描述](http://img.blog.csdn.net/20160217164808819)
###3、代码转换
可以选择MainActivity 然后选择code-->>Convert Java File to Kotlin File ...
然后将生成的文件kt 剪切到kotlin目录下。
kt 代码如下
```
package com.example.mykotlin

import android.support.v7.app.AppCompatActivity
import android.os.Bundle
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        tv.text = "Hello MyKotlin"
        tv.textSize = 20.0f
    }
}


```

最终运行如图所示：
<img src="http://img.blog.csdn.net/20160217165421721" width = "500" height = "880" alt="运行效果" align=center />

###4、例子下载
[点击查看](https://github.com/cayden/MyKotlin)
