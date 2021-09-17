Sample project for https://github.com/gradle/gradle/issues/18276

### Reproduce Steps
1. `git clone https://github.com/sify21/gradletest`
2. `mkdir /tmp/repo`, then edit `~/.m2/settings.xml`, uncomment`localRepository` and set it to `/tmp/repo`
3. `cd gradletest & mvn clean package` ->  maven build succeeds.
4. `./gradlew clean build` -> gradle build fails with this error:
```
   * What went wrong:
Execution failed for task ':compileJava'.
> Could not resolve all files for configuration ':compileClasspath'.
   > Could not find com.google.inject:guice:4.0.
     Searched in the following locations:
       - file:/tmp/repo/com/google/inject/guice/4.0/guice-4.0.pom
     If the artifact you are trying to retrieve can be found in the repository but without metadata in 'Maven POM' format, you need to adjust the 'metadataSources { ... }' of the repository declaration.
     Required by:
         project : > org.apache.maven:maven-core:3.5.0
```
5. simply create a fake jar file without classifier to fix: `touch /tmp/repo/com/google/inject/guice/4.0/guice-4.0.jar`, then run `./gradlew clean build` -> gradle build succeeds
