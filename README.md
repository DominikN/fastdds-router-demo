# fastdds-router-demo

[![Test DDS Router](https://github.com/DominikN/fastdds-router-demo/actions/workflows/test.yaml/badge.svg)](https://github.com/DominikN/fastdds-router-demo/actions/workflows/test.yaml)

A demo showing how to use DDS Router and Husarnet to bridge remote ROS 2 docker deployments

## Quick Start

### Get your Husarnet Join Code

Before running examples get your **Husarnet Join Code**. You will use it to connect Docker containers to the same VPN network.

At first rename `.env.template` file to `.env`.

You will find your Join Code at **https://app.husarnet.com  
 -> Click on the desired network  
 -> `Add element` button  
 -> `Join code` tab**

…and change the `JOINCODE` variable in the `.env` files.

### Start Discovery-Server and DDS Router

```bash
docker-compose -f compose.ds.yml up
```

That Docker Compose deployment starts also a basic `listener` node.

### Start Talker and DDS Router

```bash
docker-compose -f compose.talker.yml up
```

### Start Listener and DDS Router

```bash
docker-compose -f compose.listener.yml up
```

## Testing DDS Router config (`yaml` file)

Files `./router-config.*.yml` are attached as volumes to `dds-router` services. The DDS Router runs with a configuration reload every 2 seconds, so updating the provided config "on the fly" should work. [Read more](https://eprosima-dds-router.readthedocs.io/en/latest/rst/user_manual/user_interface.html#reload-topics)