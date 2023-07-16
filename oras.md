
ORAS provides a way to push and pull OCI Artifacts to and from OCI Registries.

Now what are artifacts and registries and what is OCI. 

### Artifacts
artifacts are like the "building blocks" of your software. They are the outputs generated as a result of the different steps involved in creating, testing, and deploying your application. Imagine building a house - the artifacts are like the bricks, cement, and other materials that you use to construct it.

Registries are already explained

### OCI means Open Container Initiative
To know more : https://opencontainers.org/

### OCI Registries 
Registries that implement the distribution-spec are referred to herein as OCI Registries. - ORAS Docs

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
