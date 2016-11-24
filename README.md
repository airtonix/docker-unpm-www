# docker-unpm-www

Containerised web frontend for unpm (or any npm registry)

## Sources

- [unpm-www](https://github.com/jarofghosts/unpm-www)
- [unpm](https://github.com/hayes/unpm)


## Development

**experiemental**

```
$ docker-compose up
```

## Deployment

### Rancher

Ssh into your rancher instance

```
$ ssh rancher
[rancher@rancher ~]$ sudo mkdir -p /mnt/Services/unpm
```

Then go :

1. Stacks > All > Create Stack
2. Name: uNpm
3. Paste below into `docker-compose` field

``` yml

web:
  image: airtonix/unpm-www
  ports:
    - "8999:8999"
  links:
    - "registry:registry"
  environment:
    - UNPM_WWW_REGISTRY=http://registry:8123

registry:
  image: 'morlay/unpm'
  ports:
    - '8123:8123'
  volumes:
    - '/mnt/Services/unpm:/unpm/data'

```