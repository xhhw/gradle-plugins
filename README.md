## Configuration
As per [spring-framework/build.gradle][1]:
```groovy
buildscript {
    repositories {
        maven { url 'http://repo.springsource.org/plugins-release' }
    }
    dependencies {
        classpath 'org.springframework.build.gradle:docbook-reference-plugin:0.2.0'
    }
}

// ...

configure(rootproject) {
    apply plugin: 'docbook-reference'

    reference {
        sourceDir = file('src/reference/docbook')
        pdfFilename = 'spring-framework-reference.pdf'
    }

    task docsZip(type: Zip) {
        group = 'Distribution'
        baseName = 'spring-framework'
        classifier = 'docs'

        // ...

        from (reference) {
            into 'reference'
        }
    }

    // ...

    artifacts {
        archives docsZip
    }
}
```
See contents of the [spring-framework/src/reference/docbook][2] for details.


## Usage
```
$ gradle referenceHtmlMulti
$ gradle referenceHtmlSingle
$ gradle referencePdf
$ gradle reference  # all of the above
$ gradle build      # depends on `reference` because of "artifacts" arrangement
```

## Output
```
$ open build/reference/html/index.html
$ open build/reference/htmlsingle/index.html
$ open build/reference/pdf/spring-framework-reference.pdf
```

## Maintenance
See [How to release the docbook reference plugin][3] wiki page.

[1]: https://github.com/SpringSource/spring-framework/blob/master/build.gradle
[2]: https://github.com/SpringSource/spring-framework/tree/master/src/reference/docbook
[3]: https://github.com/SpringSource/gradle-plugins/wiki/How-to-release-the-docbook-reference-plugin
