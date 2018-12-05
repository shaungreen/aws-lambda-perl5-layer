aws-lambda-perl5-layer
==

This repository provides the Perl5 layer for AWS Lambda with runtime API.

How to build a layer
--

```
$ make build-docker-container PERL_VERSION=x.x.x CONTAINER_TAG=x.x
$ make build CONTAINER_TAG=x.x
```

NOTE: `x.x.x` and `x.x` means perl runtime version (e.g. `5.28.1` and `5.28`). You can specify as you like.

Then this command stats to create a zip archive as `lambda-layer-perl-x.x.zip`.

--

Or you can use pre-built docker container:

```
$ make build CONTAINER_TAG=x.x DOCKER_HUB_ACCOUNT='moznion/'
```

Please refer to the following so that getting available containers: https://hub.docker.com/r/moznion/lambda-perl-layer-foundation/

How to use this layer
--

1. Register the built zip archive of layer as a layer.
2. Create a perl function
  - If you register the handler as `handler.handle`, you have to write code into `handler.pl` file and it must have `handle` subroutine
3. Enjoy :tada:

How to create a perl function
--

Please refer: [moznion/aws-lambda-perl5-layer-example](https://github.com/moznion/aws-lambda-perl5-layer-example)

An example is shown below (`handler.pl`):

```perl
#!perl

use strict;
use warnings;
use utf8;

sub handle {
    my ($payload) = @_;

    # do something
    ...

    # if you want to finish the execution as failed, please die

    # NOTE: must return hashref or arrayref
    return +{
        'msg' => 'OK',
        'this is' => 'example',
    };
}

1; # must return TRUE value here!
```

### How to build a Lambda function with package vendoring?

Please refer to the following: https://github.com/moznion/aws-lambda-perl5-layer-example/tree/master/simple

For Developers
--

### How to publish foundation docker container

```
$ make build-docker-container PERL_VERSION=x.x.x CONTAINER_TAG=x.x
$ make publish-docker-image CONTAINER_TAG=x.x DOCKER_ID_USER=xxx
```

### How to build foundation docker container without caching

```
$ make build-docker-container PERL_VERSION=x.x.x CONTAINER_TAG=x.x OPT='--no-cache'
```

TODO
--

- [ ] Publish a layer to AWS and provide ARN

See Also
--

- https://docs.aws.amazon.com/lambda/latest/dg/runtimes-custom.html

Authoer
--

moznion (<moznion@gmail.com>)

License
--

MIT

