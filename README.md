# mvn-lib-master
Master pom for my maven libraries

## My libraries
[Search for my public github libraries here](https://github.com/search?q=Frejdh%2Fmvn-lib-).

## Adding the dependency
Add this to your `pom.xml` file:
``` 
<dependency>
    <groupId>com.frejdh.util</groupId>
    <artifactId>library-master-pom</artifactId>
    <packaging>pom</packaging>
</dependency>

<repositories>
    <repository>
        <id>library-master-pom</id>
        <url>https://raw.githubusercontent.com/Frejdh/mvn-lib-master/master/</url>
    </repository>
</repositories>
```

## Releases
Go here https://github.com/Frejdh/mvn-lib-master/releases

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
