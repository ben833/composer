# composer
It's dangerous to go alone! Here's a reliable `docker-compose` to help you on your Backend adventures.

![zelda-nyan](http://i1.kym-cdn.com/photos/images/original/000/402/521/a01.png "something something")

## Setup

Composer leverages Docker with sugar, spice and everything that's nice.

Clone and install **[Pager's dotfiles][dotfiles]** (recommended) or [Docker for Mac][docker-mac].

> **NOTE**: if you're not using the `dotfiles` repo, you might want to install 
> the following for shell completion.

```bash
brew install docker-completion
```

## Running docker-compose

Once docker is up and running on your machine, you can start your dev environment by telling the composer to run the [`docker-compose.yml` file][compose-file]. Grab a cup of coffee and run the following:

```
docker-compose up
```

This will build new images for the RabbitMQ, MongoDB and Redis services and then each process in new containers. Keep in mind, the first time this is run could take a while however, subsequent builds run much quicker since Docker caches the results.

And that's it. Congratulations on getting your local env ready for some developing.

Please note that when you run a service locally, RABBIT_URL should be "amqp://localhost:5672/db".

### Running daemonized

If you don't want to block your io and you're not a big fan of Tmux, you can easily run a daemonized version of docker-compose via the `-d` flag:

```
docker-compose up -d

./run_tests
docker-compose stop
docker-compose rm -f
```

### Linking containers

`docker-compose` defaults to a `compose_default` bridged network on your system, in order to link to these containers you can:

 - add `--net=compose_default` to the `docker run` command (fresh container)
 - run `docker network connect compose_default my-container` (existing container)

See [this article][linking] for details.

## Running Kong

```bash
docker-compose -f kong.yaml up
```

Hit [http://localhost.me]() for the proxy,
[localhost:8001](http://localhost:8001) for the admin API.

[compose-file]: https://docs.docker.com/compose/compose-file/
[dotfiles]: https://github.com/pagerinc/dotfiles
[docker-mac]: https://www.docker.com/products/docker#/mac
[linking]: http://blog.csainty.com/2016/07/connecting-docker-containers.html
