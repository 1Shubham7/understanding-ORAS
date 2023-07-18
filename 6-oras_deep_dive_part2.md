# Manifest Config

we have already discusssed how image manifest looks like. To push a file with the custom manifest config file `config.json`, you can run:

`oras push --config config.json localhost:5000/hello:latest hi.txt` The media type of the config is set to the default value `application/vnd.unknown.config.v1+json`. To push a file with custom media type `application/vnd.oras.config.v1+json` ->

```oras push --config config.json:application/vnd.oras.config.v1+json localhost:5000/hello:latest hi.txt```

## Docker behavior for Manifest Config

if we do `oras push ...` and `docker pull ...` we don't get what we expect.
the config used by oras is not real config, so can't be pulled by docker as expected.

> the manifest config is not used by oras and is not worth pulling

