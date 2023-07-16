As told earilier do -> 
`docker run -d -p 5000:5000 --name oras-quickstart ghcr.io/project-zot/zot-linux-amd64:latest`

### Pushing an artifact

Step 1. Then creating a sample file :
`echo "hello world" > artifact.txt`

Step 2. Pushing the artifact :
`oras push --plain-http localhost:5000/hello-artifact:v1 --artifact-type application/vnd.acme.rocket.config artifact.txt:text/plain`

you will get similar output ->
![sson](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/8b9d03a4-e4f8-40b1-a203-28aa7a3d0257)

You will now see the zot user interface at http://localhost:5000/, you will find the artifact there
![oras2](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/6d3353b6-30b4-445f-9b15-1896b41ab898)

### Pulling the same artifact :

Step 1. `oras pull localhost:5000/hello-artifact:v1`

you will get similar output
![Windows PowerShell (x86) 16-07-2023 18_49_19](https://github.com/1Shubham7/repo-for-notary-and-oras/assets/116020663/d0bdab04-9f7a-4756-8d52-063667272b85)

### Attaching an Artifact

Step 1. First you will have to pull the artifact, you must have do this in previous section so ignore
`oras pull localhost:5000/hello-artifact:v1`

Step 1. Creating a sample file
`echo "hello world" > hi.txt`

Step 2. 
