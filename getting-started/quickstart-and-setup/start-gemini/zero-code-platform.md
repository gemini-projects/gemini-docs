# Zero Code Platform

You can build the standalone executable or download the desired version from GitHub. The only things to remember is to specify the `docker/dev/wd/` from the Gemini Repositor as the Java working directory. In this way you can use the already crafted `wd/application.properties`.

### **Executable**

Gemini is built on SpringBoot that provides out of the box all the task to create bootable or executable jar file with all dependencies. Or you can also download the latest version executables [here](https://github.com/gemini-projects/gemini/releases). 

```bash
# from gemini root - to build a standalone jar
gradle bootJar

# from gemini root - to build a standalone EXECUTABLE jar
gradle executableJar

cd gemini-postgresql/dist
```

### Run Gemini

Make sure that the executable is placed inside `docker/dev/wd/` to be sure that the root working directory contains all the crafted Spring application properties

```java
# for standalone (bootJar) you need to call java
java -jar ./gemini-postgresql-0.3.x-standalone.jar

# while for executable (executableJar) you can run it
# works on linux based machines - only some platform supported
# take a look at Spring documentation
./gemini-postgresql-0.3.x-executable.jar
```

{% hint style="info" %}
If you use the **application.properties** of _/docker/dev/wd_  directory you now have Gemini bound to port **8080.** 
{% endhint %}

{% hint style="success" %}
Now wait that Gemini auto-setup itself and once the logs prints **STARTED - GEMINI-WEBAPP CONTEXT** you are able to use Gemini as a zero code platform and define your rest entities with the Gemini DSL
{% endhint %}

Now you are ready, you can move here to define APIs and enjoy with Gemini.

{% page-ref page="../enjoy-with-dsl-and-rest.md" %}

