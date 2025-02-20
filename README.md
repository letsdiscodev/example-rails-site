# Example Disco Rails Site

This is an hello world project demonstrating Rails running on Disco.

## The basic Rails project

The Rails project itself has been created with

```bash
rails new hello
```

Then, we added the controller `app/controllers/welcome_controller.rb`.
And we added the route `/` in `config/routes.rb`.

## Making it work on Disco

### Fixing the generated Dockerfile

Running `rails new hello` created a `Dockerfile`. For some reason, trying to build an image using this file is broken. Maybe a Rails bug? In other words, running locally `docker build -t example-rails-site .` failed. To fix the issue, we added `libyaml-dev` to `apt-get install`. Search the `Dockerfile` for `libyaml-dev` to see where to add it.

### Adding disco.json

See `disco.json`. It's just specifying the `port` `80`, because the command at the end of the `Dockerfile` exposes the application on port `80`.

### SECRET_KEY_BASE env variable

You'll need to set the `SECRET_KEY_BASE` env variable in Disco for your project, using the value from `bin/rails credentials:edit`.
