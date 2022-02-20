# Jenkins & Groovy

[Groovy Syntax](http://groovy-lang.org/syntax.html)
[Groovy Language Documentation](https://docs.groovy-lang.org/next/html/documentation/)
[Groovy Tutorial](https://www.tutorialspoint.com/groovy/index.htm)

Jenkins configuration file is called `Jenkinsfile`.

## Example variables

```Groovy
String someText = 'SOME_TEXT'
def emptyList = []                          // def can be used to avoid using type
def complexList = [1, 2.1, [3, 4], 'text']  // heterogeneous list
def nullObject = null
Object someObject = load 'SOME_PATH/SOME_FILE.groovy'
final Map someMap = [
    someBool: true,
    someString: 'SOME_TEXT'
]
```

### Strings

A [string](https://docs.groovy-lang.org/next/html/documentation/#all-strings) can be represented in several ways:

1. 'Single-quoted'
2. '''Triple-single-quoted''' - Doesn't support interpolation, may span multiple lines
3. "Double-quoted" - Supports string interpolation via `${}` or just `$` but for dotted.expressions.only.

### Basics

```Groovy
def items = [1, 2]
for (item in items) {
    try {
        if (expression) {
            // some code ...
        } else {
            // some other code ...
        }
    } catch (e) {
        // handle ...
    }
}
```

## Imports

```Groovy
// Example library import
@Library('SOME_LIBRARY')

// Example class import
import NAMESPACE.CLASSNAME
```

## Running a Shell command

[Jenkins sh command](https://www.jenkins.io/doc/pipeline/steps/workflow-durable-task-step/#sh-shell-script)

Example:

```Groovy
String shout(String command) {
    return sh(script: command, returnStdout: true)?.trim()
}
```

## Environment variables

- Suffix `/env-vars.html` to your Jenkins instance to see available environment variables
- Environment variables are read/write via the `env` object.

## Stages

Stages correspond to visual columns in Jenkins. Long workflows should be broken into multiple stages.

Example:

```Groovy
stage('Environment Summary') {
    sh 'git --version'
    sh 'node --version'
    sh 'npm --version'
    sh 'yarn --version'
    sh 'env | sort'
}
stage('Checkout') {
    checkout scm
}
```

## Timing Blocks Manually

```Groovy
void someFunction() {
    long startTimeInMillis = System.currentTimeMillis()
    // some code here ...
    long elapsed = System.currentTimeMillis() - startTimeInMillis
    echo "Elapsed time: ${elapsed}"
}
```

## Authenticated Blocks

Using username and password:

```Groovy
withCredentials([usernamePassword(
    credentialsId: 'SOME_CREDENTIALS_ID',
    usernameVariable: 'SOME_USER_VARIABLE',
    passwordVariable: 'SOME_TOKEN_VARIABLE')]) {
        // In this block $SOME_USER_VARIABLE and $SOME_TOKEN_VARIABLE are available
    }
```

Using access token:

```Groovy
withCredentials([string(
        credentialsId: 'SOME_CREDENTIALS_ID',
        variable: 'SOME_ACCESS_TOKEN'
    )]) {
        // In this block $SOME_ACCESS_TOKEN is available
    }
```

## Groovy VSCode Extensions

- [code-groovy](https://marketplace.visualstudio.com/items?itemName=marlon407.code-groovy)
- [Groovy Lint, Format and Fix](https://marketplace.visualstudio.com/items?itemName=NicolasVuillamy.vscode-groovy-lint)
