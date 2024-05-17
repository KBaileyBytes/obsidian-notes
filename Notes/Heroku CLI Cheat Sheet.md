---
tags:
  - note
---
# `= this.file.name `
---

| Abbreviation             | Purpose                                                                | Parameters                              | Example                                                               |
| ------------------------ | ---------------------------------------------------------------------- | --------------------------------------- | --------------------------------------------------------------------- |
| `heroku login`           | Logs into your Heroku account                                          | N/A                                     | `heroku login`                                                        |
| `heroku create`          | Creates a new Heroku app                                               | N/A                                     | `heroku create`                                                       |
| `heroku apps`            | Lists all apps you have access to                                      | N/A                                     | `heroku apps`                                                         |
| `heroku logs`            | Displays logs for a specific app                                       | N/A                                     | `heroku logs --app <app-name>`                                        |
| `heroku ps`              | Lists dynos (containers) running in the app                            | N/A                                     | `heroku ps --app <app-name>`                                          |
| `heroku open`            | Opens the app in a web browser                                         | N/A                                     | `heroku open --app <app-name>`                                        |
| `git push heroku master` | Deploys the current branch to Heroku                                   | N/A                                     | `git push heroku master`                                              |
| `heroku config:set`      | Sets config vars (environment variables) for the app                   | `<key>=<value>`                         | `heroku config:set DATABASE_URL=postgres://user:password@host/dbname` |
| `heroku config`          | Displays config vars for the app                                       | N/A                                     | `heroku config --app <app-name>`                                      |
| `heroku addons`          | Lists all addons attached to the app                                   | N/A                                     | `heroku addons --app <app-name>`                                      |
| `heroku run`             | Runs a one-off command in the context of the app                       | `<command>`                             | `heroku run python manage.py migrate --app <app-name>`                |
| `heroku restart`         | Restarts the app's dynos                                               | N/A                                     | `heroku restart --app <app-name>`                                     |
| `heroku scale`           | Scales the number of dynos for a process type                          | `<process-type>=<quantity>`             | `heroku scale web=2 --app <app-name>`                                 |
| `heroku domains`         | Lists custom domains configured for the app                            | N/A                                     | `heroku domains --app <app-name>`                                     |
| `heroku certs:add`       | Adds SSL certificates to the app                                       | `<certificate-file> <private-key-file>` | `heroku certs:add server.crt server.key --app <app-name>`             |
| `heroku git:remote`      | Adds a Git remote for the app                                          | N/A                                     | `heroku git:remote -a <app-name>`                                     |
| `heroku pg:info`         | Displays information about the PostgreSQL database attached to the app | N/A                                     | `heroku pg:info --app <app-name>`                                     |


---
Created: March 19, 2024
Last Modified: `= this.file.mtime`
