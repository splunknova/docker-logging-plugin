# Splunk Nova Loggging Driver plugin for Docker

The Splunk Nova Logging Driver plugin enables users to send their container logs directly to a Splunk Nova account from a Docker container. See [Splunk logging driver] to send container logs to
[HTTP Event Collector](http://dev.splunk.com/view/event-collector/SP-CAAAE6M) in Splunk Enterprise and Splunk Cloud.

## Get Started

Get started by creating an account on https://www.splunknova.com.

### Prerequisites

Sign up or log in to [Docker Hub]. If you have not used Docker before, see the [Getting started tutorial](https://docs.docker.com/mac/started) for Docker.

### Install

If necessary, download and install [Docker][docker] Community Edition (CE) or Enterprise Edition (EE) >= 1.12.

Open a shell prompt or Terminal window and install the `splunk/docker-logging-driver.` plugin. To pull and enable the plugin, run:

```
docker plugin install splunk/docker-logging-driver:latest --alias splunk
```

Verify installation by running:

```
$ docker plugin ls
```
This command lists all the Docker plugins that are currently installed.

```
ID                  NAME                               TAG                 DESCRIPTION                ENABLED
89443ca1c345        splunknova/docker-logging-plugin   latest              Nova plugin for Docker     true
```

### Configure

You can configure Docker logging to use the splunk driver by default or on a per-container basis. The plugin uses the same parameters as the [splunk logging driver](https://docs.docker.com/engine/admin/logging/splunk/).

## Usage

Create an account on [www.splunknova.com][Splunk Nova]. Grab your API credentials and use them here.

#### Splunk Nova Example

Once you have your API credentials, replace the `splunk-token` with your Base-64 Encoded API Key from https://www.splunknova.com/apikeys.

```
$ docker run --log-driver=splunk \
             --log-opt splunk-url=https://api.splunknova.com:443 \
             --log-opt splunk-token=<YOUR BASE64 ENCODED API KEYS> \
             --log-opt splunk-url-path='/v1/events' \
             --log-opt tag="{{.Name}}/{{.FullID}}" \
             --log-opt splunk-format=nova \
             --log-opt splunk-verify-connection=false \
             --log-opt splunk-source='docker-logging' \
             -it ubuntu bash
```

### Development

To contribute to development, clone and run make

```
git clone git@github.com:splunk/docker-logging-plugin.git
cd docker-logging-plugin
make
```

See [Docker log driver plugins](https://docs.docker.com/engine/extend/plugins_logging/) for more information.

[docker]: https://www.docker.com/get-docker
[Docker Hub]: https://hub.docker.com
[HTTP Event Collector]: http://dev.splunk.com/view/event-collector/SP-CAAAE6M
[Splunk logging driver]: https://docs.docker.com/engine/admin/logging/splunk/
[Splunk Nova]: https://splunknova.com
