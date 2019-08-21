# drone
Drone CI (ARM)

## Building Binaries

Drone Server:

```
$ DRONE_BUILD_NUMBER=1.2.3
$ wget https://github.com/drone/drone/archive/v${DRONE_BUILD_NUMBER}.zip
$ cd drone/cmd/drone-server
$ go get
$ GOOS=linux \
  GOARCH=arm \
  GOARM=7 \
  go build -ldflags '-X github.com/drone/drone/version.VersionDev=build.'${DRONE_BUILD_NUMBER} \
  -o release/linux/arm/drone-server github.com/drone/drone/cmd/drone-server
$ mv release ../../../
```

Drone Agent:

```
$ DRONE_BUILD_NUMBER=1.2.3
$ wget https://github.com/drone/drone/archive/v${DRONE_BUILD_NUMBER}.zip
$ cd drone/cmd/drone-agent
$ go get
$ GOOS=linux \
  GOARCH=arm \
  CGO_ENABLED=0 \
  GOARM=7 \
  go build -ldflags '-X github.com/drone/drone/version.VersionDev=build.'${DRONE_BUILD_NUMBER} \
  -o release/linux/arm/drone-agent github.com/drone/drone/cmd/drone-agent
$ mv release ../../../
```

## Docker Hub

- [pistacks/drone-server:1.2.3](https://hub.docker.com/r/pistacks/drone-server)
- [pistacks/drone-agent:1.2.3](https://hub.docker.com/r/pistacks/drone-agent)
