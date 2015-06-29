#How to use the maven plugin?

You can easily verify under maven that the new binary your a creating are still backward compatible compare to a reference version. In order to enable the checking you can get our maven checker plugin to run during the verify stage of a maven build:

```
<project>

  ...
  <build>
    <plugins>
      ...
      <plugin>
        <groupId>com.googlecode.japi-checker</groupId>
        <artifactId>japi-checker-maven-plugin</artifactId>
        <version>0.1.4</version> <!-- The check is still in development at the moment so snapshot is the only way to get it. -->
        <configuration>
            <reference>
                <!-- Replace here with the reference artifact of your project. -->
                <groupId>com.mydomain</groupId>
                <artifactId>my-artifact</artifactId> 
                <version>1.0.0</version>
            </reference>
            <rules>
                <rule>com.googlecode.japi.checker.rules.AllRules</rule>
            </rules>
          </configuration>
          <executions>
            <execution>
              <id>check-bc</id> <!-- this is used for inheritance merges -->
              <phase>verify</phase> <!-- bind to the packaging phase -->
              <goals>
                <goal>check</goal>
              </goals>
            </execution>
          </executions>
      </plugin>
      ....
    </plugins>
  </build>
  ...
</project>
```

You can run the verification with all rules by using the "com.googlecode.japi.checker.rules.AllRules" rule, or define which check you want to enable individually.


For a live demo of the plugin feel free to check out the [demo](http://code.google.com/p/japi-checker/source/checkout?repo=demo) repository and run maven:

```
MacBookPro:japi-checker.demo wbernard$ mvn verify 
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building Unnamed - com.googlecode.japi-checker:demo:jar:0.1.0-SNAPSHOT
[INFO]    task-segment: [verify]
[INFO] ------------------------------------------------------------------------
[INFO] [resources:resources {execution: default-resources}]
[WARNING] Using platform encoding (MacRoman actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /Users/wbernard/development/workspace/japi-checker.demo/src/main/resources
[INFO] [compiler:compile {execution: default-compile}]
[INFO] Nothing to compile - all classes are up to date
[INFO] [resources:testResources {execution: default-testResources}]
[WARNING] Using platform encoding (MacRoman actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /Users/wbernard/development/workspace/japi-checker.demo/src/test/resources
[INFO] [compiler:testCompile {execution: default-testCompile}]
[INFO] No sources to compile
[INFO] [surefire:test {execution: default-test}]
[INFO] No tests to run.
[INFO] [jar:jar {execution: default-jar}]
[INFO] Building jar: /Users/wbernard/development/workspace/japi-checker.demo/target/demo-0.1.0-SNAPSHOT.jar
[INFO] [japi-checker:check {execution: check-bc}]
[INFO] snapshot com.googlecode.japi-checker:reference-test-jar:0.1.0-SNAPSHOT: checking for updates from oss-sonatype-snapshots
Downloading: https://oss.sonatype.org/content/repositories/snapshots/com/googlecode/japi-checker/reference-test-jar/0.1.0-SNAPSHOT/reference-test-jar-0.1.0-SNAPSHOT.jar
11K downloaded  (reference-test-jar-0.1.0-SNAPSHOT.jar)
[INFO] Checking backward compatibility of com.googlecode.japi-checker:demo:jar:0.1.0-SNAPSHOT against com.googlecode.japi-checker:reference-test-jar:jar:0.1.0-SNAPSHOT:compile
[ERROR] com/googlecode/japi/checker/tests/PublicClassToFinal.java: The class com/googlecode/japi/checker/tests/PublicClassToFinal has been made final, this breaks inheritance.
[ERROR] com/googlecode/japi/checker/tests/ClassToAbstract.java: The class com/googlecode/japi/checker/tests/ClassToAbstract has been made abstract.
[ERROR] com/googlecode/japi/checker/tests/CheckMethodAccess.java(20): The method publicToFinal has been made final, this now prevents overriding.
[ERROR] com/googlecode/japi/checker/tests/CheckMethodAccess.java(21): The method protectedToFinal has been made final, this now prevents overriding.
[ERROR] com/googlecode/japi/checker/tests/PublicClassToProtected.java: The visibility of the com/googlecode/japi/checker/tests/PublicClassToProtected class has been changed from PUBLIC to NO_SCOPE
[ERROR] com/googlecode/japi/checker/tests/PublicClassToProtected.java(18): The visibility of the <init> method has been changed from PUBLIC to NO_SCOPE
[ERROR] com/googlecode/japi/checker/tests/InnerClassRemoved.java: Public class com/googlecode/japi/checker/tests/InnerClassRemoved$ProtectedStaticInnerClass has been removed.
[ERROR] com/googlecode/japi/checker/tests/InnerClassRemoved.java: Public class com/googlecode/japi/checker/tests/InnerClassRemoved$PublicInnerClass has been removed.
[ERROR] com/googlecode/japi/checker/tests/CheckInheritanceChanges.java: com/googlecode/japi/checker/tests/CheckInheritanceChanges extends java/util/ArrayList and not java/util/Vector anymore.
[ERROR] com/googlecode/japi/checker/tests/CheckInheritanceChanges.java: com/googlecode/japi/checker/tests/CheckInheritanceChanges is not implementing java/io/Serializable anymore.
[ERROR] com/googlecode/japi/checker/tests/FieldTestCases.java: The field testChangeOfTypePublic has been modified from Ljava/lang/String; to Ljava/lang/Boolean;
[ERROR] com/googlecode/japi/checker/tests/FieldTestCases.java: The field testChangeOfTypeProtected has been modified from Ljava/lang/String; to Ljava/lang/Boolean;
[ERROR] com/googlecode/japi/checker/tests/FieldTestCases.java: The visibility of the testChangeOfScopeFromPublicToProtected field has been changed from PUBLIC to PROTECTED
[ERROR] com/googlecode/japi/checker/tests/FieldTestCases.java: The visibility of the testChangeOfScopeFromPublicToPrivate field has been changed from PUBLIC to PRIVATE
[WARNING] com/googlecode/japi/checker/tests/FieldTestCases.java: The visibility of the testChangeOfScopeFromProtectedToPublic field has been changed from PROTECTED to PUBLIC
[ERROR] com/googlecode/japi/checker/tests/FieldTestCases.java: The visibility of the testChangeOfScopeFromProtectedToPrivate field has been changed from PROTECTED to PRIVATE
[WARNING] com/googlecode/japi/checker/tests/FieldTestCases.java: The visibility of the testChangeOfScopeFromPrivateToProtected field has been changed from PRIVATE to PROTECTED
[WARNING] com/googlecode/japi/checker/tests/FieldTestCases.java: The visibility of the testChangeOfScopeFromPrivateToPublic field has been changed from PRIVATE to PUBLIC
[ERROR] com/googlecode/japi/checker/tests/FieldTestCases.java: The field testPublicChangeToStatic is now static.
[ERROR] com/googlecode/japi/checker/tests/FieldTestCases.java: The field testPublicChangeFromStatic is not static anymore.
[ERROR] com/googlecode/japi/checker/tests/FieldTestCases.java: The field testProtectedChangeToStatic is now static.
[ERROR] com/googlecode/japi/checker/tests/FieldTestCases.java: The field testProtectedChangeFromStatic is not static anymore.
[ERROR] com/googlecode/japi/checker/tests/CheckMethodException.java(22): publicAddedException is now throwing java/lang/Exception.
[ERROR] com/googlecode/japi/checker/tests/CheckMethodException.java(26): protectedAddedException is now throwing java/lang/Exception.
[ERROR] com/googlecode/japi/checker/tests/CheckMethodException.java(34): publicRemovedException is not throwing java/lang/Exception anymore.
[ERROR] com/googlecode/japi/checker/tests/CheckMethodException.java(38): protectedRemovedException is not throwing java/lang/Exception anymore.
[ERROR] com/googlecode/japi/checker/tests/RemovedClass.java: Public class com/googlecode/japi/checker/tests/RemovedClass has been removed.
[ERROR] com/googlecode/japi/checker/tests/CheckRemovedMethod.java: Could not find method publicMethodRemoved in newer version.
[ERROR] com/googlecode/japi/checker/tests/CheckRemovedMethod.java: Could not find method protectedMethodRemoved in newer version.
[ERROR] com/googlecode/japi/checker/tests/CheckRemovedMethod.java(28): publicMethodRemoved is not throwing java/lang/Exception anymore.
[ERROR] com/googlecode/japi/checker/tests/CheckRemovedMethod.java(28): publicMethodRemoved is now throwing java/io/IOException.
[ERROR] com/googlecode/japi/checker/tests/InnerClassRemoved.java: Public class com/googlecode/japi/checker/tests/InnerClassRemoved$PublicStaticInnerClass has been removed.
[ERROR] com/googlecode/japi/checker/tests/ClassToInterface.java: Could not find method <init> in newer version.
[ERROR] com/googlecode/japi/checker/tests/ClassToInterface.java: The class com/googlecode/japi/checker/tests/ClassToInterface has been made abstract.
[ERROR] com/googlecode/japi/checker/tests/ClassToInterface.java: The class has been change into an interface.
[ERROR] com/googlecode/japi/checker/tests/InnerClassRemoved.java: Public class com/googlecode/japi/checker/tests/InnerClassRemoved$ProtectedInnerClass has been removed.
[ERROR] You have 33 backward compatibility issues.
[INFO] ------------------------------------------------------------------------
[ERROR] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] You have 33 backward compatibility issues.
[INFO] ------------------------------------------------------------------------
[INFO] For more information, run Maven with the -e switch
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 6 seconds
[INFO] Finished at: Wed Aug 24 22:38:07 EEST 2011
[INFO] Final Memory: 12M/81M
[INFO] ------------------------------------------------------------------------
```