# Maven Plugins

- [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/index.html)
- [help:evlauate](https://maven.apache.org/plugins/maven-help-plugin/evaluate-mojo.html)
  Evaluates Maven expression given by the user in interactive mode
- [frontend-maven-plugin]()
- [Maven AntRun Plugin](https://maven.apache.org/plugins/maven-antrun-plugin/)
- [Properties Maven Plugin](https://www.mojohaus.org/properties-maven-plugin/)
  It makes available key=value pairs defined in `.properties` files as if they're defined in the `<properties>` section of `pom.xml`.

# Maven Properties

- [Maven Properties Guide](https://cwiki.apache.org/confluence/display/MAVEN/Maven+Properties+Guide)
- [Maven 3.2.1 Release Notes](https://maven.apache.org/docs/3.2.1/release-notes.html)
  - revision
  - changelist
  - sha1
- [Maven Model Builder](https://maven.apache.org/components/ref/3-LATEST/maven-model-builder/index.html)

# Maven Command line arguments

- `-Dkey=value` where key and value are generic, exmples
  - `enforcer.skip=true`
  - `maven.test.skip=true`
- `--batch-mode`
- `--fail-at-end`
- `--strict--checksums`
- `--update-snapshots`
