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


