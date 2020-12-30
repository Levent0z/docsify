# Heroku

[Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)

## Heroku CLI Auto-Completion

To use the Heroku CLI's autocomplete, there are 2 options:

1. Via homebrew's shell completion:
    1. Follow homebrew's [install instructions](https://docs.brew.sh/Shell-Completion)
        NOTE: For zsh, as the instructions mention, be sure `compinit` is autoloaded and called, either explicitly or via a framework like `oh-my-zsh`.
    2. Then run
        ```sh
        $ heroku autocomplete --refresh-cache
        ```

2. Use our standalone setup. Run and follow the install steps:
    ```sh
    $ heroku autocomplete
    ```

Result:
```
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d

zsh completions have been installed to:
  /usr/local/share/zsh/site-functions
```

## Create a new app
```sh
heroku create --app <give_your_app_a_name>
```

## SSO Login
```sh
heroku login --sso
```

## Auth Tokens

https://help.heroku.com/PBGP6IDE/how-should-i-generate-an-api-key-that-allows-me-to-use-the-heroku-platform-api

```sh
heroku auth:token
```

## Add Neo4j Graph DB
```sh
heroku addons:create graphenedb:dev-free
```

## Add conguration
```sh
heroku config:add YOUR_KEY="YOUR_VALUE"
```

## Deploy the app to Heroku
```sh
git push heroku master
```

## Check deployment
```sh
heroku logs -t
```