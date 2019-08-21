
Bash:

```
kind: pipeline
name: default
steps:
  - name: hello
    image: arm32v6/alpine
    commands:
      - echo "hello, world"
```

Docker:

```
kind: pipeline
name: default

steps:
  - name: test
    image: pistacks/docker:dind-19.03.0
    volumes:
      - name: dockersock
        path: /var/run
    commands: 
      - sleep 10
      - docker build -f Dockerfile -t local/test:$DRONE_COMMIT_SHA .
      - docker images
      - docker ps -a

services:
  - name: docker
    image: pistacks/docker:dind-19.03.0
    privileged: true
    volumes:
      - name: dockersock
        path: /var/run

volumes:
  - name: dockersock
    temp: {}
```
