
ORAS provides a way to push and pull OCI Artifacts to and from OCI Registries.

Now what are artifacts and registries and what is OCI. 

![oras4](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/f4f23c87-7fed-425a-a1dd-ec58d4da3f4d)


### Artifacts
artifacts are like the "building blocks" of your software. They are the outputs generated as a result of the different steps involved in creating, testing, and deploying your application. Imagine building a house - the artifacts are like the bricks, cement, and other materials that you use to construct it.

Registries are already explained

### OCI means Open Container Initiative
To know more : https://opencontainers.org/

### OCI Registries 
Registries that implement the distribution-spec are referred to herein as OCI Registries. - ORAS Docs

### OCI Artifacts
The OCI Artifacts project is an attempt to define an opinionated way to leverage OCI Registries for arbitrary artifacts without masquerading them as container images.

The first line of ORAS Docs says _Registries are evolving as generic artifact stores._ What does that mean?
-> that means  registries are transforming into versatile storage places for various types of digital items. They are not limited to just container images or specific formats anymore. Instead, they are becoming more flexible and can store different types of artifacts, which are the digital "things" produced during software development.In the past, registries were primarily used to store container images.However, as software development practices have evolved, so have the needs for storing different types of files beyond just container images. These other files are called "artifacts," and they can be anything that's important for the software development process. For example:
- Compiled code or executables.
- Application packages for languages like Python or JavaScript.
- Documentation files, like READMEs or user guides.
- Test reports generated during the testing process.
- Configuration files for deployments.
- Database scripts for managing data.

Modern registries are adapting to this change by supporting storage for a wide range of artifacts. They are becoming more like flexible digital warehouses that can hold different types of files related to software development and deployment.
This evolution is beneficial because it allows developers and teams to keep all their essential files and resources in one central location. It simplifies collaboration, ensures consistent access to various artifacts, and helps maintain a clear record of the software development process.


//  OCI Image Manifests have a required field known as `config.mediaType` . According to the guidelines provided by OCI Artifacts, this field provides the ability to differentiate between various types of artifacts.

- ORAS works similarly to tools you may already be familiar with, such as docker. It allows you to push (upload) and pull (download) things to and from an OCI Registry, and also handles login (authentication) and token flow (authorization). What ORAS does differently is shift the focus from container images to other types of artifacts.



ORAS Docs -> We will be using zot registry in this guide. Zot ![registry](https://zotregistry.io/v1.4.3/) is an OCI-native container registry for distributing container images and OCI artifacts.

### Installation (Windows)

Step 1.`winget install oras` that's it. For Mac or Linux check this out -> https://oras.land/docs/installation/
now just do `oras version` to check if it is installed or not.
![Windows PowerShell (x86) 16-07-2023 17_20_59](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/da71bb3a-b665-4f5d-908c-481ffc43e9ff)

## Quickstart

Now we will have to install zot : for Linux user check out https://zotregistry.io/install-guides/install-guide-linux/ . but I couldn't find any way in this link to install for windows.

Prerequisite is Docker, have Docker installed in your PC, then -
`docker run -d -p 5000:5000 --name oras-quickstart ghcr.io/project-zot/zot-linux-amd64:latest`


