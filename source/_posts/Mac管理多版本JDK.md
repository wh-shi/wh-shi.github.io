---
title: Mac管理多版本JDK
tags:
  - Mac
  - JDK
  - jenv
date: 2017-11-21 17:17:06
categories: JDK
---

### 系统环境
macOS High Sierra  
版本 10.13.1

### JDK版本
``` shell
➜  ~ /usr/libexec/java_home -V
Matching Java Virtual Machines (2):
    1.8.0_112, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_112.jdk/Contents/Home
    1.7.0_80, x86_64:	"Java SE 7"	/Library/Java/JavaVirtualMachines/jdk1.7.0_80.jdk/Contents/Home

/Library/Java/JavaVirtualMachines/jdk1.8.0_112.jdk/Contents/Home
➜  ~
```

### 方法1
编辑.bash_profile文件  `vi ~/.bash_profile`
``` shell
# 设置 JDK 7
export JAVA_7_HOME=`/usr/libexec/java_home -v 1.7`
# 设置 JDK 8（如果有多个版本，需指定具体的版本号）
export JAVA_8_HOME=`/usr/libexec/java_home -v 1.8`

#默认JDK 7
export JAVA_HOME=$JAVA_7_HOME

#alias命令动态切换JDK版本
alias jdk7="export JAVA_HOME=$JAVA_7_HOME"
alias jdk8="export JAVA_HOME=$JAVA_8_HOME"
```
执行`source ~/.bash_profile` 保存

验证
``` shell
➜  ~ java -version
java version "1.7.0_80"
Java(TM) SE Runtime Environment (build 1.7.0_80-b15)
Java HotSpot(TM) 64-Bit Server VM (build 24.80-b11, mixed mode)
➜  ~ jdk8
➜  ~ java -version
java version "1.8.0_112"
Java(TM) SE Runtime Environment (build 1.8.0_112-b16)
Java HotSpot(TM) 64-Bit Server VM (build 25.112-b16, mixed mode)
➜  ~
```
再次验证  
准备Hello.java
``` java
public class Hello {
    public static void main(String[] args) {
        // jdk8写法
        new Thread(() -> test1()).start();
    }

    private static void test1(){
        System.out.println("ok");
    }
}
```
先切换jdk7，然后编译Hello.java  
``` shell
➜  test jdk7
➜  test javac Hello.java
Hello.java:3: 错误: 非法的表达式开始
        new Thread(() -> test1()).start();
                    ^
Hello.java:3: 错误: 非法的表达式开始
        new Thread(() -> test1()).start();
                       ^
2 个错误
➜  test
```
现在切回jdk8并重新编译
``` shell
➜  test jdk8
➜  test javac Hello.java
➜  test java Hello
ok
➜  test
```


### 方法2
`使用jenv` [参考文章](http://chessman-126-com.iteye.com/blog/2162466)

### 后续
尽管这俩种方法都能切换jdk版本，但只是在当前shell中，如果重新开一个则会失效，始终是默认的jdk版本  
解决方法：  
Intellij Idea -> File -> Project Struction  
{% asset_img image/Intellij_idea控制jdk版本.png example dissolve start page %}
