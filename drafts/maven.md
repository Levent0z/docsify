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