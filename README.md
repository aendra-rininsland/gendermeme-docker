# Gendermeme Docker

This repo contains Dockerfiles for building the following images:

* [aendrew/corenlp][1]
* [aendrew/gendermeme-core][2]

## How to use

CoreNLP surfaces a webservice that is capable of receiving requests from
gendermeme-core. A docker-compose.yml file is provided to help orchestrate
development.

### aendrew/corenlp

This is an optimised version of the Dockerfile provided by [konradstrack/corenlp][3].
It gives 10GB memory to CoreNLP (CoreNLP eats RAM like candy) and exposes the port
via the `$PORT` environment variable:

```bash
$ docker run -e PORT=9292 aendrew/corenlp
```

### aendrew/gendermeme-core

This is a base image intended to be built from. It clones the gendermeme-core sources
to `/project/gendermeme` and installs dependencies:

```Dockerfile
FROM aendrew/gendermeme-core:latest

WORKDIR /project`

COPY . /project

CMD ["python2", "__main__.py"]
```

In this example, it assumes you've created the above Dockerfile in the project directory
where your server implementation is stored (referencing modules from "gendermeme-core").
It copies to the image at buildtime and runs `__main__.py` as the entrypoint.

I am in no way a Python dev so if there's a better way to organise the sources
than I've used, please [file an issue][issues].

[1]: https://hub.docker.com/r/aendrew/corenlp/
[2]: https://hub.docker.com/r/aendrew/gendermeme-core/
[3]: https://hub.docker.com/r/konradstrack/corenlp/~/dockerfile/
[issues]: https://github.com/aendrew/gendermeme-docker/issues
