As told earilier do -> 
`docker run -d -p 5000:5000 --name oras-quickstart ghcr.io/project-zot/zot-linux-amd64:latest`

Step 1. Then creating a sample file :
`echo "hello world" > artifact.txt`

Step 2. Pushing it :
`oras push --plain-http localhost:5000/hello-artifact:v1 --artifact-type application/vnd.acme.rocket.config artifact.txt:text/plain`
