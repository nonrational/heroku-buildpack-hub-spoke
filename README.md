# Heroku Hub-And-Spoke Buildpack

A strategy for deploying monorepo one-app-per-audience Rails applications on Heroku.

Sample Application: https://github.com/nonrational/unibus

<img src='http://i.imgur.com/58wavHO.gif' width=300>

# Usage

1. Create some spoke rails applications and at least one hub engine for them all
  - See https://github.com/nonrational/unibus for an example layout
2. Create one Heroku application for every spoke app.
  - You'll probabaly end up with a pair per rails app e.g. `app-X-staging`/`app-X-production`
  - You can even use [pipelines](https://devcenter.heroku.com/articles/pipelines). Go nuts.
  - You cannot use review apps. :cry:
3. For each app, set:

    ```
    APP_BASE=<spoke-app-name>
    APP_DEPS=<engine-one> <engine-two>
    ENGINE_PATH=./.engines
    ```

4. Add this buildpack _before the Ruby buildpack_.

    ```
    heroku buildpacks:add -r <heroku-remote> --index 1 https://github.com/nonrational/heroku-buildpack-hub-spoke
    ```

5. :shipit:. And often.

## Author

- Alan Norton [@nonrational](https://github.com/nonrational)

### Giants

... _upon whose shoulders the author(s) stood_.

- Andrew Gwozdziewycz <apg@heroku.com>
- Cyril David <cyx@heroku.com>
- Lincoln Stoll <lstoll@heroku.com>
