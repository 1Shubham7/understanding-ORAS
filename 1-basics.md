We all know what containers are, let's directly jump into Container Registries and OCI

## Container Registries -
Container registries are centralized repositories that store and manage container images. In the context of software development and deployment using containers,a container registry plays a crucial role in 
facilitating the storage, distribution, and versioning of container images.

Like Docker Hub, it is a container registry
Now like every cloud service like Google has container registry called Google Container Registry (GCR), Amazon has Amazon Elastic Container Registry (ECR), so keep that in mind.

![suppy](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/a9098365-c381-4a71-9818-b026da4ae5b7)


## Notary v2
We are only insterested about Notary v2. but this pic is about Notary v1 -> 
![notaryv1](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/c5b69eab-baeb-4cd3-a03a-71b033150dda)

By Anais -> _Since Notary V1 does not seem actively maintained, I am focusing this blog post on Notary V2. “Not maintained” refers hereby to it having an active community with a public governance structure within the CNCF. There still seem to be lots of projects that integrate and build upon Notary V1 instead of Notary V2, so tech-wise, it still seems to be alive but just not maintained the way you would expect it from a CNCF project. With Notary, users can generate signatures and use these signatures to sign their container image. The signature is then directly attached to the container image, and stored in the container registry._
- _Each signature consists of a public & private key pair. The private key of other people should always be unknown. However, Bob can distribute their public key and announce that they are the owner of the container image X. A user can then verify that Bob’s public key matches the signature on container image X_

By Notary Docs -> _Notation is a CLI project to add signatures as standard items in the registry ecosystem, and to build a set of simple tooling for signing and verifying these signatures._

// The CLI is called Notation

What happens is when we build a container image , Docker looks out for image in your PC if not found, Docker goes to Docker Hub (container registry) and pulls an image from there. Now what happens here is that you don't know what you pulled down actually, what kind of resounce you are accessing, is it signed by people I trust. What Notary does is that it provides you the signatures - now you can look at those signatures for example

![image1](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/e60c68fc-bf63-4e26-a615-143fc215f8ef)

and say ok, I can trust Bob's signature, I have used other resources from Bob, therefore I can trust the container image and I will use it.

-> Notary is one of the projects that enable users to verify the origin of container images before resources are accessed from container registries.

![Download Notary](https://notaryproject.dev/docs/installation/cli/?ref=anaisurl.com)

Get Notation installed (What I did exactly - I use Windows)
Step 1. Download the two files from ![This Link](https://notaryproject.dev/docs/installation/cli/?ref=anaisurl.com)

Step 2. go to downloads in powershell and `(Get-FileHash .\notation_1.0.0-rc.7_windows_amd64.zip).Hash`

Step 3. you will get a hash key, confirm that it matches with the key in the "notation_1.0.0-rc.7_checksums" file

Step 4. `C:\Users\Shubh\Downloads\notation_1.0.0-rc.7_windows_amd64> .\notation.exe`
![notation_1 0 0-rc 7_checksums - Notepad 16-07-2023 10_40_15](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/d5140fdd-0135-4e95-9bf7-aef37dacfa27)

Step 5. for any commands do `C:\Users\Shubh\Downloads\notation_1.0.0-rc.7_windows_amd64> .\notation.exe version`
![Captures 16-07-2023 10_42_15](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/92258e85-14e8-489c-96e7-789dd3ff36be)

I was just randomly trying out multiple things and I though why not `choco install notary` and it worked. After this I can `notary version ` and it works. so

Step 6. `choco install notary`
![Editing repo-for-notary-and-oras_basics md at main · 1Shubham7_repo-for-notary-and-oras - Google Chrome 16-07-2023 10_58_00](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/96851a53-57c3-4b39-9f6f-914e5708d7ad)

