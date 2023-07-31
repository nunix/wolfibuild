# wolfibuild
Set of Dockerfiles used to create WSL distros based on WolfiOS

## Wolfi community call
The Dockerfiles `k3s`, `openrc` and `k3d` will be used for a demo during the Wolfi community call on August 2nd.

The demo consists on the following steps:

- Build the Dockerfiles and output the result as a `tar` file instead of container image
- Import the `tar` file as a new wsl distro
- K3s is already installed, so just start it with the commands depending on the distro
  - K3s: `k3s server` + open a new tab to show the cluster is created and running (`kubectl cluster-info && kubectl get all -A`)
  - OpenRC: check the `k3s` service (`rc-status`), it should be running by default. Show the cluster is running (`kubectl cluster-info && kubectl get all -A`)
  - k3d: check the containerD service (`rc-status`), it should be running by default. Create a new k3d container (`nerdctl run -d --privileged --name k3dind -p 6550:6550 -v $PWD/.kube:/root/.kube ghcr.io/k3d-io/k3d:sha-1afe360-dind`), create a new k3d cluster (`nerdctl exec -it k3dind k3d cluster create --api-port 6550`), show the cluster is running (`kubectl cluster-info && kubectl get all -A`)
 
## Work in progress
The Dockerfile `systemd` is still being worked on and doesn't work as expected.

## Future work
There's at least another test to be done and it will be described here once I started working on it.

## Tips
The command to create the `tar` file can be used for other distros, feel free to take the ideas and create your own.
