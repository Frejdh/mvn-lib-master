# Master pom for my libraries
[Search for my public github libraries here](https://github.com/search?q=Frejdh%2Fmvn-lib-).

## Releases
Go here https://github.com/Frejdh/mvn-lib-master/releases

## Adding this as your parent pom
Either use this [pom.xml](https://github.com/Frejdh/mvn-lib-master/blob/master/inherited-pom-example.xml) file as a base, 
or add these lines to your `pom.xml` file:
```
<dependencies> <!-- Required in order to use this library -->
    <dependency>
        <groupId>com.frejdh.util</groupId>
        <artifactId>library-master-pom</artifactId>
        <packaging>pom</packaging>
    </dependency>
</dependencies>

<repositories> <!-- Required in order to resolve this library -->
    <repository>
        <id>library-master-pom</id>
        <url>https://raw.githubusercontent.com/Frejdh/mvn-lib-master/master/</url>
    </repository>
</repositories>

<properties> <!-- Optional, but required for artifact deployment -->
    <github.repository.owner>github-owner-of-repository</github.repository.owner>
    <github.repository.name>example-repository-name</github.repository.name>
<properties>
```

## Deploying artifacts (dev only)
Simply type `mvn clean deploy` in order to deploy to the repository's `mvn-repo` branch. <br>
<strong>Note:</strong> In order to deploy anything, a couple of requisites needs to be fullfilled.
1. You need to have write access to the repository (<i>obviously</i>).
2. [A personal access token](https://github.com/settings/tokens) with both repository and user permissions (optional but highly recommended).
3. A name set on your [Github profile](https://github.com/settings/profile) (an error will occur otherwise).
4. Added the following fields to your `.m2/settings.xml` file:
```		
<server>
    <id>github</id>
    <username>[REPLACE. Your Github username]</username>
    <password>[REPLACE. Your personal access token or plain text password]</password>
</server>
```
