# Maven

## Installation

```sh
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

```sh
mvn jetty:run -Djetty.port=9877
```

## List all dependencies (including transitive dependencies)

```sh
mvn dependency:tree
```

## Versions

[Versions plugin](http://www.mojohaus.org/versions-maven-plugin/)

```sh
mvn versions:set -DnewVersion=MAJOR.MINOR.BUILD-SNAPSHOT
mvn versions:revert # To undo
mvn versions:commit
```

To increment the build version unconditionally:

```sh
mvn build-helper:parse-version versions:set -DnewVersion=\${parsedVersion.majorVersion}.\${parsedVersion.minorVersion}.\${parsedVersion.nextIncrementalVersion} versions:commit
```

## Mvn Arguments:

- `--strict-checksums`: Fail the build if checksums don’t match
- `--batch-mode prevents`: Maven from polluting the log with progress messages
- `--update-snapshots`: Forces a check for updated releases and snapshots on remote repositories

One can also "define" key-value pairs. For example

- `-Denforcer.skip=true`: Skips checks for the [maven-enforcer-plugin](https://maven.apache.org/enforcer-archives/enforcer-1.4/maven-enforcer-plugin/
