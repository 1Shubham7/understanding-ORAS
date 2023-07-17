## OCI - Open Container Initiative
_" The Open Container Initiative (OCI) is a lightweight, open governance structure (project), formed under the auspices of the Linux Foundation, for the express purpose of creating open industry standards around container formats and runtimes. "_
The OCI provides a set of open standards and specifications for containers. These standards ensure that containers created by different tools and platforms work together smoothly

The OCI currently contains three specifications: 
1. the Runtime Specification (runtime-spec)
   This specification explains how to run a container. It defines the setup and environment for a container to work properly.
   
2. the Image Specification (image-spec)
   This specification describes how to create a container image.
  
3. Distribution Specification (distribution-spec).
   This specification outlines how container images should be stored and shared. It defines the rules for uploading and downloading container images to and from
   container registries.

### How it works:

First, an OCI implementation (like Docker) downloads a container image.
Then, the image is unpacked into a "filesystem bundle" by the OCI runtime.
Finally, the OCI runtime runs the application inside the container.

### Supporting User Experience:
OCI is designed to work like familiar container engines such as Docker or rkt. Users can run a container image without any extra settings:
For example:
`docker run example.com/org/app:v1.0.0
rkt run example.com/org/app,version=v1.0.0`

OCI's Image Format contains all the necessary information to launch the application inside the container. This includes the command to run, environment variables, and other details.  This specification defines how to create an OCI Image, and output an **image manifest**, a **filesystem (layer) serialization**, and an **image configuration**. 
Now what are these three terms:
- Image manifest
- filesystem serialization
- image configuration

# Image Manifest

so there are two terms image index and image manifest :
image index contains information about a set of images that can span a variety of architectures and operating systems.
->> an image manifest provides a configuration and set of layers for a single container image for a specific architecture and operating system.

## OCI Image Manifest Specification

