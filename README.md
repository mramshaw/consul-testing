# Consul Testing

![Consul logo](images/consul_logo.png)

Noodling around with HashiCorp's [consul](https://www.consul.io/).

## Locally

Verify installation as follows:

```
$ consul --version
Consul v1.0.7
Protocol 2 spoken by default, understands 2 to 3 (agent will automatically use protocol >2 when speaking to compatible agents)
$
```

`consul` may be run in development mode as follows:

```
$ consul agent -dev
```

[As usual, Ctrl-C to terminate.]

The `consul` console should now be available at:

    http://localhost:8500

Register service:

```
$ curl --request PUT --data @sample.json http://localhost:8500/v1/catalog/register
```

Curl service:

```
$ curl http://localhost:8500/v1/catalog/service/redis
```

Dig service:

```
$ dig @127.0.0.1 -p 8600 redis.service.consul
```

Deregister service:

```
$ curl --request PUT --data @sample.json http://localhost:8500/v1/catalog/deregister
```

## With Docker

Some useful stuff here:

    https://www.consul.io/docs/guides/consul-containers.html

[Official image](https://hub.docker.com/_/consul/)

Consul uses HashiCorp's [serf](https://github.com/hashicorp/serf),
but provides some useful features on top of what serf can provide.

#### Ports

Consul uses the following ports:

Port | Protocol
---- | --------
8400 | RPC
8500 | HTTP
8600 | DNS

There is also an HTTPS port, but it usually seems to be set to -1.

#### Binaries

Like many other HashiCorp products, there is only a single binary.

Which simplifies deployment ... the client and the server are the same docker image.

Servers are specified with the `-server` option.

## Golang code

Install dependencies:

    $ go get github.com/hashicorp/consul/api

Voluminous documentation [here](https://godoc.org/github.com/hashicorp/consul/api).

## Credits

Some inspiration here, but not actually very useful:

    http://varunksaini.com/consul-service-discovery-golang/
