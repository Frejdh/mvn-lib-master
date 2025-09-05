[![Current Build](https://github.com/Frejdh/mvn-lib-master/actions/workflows/current-build.yml/badge.svg?branch=master)](https://github.com/Frejdh/mvn-lib-master/actions/workflows/current-build.yml)

# Master pom for my libraries
[Search for my public github libraries here](https://github.com/search?q=Frejdh%2Fmvn-lib-).

## Releases
Go here https://github.com/Frejdh/mvn-lib-master/releases

## Adding this as your parent pom
Either use this [pom.xml](https://github.com/Frejdh/mvn-lib-master/blob/master/inherited-pom-example.xml) file as a base, 
or add these lines to your `pom.xml` file:
```xml
<parent>
    <groupId>com.frejdh</groupId>
    <artifactId>master-pom</artifactId>
    <version>3.0.0-SNAPSHOT</version>
</parent>

<repositories> <!-- Required in order to resolve this package -->
    <repository>
        <id>frejdh</id>
        <url>https://raw.githubusercontent.com/Frejdh/releases/maven</url>
    </repository>
</repositories>
```

## Update dependencies
There are some plugins that can be used in order to detect dependency updates.

### Based on properties
List them using:
`mvn initialize -P list-property-updates`

Auto-update them using:
`mvn initialize -P update-properties`

### Based on the dependencies/plugins found
`mvn initialize -P list-all-updates`
