# Quickstart guide to writing a challenge

The basic steps when preparing a challenge are:

* A Docker image is built from the `challenge` directory.
* Edit the Foundry project at `challenge/project`. Note the deploy script at `script/Deploy.s.sol` and the solve script at `Solve.s.sol`
* To try the challenge locally, you will need to
  * create a a local cluster with `kctf cluster create --type kind --start $configname`
  * deploy the challenge with `kctf chal start`
* To access the challenge, create a port forward with `kctf chal debug port-forward` and connect to it via `nc localhost PORT` using the printed port.
* Check out `kctf chal <tab>` for more commands.

## Directory layout

The following files/directories are available:

### /challenge.yaml

`challenge.yaml` is the main configuration file. You can use it to change
settings like the name and namespace of the challenge, the exposed ports, the
proof-of-work difficulty etc.
For documentation on the available fields, you can run `kubectl explain challenge` and
`kubectl explain challenge.spec`.

### /challenge

The `challenge` directory contains a Dockerfile that describes the challenge and
any challenge files.

### /healthcheck

The `healthcheck` directory is optional. If you don't want to write a healthcheck, feel free to delete it. However, we strongly recommend that you implement a healthcheck :).

We provide a basic healthcheck skeleton that uses pwntools to implement the
healthcheck code. The only requirement is that the healthcheck replies to GET
requests to http://$host:45281/healthz with either a success or an error status
code.

In most cases, you will only have to modify `healthcheck/healthcheck.py`.

## API contract

Ensure your setup fulfills the following requirements to ensure it works with kCTF:

* Verify `kctf_setup` is used as the first command in the CMD instruction of your `challenge/Dockerfile`.
* You can do pretty much whatever you want in the `challenge` directory but:
* We strongly recommend using nsjail in all challenges. While nsjail is already installed, you need to configure it in `challenge/nsjail.cfg`. For more information on nsjail, see the [official website](https://nsjail.dev/).
* Your challenge receives connections on port 1337. The port can be changed in `challenge.yaml`.
* The healthcheck directory is optional.
  * If it exists, the image should run a webserver on port 45281 and respond to `/healthz` requests.