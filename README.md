# fastdds-router-demo

[![Test DDS Router](https://github.com/DominikN/fastdds-router-demo/actions/workflows/test.yaml/badge.svg)](https://github.com/DominikN/fastdds-router-demo/actions/workflows/test.yaml)

A demo showing how to use DDS Router and Husarnet to connect remote ROS 2 nodes over the Internet.

> **Prerequisites** 
>
> I use the [latest compose file spec](https://github.com/compose-spec/compose-spec/blob/master/spec.md) (eg. no `version: "3.7"` on top of. `.yaml` file and using `compose.yaml` instead of `docker-compose.yaml`). Therefore make sure you use [Docker Compose V2](https://docs.docker.com/compose/cli-command/).
>
> Tested on the following host:
>
> ```bash
> $ docker --version
> Docker version 20.10.10, build b485636
> $ docker compose version
> Docker Compose version v2.2.3
> ```

## Quick Start

### Get your Husarnet Join Code

Before running examples get your **Husarnet Join Code**. You will use it to connect Docker containers to the same VPN network.

At first rename `.env.template` file to `.env`.

You will find your Join Code at **https://app.husarnet.com  
 -> Click on the desired network  
 -> `Add element` button  
 -> `Join code` tab**

…and change the `JOINCODE` variable in the `.env` files.

### Deploy

You can execute those commands on the same, or on different hosts in different LANs.

#### Discovery-Server and DDS Router

```bash
docker compose -f compose.ds.yaml up
```

#### Talker and DDS Router

```bash
docker compose -f compose.talker.yaml up
```

#### Listener and DDS Router

```bash
docker compose -f compose.listener.yaml up
```

## Testing DDS Router config (`yaml` file)

Files `./router-config.*.yaml` are attached as volumes to `dds-router` services. The DDS Router runs with a configuration reload every 10 seconds, so updating the provided config "on the fly" should work. [Read more](https://eprosima-dds-router.readthedocs.io/en/latest/rst/user_manual/user_interface.html#reload-topics)