TDD Exercise
---------------------

1. Create a new maven project based on the quickstart archetype
`mvn archetype:generate -DgroupId=net.spe -DartifactId=mvn-test -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

And add the following to pom.xml
```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

```

2. Run `mvn test` to make sure all tests succeed

3. Your client gave you a new requirement and you need to implement a function that given a number i returns the smallest prime number equal or larger than i.

4. Implement a stub method `nextPrime` in `App.java`  and one or more tests of `nextPrime` with example combinations of input and output.

5. Run `mvn test` to check that your tests are indeed failing

6. Instead of working out the solution ourselves we are **standing on the shoulders of giants** and use a tested library. Add the following dependency to your pom.xml file
```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-math3</artifactId>
    <version>3.6.1</version>
</dependency>
```

7. In `App.java` import `org.apache.commons.math3.primes.Primes` and in `nextPrime` delegate to the function `Primes.nextPrime()`

8. Re-run the test and check that the test passes. 