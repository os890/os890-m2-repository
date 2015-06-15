# Usage in Maven 2 projects #

Details about the content of these repositories are available **[here](Repository_Overview.md)**

## Stable versions of os890 ##
```
<repositories>
  <repository>
    <id>googlecode.com</id>
    <url>http://os890-m2-repository.googlecode.com/svn/tags/os890</url>
  </repository>
</repositories>
```

## Stable versions of sandbox890 ##
```
<repositories>
  <repository>
    <id>googlecode.com</id>
    <url>http://os890-m2-repository.googlecode.com/svn/tags/sandbox890</url>
  </repository>
</repositories>
```

## Latest snapshots ##
```
<repositories>
  <repository>
    <id>googlecode.com</id>
    <url>http://os890-m2-repository.googlecode.com/svn/trunk/[os890|sandbox890]</url>
  </repository>
</repositories>
```

# Deployment #
## Local settings ##

~/.m2/settings.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<settings>
  <servers>
    <server>
      <id>googlecode</id>
      <username>my.username</username>
      <password>password</password>
    </server>
  </servers>
</settings>
```

## Settings within a pom.xml of ...890-projects ##

```
<project>
    <repositories>
        <repository>
            <id>jboss</id>
            <url>http://repository.jboss.com/maven2</url>
        </repository>
        <repository>
            <id>maven2-repository.dev.java.net</id>
            <name>Java.net Repository for Maven</name>
            <url>http://download.java.net/maven/2/</url>
        </repository>
    </repositories>

    <build>
        <plugins>
            <plugin>
                <!-- Set compile source at 1.5, since the target JSF impl is 1.2 -->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.5</source>
                    <target>1.5</target>
                    <optimize>false</optimize>
                </configuration>
            </plugin>
        </plugins>

        <extensions>
            <extension>
                <groupId>org.jvnet.wagon-svn</groupId>
                <artifactId>wagon-svn</artifactId>
                <version>1.8</version>
            </extension>
        </extensions>
    </build>

    <distributionManagement>
        <repository>
            <uniqueVersion>false</uniqueVersion>
            <id>googlecode.com</id>
            <url>svn:https://os890-m2-repository.googlecode.com/svn/[trunk|tags]/[os890|sandbox890]</url>
        </repository>
    </distributionManagement>
</project>
```

## Deploy ##
To deploy a project to the maven repository
```
mvn deploy
```