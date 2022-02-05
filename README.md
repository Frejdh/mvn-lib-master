# Master pom for my libraries
[Search for my public github libraries here](https://github.com/search?q=Frejdh%2Fmvn-lib-).

## Releases
Go here https://github.com/Frejdh/mvn-lib-master/releases

## Adding this as your parent pom
Either use this [pom.xml](https://github.com/Frejdh/mvn-lib-master/blob/master/inherited-pom-example.xml) file as a base, 
or add these lines to your `pom.xml` file:
```
<parent>
    <groupId>com.frejdh</groupId>
    <artifactId>master-pom</artifactId>
    <version>2.0.0</version>
</parent>

<repositories> <!-- Required in order to resolve this package -->
    <repository>
        <id>library-master-pom</id>
        <url>https://raw.github.com/Frejdh/mvn-lib-master/releases/</url>
    </repository>
</repositories>
```

### Deployment to github
A part of the parent pom is pre-defined properties that enables easy releases to your github repository. 
An artifact (non-fat version) and a branch can be automatically created upon `mvn clean deploy`. However, in order to set this up, some 
properties needs to be set along with a plugin, please add the following to your child pom:
```
<properties> 
    <github.repository.owner>github-owner-of-repository</github.repository.owner>
    <github.repository.name>example-repository-name</github.repository.name>
<properties>
```
Also add the following plugin (no adjustments required):
```
<plugin> <!-- Optional. Push artifact and files to github upon mvn deploy -->
    <inherited>false</inherited>
    <groupId>com.github.github</groupId>
    <artifactId>site-maven-plugin</artifactId>
    <version>0.11</version>

    <executions> <!-- run site-maven-plugin's 'site' target as part of the build's normal 'deploy' phase -->
        <execution> <!-- Package and push .jar file as a release, available for direct download on github -->
            <id>github-site-to-artifact</id>
            <goals>
                <goal>site</goal>
            </goals>
            <phase>deploy</phase>
            <configuration>
                <message>Maven artifact for ${project.version}</message> <!-- Git commit message -->
                <noJekyll>true</noJekyll><!-- Disable webpage processing -->
                <outputDirectory>${project.build.directory}/${github.deploy.branch}</outputDirectory> <!-- Matches distribution management repository url above -->
                <branch>${github.ref.release.jar}/${project.version}</branch> <!-- Remote branch name (maven repository) -->
                <includes>
                    <include>**/*</include>
                </includes>
                <repositoryOwner>${github.repository.owner}</repositoryOwner> <!-- Organization or username  -->
                <repositoryName>${github.repository.name}</repositoryName> <!-- Github repo name -->
            </configuration>
        </execution>

        <execution> <!-- Upload files to a specific branch used as a maven repository -->
            <id>github-site-to-branch</id>
            <goals>
                <goal>site</goal>
            </goals>
            <phase>deploy</phase>
            <configuration>
                <message>Maven artifact for ${project.version}</message> <!-- Git commit message -->
                <noJekyll>true</noJekyll><!-- Disable webpage processing -->
                <outputDirectory>${project.build.directory}/${github.deploy.branch}</outputDirectory> <!-- Matches distribution management repository url above -->
                <branch>${github.ref.release.branch}/${github.deploy.branch}</branch> <!-- Remote branch name (maven repository) -->
                <includes>
                    <include>**/*</include>
                </includes>
                <repositoryOwner>${github.repository.owner}</repositoryOwner> <!-- Organization or username  -->
                <repositoryName>${github.repository.name}</repositoryName> <!-- Github repo name -->
            </configuration>
        </execution>
    </executions>
</plugin>
```
Simply type `mvn clean deploy` in order to deploy to the repository's `mvn-repo` branch. <br>

#### Github authorization for deployment
In order to deploy anything, a couple of requisites needs to be fullfilled (once per computer).
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
