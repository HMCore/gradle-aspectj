We forked this to adjust it to work again because the fork of an abandoned project is now also abandoned :/
-----------------------------------------------------------------------------------------------------------

Gradle AspectJ plugin
=====================

Usage
-----

Either build this project yourself, and include the `.jar` in your buildscript dependencies,
or use our Maven repo. The plugin is applied using `apply plugin: 'aspectj'`. 
The version of AspectJ to use can be defined using either `ext.aspectjVersion`, 
or the `aspectj` extension's `version` attribute. 
If the AspectJ version is not set, version `1.8.12` is used as the default.

Something like this:

```groovy
buildscript {
    repositories {
        mavenCentral()
    }

    dependencies {
        classpath "net.uberfoo.gradle:gradle-aspectj:2.2"
    }
}

repositories {
    mavenCentral()
}

apply plugin: 'aspectj'

// Optionally
project.ext {
    aspectjVersion = '1.9.0'
}
// Or
aspectj {
    version = '1.9.0'
}
```

Note that version 2.0+ is only compatible with Gradle 4+. Use version 1.6 for earlier Gradle versions.

Use the `aspectpath`, `ajInpath`, `testAspectpath` and `testAjInpath` to specify external aspects or external code to weave:

```groovy
dependencies {
    aspectpath "org.springframework:spring-aspects:${springVersion}"
}
```

By default, `xlint: ignore` is used. Specify a different value for the `xlint` variable of the `compileAspect` or
`compileTestAspect` task to show AspectJ warnings:

```groovy
compileAspect {
    xlint = 'warning'
}
```

It is possible to specify a different value for the `maxmem` variable of the `compileAspect` or
`compileTestAspect` task to increase or decrease the max heap size:

```groovy
compileAspect {
    maxmem = '1024m'
}
```

To specify additional [ajc arguments](http://www.eclipse.org/aspectj/doc/released/devguide/antTasks-iajc.html#antTasks-iajc-options), you can use ```additionalAjcArgs```. If ```xlint``` or ```maxmem``` are also specified in ```additionalAjcArgs```, the values in ```additionalAjcArgs``` will take precedence. For example, to preserve debug symbols,

```groovy
compileAspect {
     additionalAjcArgs = ['debug' : '', 'X' : 'noInline', 'preserveAllLocals' : '']
}
```
To specify additional Java compiler arguments, you can use ```additionalCompilerArgs```,

```groovy
compileAspect {
    additionalCompilerArgs = ['--add-modules', 'java.xml.bind,java.io']
}
```

Development
-----------

This project was forked from an abandoned project.  The project is now maintained by us.

License
-------

The project is licensed under the Apache 2.0 license. Most/all of the code
originated from the Spring Security project and was created by Luke Taylor and
Rob Winch. See `LICENSE` for details.
