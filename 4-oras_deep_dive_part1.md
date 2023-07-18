Couldn't understand this part -
![oras3](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/813ffcf2-b469-49ac-b109-c49ef593f54d)

but for authentication we can do this :
`oras pull -u username -p password myregistry.io/myimage:latest `
replace username, password, myregistry and my image accordingly.

## Pushing Artifacts

## 1. Pushing artifacts with single files

Pushing single files involves referencing the unique artifact type and at least one file. Defining an Artifact uses the `config.mediaType` as the unique artifact type. The following sample defines a new Artifact Type of Acme Rocket - 

> Make sure that Zot or registry is running on localhost:5000 for this [Explained eariler how to do that]

Step 1. Create a sample file to push/pull as an artifact
```echo "hello world" > artifact.txt```

Step 2. Push the sample file to the registry:
```oras push localhost:5000/hello-artifact:v1 --artifact-type application/vnd.acme.rocket.config ./artifact.txt```

Now your file is pushed.
Mine already exists that's why it shows -

![oras - Cloud Native Computing Foundation - Slack 18-07-2023 10_28_23](https://github.com/1Shubham7/understanding-ORAS/assets/116020663/18f813da-f1ff-4c69-83d4-ff6e86d18f49)

Step 3. Pull the file from the registry

I am doing this part on Git Bash not on Powershell ->

Step 3.1 -  first delete the file
```rm -f artifact.txt```

Step 3.2 pull the artifact you pushed (it was called hello-artifact)
```oras pull localhost:5000/hello-artifact:v1```

Step 3.3 printing what was on the file, it should print "hello world"
```cat artifact.txt ```

![Screenshot 18-07-2023 10_35_50](https://github.com/1Shubham7/understanding-ORAS/assets/116020663/d947bf83-7d1c-4b6d-a6fd-8098932c5a8e)

Step 4. Push the sample file, with a layer `mediaType`, using the format `filename[:type]`
```oras push localhost:5000/hello-artifact:v2 --artifact-type application/vnd.acme.rocket.config artifact.txt:text/plain```

![MINGW64__c_Users_Shubh 18-07-2023 10_37_56](https://github.com/1Shubham7/understanding-ORAS/assets/116020663/5eeda96f-1ce5-4b0c-947c-a7a8bf4890ea)

## 2. Pushing artifacts with config files

config files can be used by the artifact to determine how or where to process and/or route the blobs.

Step 1. Create a config file
```echo "{\"name\":\"foo\",\"value\":\"bar\"}" > config.json```

Step 2. Push an artifact, with the `config.json` file
```oras push localhost:5000/hello-artifact:v2 --config config.json:application/vnd.acme.rocket.config.v1+json artifact.txt:text/plain```

![oras5](https://github.com/1Shubham7/understanding-ORAS/assets/116020663/ce9c7948-b4ee-4a45-9bb2-9c6671c5dd87)

you can the the similarities in the steps. These are just optional ways to push artifacts.

## 3. Pushing artifacts with multiple files

here we'll push a collection of files.
- A single file (artifact.txt)
- A collection of files (docs/*)

Step 1. Run these three steps to create additional blobs
```
mkdir docs
echo "Docs on this artifact" > ./docs/readme.md
echo "More content for this artifact" > ./docs/readme2.md
```

Step 2. Create a config file, referencing the entry doc file
```
echo "{\"doc\":\"readme.md\"}" > config.json
```

Step 3. Push multiple files with different `mediaTypes`:

```
oras push localhost:5000/hello-artifact:v2 --config config.json:application/vnd.acme.rocket.config.v1+json artifact.txt:text/plain ./docs/:application/vnd.acme.rocket.docs.layer.v1+tar
```
The Docs says that the push would generate this manifest, 
To have a look at what manifest was generated - `oras manifest fetch localhost:5000/hello-artifact:v2 --pretty`
Mine is here -
![MINGW64__c_Users_Shubh 18-07-2023 16_43_48](https://github.com/1Shubham7/understanding-ORAS/assets/116020663/a92d11f4-7230-4aac-b7c0-ccf0c40df2b6)

your's should be like this ->
```
{
  "schemaVersion": 2,
  "config": {
    "mediaType": "application/vnd.acme.rocket.config.v1+json",
    "digest": "sha256:7aa5d0dee9a3a73c81db4356cf7aa5666e175d96e68ee763eeb977bd7ba59ee5",
    "size": 20
  },
  "layers": [
    {
      "mediaType": "text/plain",
      "digest": "sha256:a948904f2f0f479b8f8197694b30184b0d2ed1c1cd2a1ec0fb85d299a192a447",
      "size": 12,
      "annotations": {
        "org.opencontainers.image.title": "artifact.txt"
      }
    },
    {
      "mediaType": "application/vnd.acme.rocket.docs.layer.v1+tar",
      "digest": "sha256:20ae7d51e2365405e6942439140d897548e1d4610db60354aef8a5ce1f1699a7",
      "size": 196,
      "annotations": {
        "io.deis.oras.content.digest": "sha256:4329ea6c620ca4e9cedc5f5e8040432114cb5d64fc53107ea870db149e3d2b9e",
        "io.deis.oras.content.unpack": "true",
        "org.opencontainers.image.title": "docs"
      }
    }
  ]
}
```

Now for pulling, the same thing `oras pull localhost:5000/hello-artifact:v2`

## Using cache when pulling artifacts

In order to save unnecessary network bandwidth and disk I/O, oras provides a solution to pull the artifacts into a local content-address storage (CAS) if the content does not exist, and then copy the artifact to the desired storage. The cache directory is specified by using the environment variable `ORAS_CACHE`.

Step 1. Set cache root
`export ORAS_CACHE=~/.oras/cache`

Step 2. Pull artifacts as usual
`oras pull localhost:5000/hello:latest`   -> This step gives me an error.
