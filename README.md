# Portefaix Elasticsearch

* Master :
[![Circle CI](https://circleci.com/gh/portefaix/docker-elasticsearch/tree/master.svg?style=svg)](https://circleci.com/gh/portefaix/docker-elasticsearch/tree/master)

* Develop :
[![Circle CI](https://circleci.com/gh/portefaix/docker-elasticsearch/tree/develop.svg?style=svg)](https://circleci.com/gh/portefaix/docker-elasticsearch/tree/develop)

![logo](https://raw.githubusercontent.com/1science/docker-alpine/latest/logo.png)

[Alpine Linux][] is a Linux distribution built around musl libc and BusyBox.
This image is based on the official Alpine Linux.

The following [Elasticsearch][] plugins are installed :

Some [Elasticsearch][] plugins are available:
* [ElasticSearchHead][]: `http://xxx:9200/_plugin/head/`
* [Kopf][]: `http://xxx:9200/_plugin/kopf/`

Ports exported are : `9200` and `9300`
Volumes exported is : `/usr/share/elasticsearch/data`

## Usage

    $ docker run -it -p 9200:9200 -p 9300:9300 portefaix/elasticsearch:1.7.1

## Supported tags

- `1.5.2` [![](https://badge.imagelayers.io/portefaix/elasticsearch:1.5.2.svg)](https://imagelayers.io/?images=portefaix/elasticsearch:1.5.2 'imagelayers.io')
- `1.6.0` [![](https://badge.imagelayers.io/portefaix/elasticsearch:1.6.0.svg)](https://imagelayers.io/?images=portefaix/elasticsearch:1.6.0 'imagelayers.io')
- `1.7.1` [![](https://badge.imagelayers.io/portefaix/elasticsearch:1.7.1.svg)](https://imagelayers.io/?images=portefaix/elasticsearch:1.7.1 'imagelayers.io')
- `1.7.2` [![](https://badge.imagelayers.io/portefaix/elasticsearch:1.7.2.svg)](https://imagelayers.io/?images=portefaix/elasticsearch:1.7.2 'imagelayers.io')
- `2.0.0` [![](https://badge.imagelayers.io/portefaix/elasticsearch:2.0.0.svg)](https://imagelayers.io/?images=portefaix/elasticsearch:2.0.0 'imagelayers.io')
- `2.1.0` [![](https://badge.imagelayers.io/portefaix/elasticsearch:2.1.0.svg)](https://imagelayers.io/?images=portefaix/elasticsearch:2.1.0 'imagelayers.io')
- `2.2.0` [![](https://badge.imagelayers.io/portefaix/elasticsearch:2.2.0.svg)](https://imagelayers.io/?images=portefaix/elasticsearch:2.2.0 'imagelayers.io')

## License

See [LICENSE](LICENSE) for the complete license.


## Changelog

A [ChangeLog.md](ChangeLog.md) is available.


## Contact

Nicolas Lamirault <nicolas.lamirault@gmail.com>


[Alpine Linux]: http://www.alpinelinux.org

[Elasticsearch]: https://www.elastic.co/products/elasticsearch
[ElasticSearchHead]: http://mobz.github.io/elasticsearch-head
[ElasticHQ]: http://www.elastichq.org
[Kopf]: https://github.com/lmenezes/elasticsearch-kopf
