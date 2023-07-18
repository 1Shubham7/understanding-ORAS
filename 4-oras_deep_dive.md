Couldn't understand this part -
![oras3](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/813ffcf2-b469-49ac-b109-c49ef593f54d)

but for authentication we can do this :
`oras pull -u username -p password myregistry.io/myimage:latest `
replace username, password, myregistry and my image accordingly.

## Pushing Artifacts

## 1. Pushing artifacts with single files

Pushing single files involves referencing the unique artifact type and at least one file. Defining an Artifact uses the `config.mediaType` as the unique artifact type. The following sample defines a new Artifact Type of Acme Rocket - 

Step 1. Create a sample file to push/pull as an artifact
```echo "hello world" > artifact.txt```

Step 2. Push the sample file to the registry:
```oras push localhost:5000/hello-artifact:v1 --artifact-type application/vnd.acme.rocket.config ./artifact.txt```
