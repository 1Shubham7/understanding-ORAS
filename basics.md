We all know what containers are, let's directly jump into Container Registries and OCI

## Container Registries -
Container registries are centralized repositories that store and manage container images. In the context of software development and deployment using containers,a container registry plays a crucial role in 
facilitating the storage, distribution, and versioning of container images.

Like Docker Hub, it is a container registry
Now like every cloud service like Google has container registry called Google Container Registry (GCR), Amazon has Amazon Elastic Container Registry (ECR), so keep that in mind.

## Notary v2
We are only insterested about Notary v2. but this pic is about Notary v1 -> 
![notaryv1](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/c5b69eab-baeb-4cd3-a03a-71b033150dda)

// The CLI is called Notation

What happens is when we build a container image , Docker looks out for image in your PC if not found, Docker goes to Docker Hub (container registry) and pulls an image from there. Now what happens here is that you don't know what you pulled down actually, what kind of resounce you are accessing, is it signed by people I trust. What Notary does is that it provides you the signatures - now you can look at those signatures for example

![image1](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/e60c68fc-bf63-4e26-a615-143fc215f8ef)

and say ok, I can trust Bob's signature, I have used other resources from Bob, therefore I can trust the container image and I will use it.

-> Notary is one of the projects that enable users to verify the origin of container images before resources are accessed from container registries.

Get Notation installed
Step 1. `notation`
Step 2. `
