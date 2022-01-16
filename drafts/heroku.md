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

## Get/Set environment variables

```sh
heroku config
heroku config:set TIMES=2
heroku config:add YOUR_KEY="YOUR_VALUE"
```

## Auth Tokens

https://help.heroku.com/PBGP6IDE/how-should-i-generate-an-api-key-that-allows-me-to-use-the-heroku-platform-api

```sh
heroku auth:token
```

## Add-ons

```sh
heroku addons:create graphenedb:dev-free            # Neo4j Graph DB
heroku addons:create heroku-postgresql:hobby-dev    # Postgres
```

## Deploy the app to Heroku

```sh
git push heroku master
```

## Check deployment

```sh
heroku logs -t
```

## Run locally?

```sh
heroku local # This will respect the .env file
```

## Example `.env` file:

Remember to add an entry for the file to `.gitignore`

```
DATABASE_URL='postgres://localhost/foobar'
HTTP_TIMEOUT=10000
```

## Example `procfile` with two projects

[Worker processes with Heroku by Example](https://codeburst.io/worker-processes-with-heroku-by-example-49863913008f)

```
web: node packages/web/dist/server.js
worker: node packages/worker/dist/worker.js
```

## Enable Heroku app?

```sh
heroku ps:scale web=1
heroku ps:scale worker=1
```

## Browse the web app

```sh
heroku open
```

## Using a monorepo to deploy multiple Heroku projects

https://github.com/lstoll/heroku-buildpack-monorepo

## Get running processes / view dyno configuration

```sh
heroku ps
```

## App.json

```json
{
  //...
  },
  "formation": {
    "web": {
      "quantity": 1
    },
    "worker": {
      "quantity": 1
    }
  },
  //...
}
```

## Various commands

```sh
heroku ps:scale worker=1
```

## Postgres

Assuming that you have Postgres installed locally, use the heroku pg:psql command to connect to the remote database, create a table and insert a row:

```sh
> heroku pg:psql
psql (11.5)
SSL connection (cipher: DHE-RSA-AES256-SHA, bits: 256)
Type "help" for help.
=> create table test_table (id integer, name text);
CREATE TABLE
=> insert into test_table values (1, 'hello database');
INSERT 0 1
=> \q
```

## Heroku-specific Build Scripts

In `package.json`:

```json
"scripts": {
  "heroku-prebuild": "echo This runs before Heroku installs dependencies.",
  "heroku-postbuild": "echo This runs after Heroku installs dependencies, but before Heroku prunes and caches dependencies.",
  "heroku-cleanup": "echo This runs after Heroku prunes and caches dependencies."
}
```
