# Gradle 的安装并使用

[官网 Gradle 安装教程]( https://docs.gradle.org/current/userguide/installation.html )



## 一、安装

> windows 和 linux 的安装过程基本相同

1 下载二进制的 Gradle 压缩包

2 解压该压缩包

3 根据该压缩包路径配置以下环境变量：

+ GRADLE_HOME 将 gradle 的安装目录配置到环境变量中去
+ 配置 `%GRADLE_HOME%\bin` 配置到 `PATH` 变量中
+ (可选) 配置 `GRADLE_USER_HOME` 变量指定用户配置和缓存存放的目录，如果不配置默认为  `当前用户目录\.gradle`

4 运行下面的命令验证是否安装成功

```shell
gradle -v
```



## 二、一些实用的配置

### 1 设置远程下载仓库

全局设置：

在用户目录下的 `.gradle` 文件夹中，新建或修改 `init.gradle` 配置文件，添加以下内容：

```groovy
allprojects {
    repositories {
        def ALIYUN_REPOSITORY_URL = 'http://maven.aliyun.com/nexus/content/groups/public'
        def ALIYUN_JCENTER_URL = 'http://maven.aliyun.com/nexus/content/repositories/jcenter'
        all { ArtifactRepository repo ->
            if(repo instanceof MavenArtifactRepository){
                def url = repo.url.toString()
                if (url.startsWith('https://repo1.maven.org/maven2')) {
                    project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_REPOSITORY_URL."
                    remove repo
                }
                if (url.startsWith('https://jcenter.bintray.com/')) {
                    project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_JCENTER_URL."
                    remove repo
                }
            }
        }
        maven {
            url ALIYUN_REPOSITORY_URL
            url ALIYUN_JCENTER_URL
        }
    }
}
```

单个项目设置：

在该项目的 `build.gradle` 文件中，添加以下内容：

```groovy
buildscript {
    repositories {
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
                maven{ url 'http://maven.aliyun.com/nexus/content/repositories/jcenter'}
    }
    
    dependencies {
        classpath 'com.android.tools.build:gradle:2.2.3'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }        
}

allprojects {
    repositories {
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
        maven{ url 'http://maven.aliyun.com/nexus/content/repositories/jcenter'}
    }
}

```

