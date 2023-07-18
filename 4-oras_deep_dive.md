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
