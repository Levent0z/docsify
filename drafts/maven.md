# Maven

## Installation

```bash
brew install maven
```

[Download from Apache](https://archive.apache.org/dist/maven/maven-3/)

## Settings

`~/.m2/settings.xml`

## Lifeycle Phases

- validate
- initialize
- generate-sources
- process-sources
- generate-resources
- process-resources
- compile
- process-classes
- generate-test-sources
- process-test-sources
- generate-test-resources
- process-test-resources
- test-compile
- process-test-classes
- test
- prepare-package
- package
- pre-integration-test
- integration-test
- post-integration-test
- verify
- install
- deploy
- pre-clean
- clean
- post-clean
- pre-site
- site
- post-site
- site-deploy

## Serve with Jetty

```bash
mvn jetty:run -Djetty.port=9877
```

## List all dependencies (including transitive dependencies)

```bash
mvn dependency:tree
```

## Versions

[Baeldung Article](https://www.baeldung.com/maven-dependency-latest-version)

[Versions plugin](http://www.mojohaus.org/versions-maven-plugin/)

```bash
mvn versions:set -DnewVersion=MAJOR.MINOR.BUILD-SNAPSHOT
mvn versions:revert # To undo
mvn versions:commit
```

To increment the build version unconditionally:

```bash
mvn build-helper:parse-version versions:set -DnewVersion=\${parsedVersion.majorVersion}.\${parsedVersion.minorVersion}.\${parsedVersion.nextIncrementalVersion} versions:commit
```

## Mvn Arguments:

- `--strict-checksums`: Fail the build if checksums don’t match
- `--batch-mode prevents`: Maven from polluting the log with progress messages
- `--update-snapshots`: Forces a check for updated releases and snapshots on remote repositories

One can also "define" key-value pairs. For example

- `-Denforcer.skip=true`: Skips checks for the [maven-enforcer-plugin](https://maven.apache.org/enforcer-archives/enforcer-1.4/maven-enforcer-plugin/

## Example POM [Model Interpolation](https://maven.apache.org/ref/3.8.4/maven-model-builder/#Model_Interpolation) Strings

- `${project.basedir}`: root folder of the module/project. Note: Also see multiModuleProjectDirectory.
- `${project.build.directory}`: target folder
- `${project.build.outputDirectory}`: target/classes folder
- `${project.build.testOutputDirectory}`: target/test-classes folder
- `${project.build.sourceDirectory}`: src/main/java folder
- `${project.build.testSourceDirectory}`: src/test/java folder
- `${maven.multiModuleProjectDirectory}`: root folder of a multi-pom project
- `${project.version}`: Useful in multi-modules to get inherited version
- `${env.VARNAME}`: Can reference environment variables
- `${settings.VARNAME}`: Can reference properties in settings XML
