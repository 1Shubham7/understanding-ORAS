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

so there are two terms - image index and image manifest :
image index contains information about a set of images that can span a variety of architectures and operating systems.

->> an image manifest provides a configuration and set of layers for a single container image for a specific architecture and operating system.

## OCI Image Manifest Specification

There are three main goals of the Image Manifest Specification. 
- The first goal is content-addressable images, by supporting an image model where the image's configuration can be hashed to generate a unique ID for the image and its components.
- The second goal is to allow multi-architecture images, through a "fat manifest" which references image manifests for platform-specific versions of an image. In OCI, this is codified in an image index.
- The third goal is to be translatable to the OCI Runtime Specification.

>> Image manifest Property Description
Now there are many image manifest Property Description 
like `schemaVersion` (int) , `mediaType` (string), `artifactType` (string) etc etc. To learn more about them -> https://github.com/opencontainers/image-spec/blob/main/manifest.md

Here's an example image manifest :
`{
  "schemaVersion": 2,
  "mediaType": "application/vnd.oci.image.manifest.v1+json",
  "config": {
    "mediaType": "application/vnd.oci.image.config.v1+json",
    "digest": "sha256:b5b2b2c507a0944348e0303114d8d93aaaa081732b86451d9bce1f432a537bc7",
    "size": 7023
  },
  "layers": [
    {
      "mediaType": "application/vnd.oci.image.layer.v1.tar+gzip",
      "digest": "sha256:9834876dcfb05cb167a5c24953eba58c4ac89b1adf57f28f2f9d09af107ee8f0",
      "size": 32654
    },
    {
      "mediaType": "application/vnd.oci.image.layer.v1.tar+gzip",
      "digest": "sha256:3c3a4604a545cdc127456d94e421cd355bca5b528f4a9c1905b15da2eb4a4c6b",
      "size": 16724
    },
    {
      "mediaType": "application/vnd.oci.image.layer.v1.tar+gzip",
      "digest": "sha256:ec4b8955958665577945c89419d1af06b5f7636b4ac3da7f12184802ad867736",
      "size": 73109
    }
  ],
  "subject": {
    "mediaType": "application/vnd.oci.image.manifest.v1+json",
    "digest": "sha256:5b0bcabd1ed22e9fb1310cf6c2dec7cdef19f0ad69efa1f392e94a4333501270",
    "size": 7682
  },
  "annotations": {
    "com.example.key1": "value1",
    "com.example.key2": "value2"
  }
}`

