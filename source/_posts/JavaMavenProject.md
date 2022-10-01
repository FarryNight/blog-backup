---
title: JavaMavenProject
author: Farry
img: 
top: false
cover: true
tags: [java,development]
categories: [Bavk End]
reprintPolicy: cc_by
date: 2022-09-29 22:58:02
---
## Enviroment
set up java and maven (use command line)
attention kit tool version
setup java : java jdk , java se
java development kit , java standard edition
java -version 

### Maven
``` bash
mvn clean compile

mvn clean test

mvn clean package

mvn clean install
```
atention maven plugin may cause problem 
cheek https://maven.apache.org/plugins/maven-shade-plugin/
``` bash
<build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>3.3.0</version>
        <configuration>
          <!-- put your configurations here -->
        </configuration>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
</build>
```
https://maven.apache.org/plugins/maven-shade-plugin/

https://maven.apache.org/run.html

https://maven.apache.org/run-maven/index.html

https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html
###


### 


### 

