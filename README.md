# Detectatron Unifi Connector

This companion Java application runs on any server running the Ubiquiti Unifi NVR software. It regularly polls the
MongoDB database used by the NVR software and when a video event occurs, exports the video and posts it up to the
Detectatron service for scoring and validation.


# Requirements

* Unifi Video controller 3.6.0+
* JDK 7 or later
* Network access to upstream Detectatron service



# Build & Execution

Development is done with IntelliJ, however any Gradle & Java compatible IDE should work.

Standard gradle build commands can be used to build and run the application:

    gradle bootRun
    
A standalone self-contained JAR executable can be built and run with:

    gradle bootRepackage
    LATEST=`find build -name '*.jar' | tail -n1`
    
    export UNIFI_API_KEY=foobar
    java -jar $LATEST


# Testing

We aim for 80%+ code coverage with unit and integration tests. The tests can be executed with:

    gradle test

If the tests fail, you can obtain additional information with the --info parameter. This can show errors such as missing configuration causing faults with the test suite.

    gradle test --info

Note that the tests require access to a function AWS account as a number of the tests take place against AWS service endpoints.

It is possible to bypass tests by adding -x test to your normal gradle commands, for example:

    gradle bootRun -x test

This of course is not recommended, but it can be useful if you need to separate the build task and the testing task (eg as part of a CI/CD workflow).
