# fastdds-router-demo

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

### Start Discovery-Server

```bash
docker-compose -f docker-compose.discovery-server.yml up
```

Check IPv6 address of the `dds-discovery-server` element of your Husarnet network (eg. in https://app.husarnet.com ) and place it's IPv6 in `./dds-router-config.yaml`.

The Discovery Server guid is as follows (read more [here](https://github.com/DominikN/fastdds-discovery-server-demo/blob/main/docker_image/fastdds_server.xml)):

```xml
<prefix>44.49.53.43.53.45.52.56.45.52.5F.31</prefix>
```

That Docker Compose deployment starts also a basic `listener` node.

### Start Talker and DDS Router

```bash
docker-compose -f docker-compose.talker.yml up
```

## Testing DDS Router config (`yaml` file)

The file `./dds-router-config.yml` is attached as a volume to a `dds-router` service. The DDS Router runs with a configuration reload every 2 seconds, so updating the provided config "on the fly" should work. [Read more](https://eprosima-dds-router.readthedocs.io/en/latest/rst/user_manual/user_interface.html#reload-topics)