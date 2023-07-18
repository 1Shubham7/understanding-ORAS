# Manifest Config

> the manifest config is not used by oras and is not worth pulling. However, it is still possible to push pullable config with the oras CLI by leveraging Manifest Annotations.

we have already discusssed how image manifest looks like. To push a file with the custom manifest config file `config.json`, you can run:

```oras push --config config.json localhost:5000/hello:latest hi.txt```

The media type of the config is set to the default value `application/vnd.unknown.config.v1+json`. To push a file with custom media type `application/vnd.oras.config.v1+json` ->

```oras push --config config.json:application/vnd.oras.config.v1+json localhost:5000/hello:latest hi.txt```

## Docker behavior for Manifest Config

if we do `oras push ...` and `docker pull ...` we don't get what we expect.
the config used by oras is not real config, so can't be pulled by docker as expected.

# Annotations

annotations refer to additional metadata that can be associated with container images or other artifacts.
check out https://github.com/opencontainers/image-spec/blob/main/annotations.md for rules etc.

## How to Make annotations

Users can make annotations to the manifest, the config, and individual files (i.e. layers) by the --annotation-file file option. The annotations file is a JSON file with the following format:

```
{
  "<filename>": {
    "<annotation_key>": "annotation_value"
  }
}
```

Note that there are two special filenames:

> $config is reserved for the annotation of the manifest config.
> $manifest is reserved for the annotation of the manifest itself.

## Trying it out

Step 1. this is annontation file -
```
{
  "$config": {
    "hello": "world"
  },
  "$manifest": {
    "foo": "bar"
  },
  "cake.txt": {
    "fun": "more cream"
  }
}
```

so you will also have to make cake.txt and juice.txt for next step.

Step 2. push it

```oras push --annotation-file annotations.json localhost:5000/club:party cake.txt juice.txt```

![Manifest Config _ OCI Registry As Storage - Google Chrome 18-07-2023 16_29_44](https://github.com/1Shubham7/understanding-ORAS/assets/116020663/319deb40-0a7d-4b6b-9b14-6506cb5ca0b0)

ti check the manifest file - `oras manifest fetch localhost:5000/club:party --pretty`

It results in -
![Billy Zha - Cloud Native Computing Foundation - Slack 18-07-2023 16_48_41](https://github.com/1Shubham7/understanding-ORAS/assets/116020663/a973ea6a-c438-4cab-a710-629e6e128064)

## these are complete docs till go scripting, will be covering them in future.
