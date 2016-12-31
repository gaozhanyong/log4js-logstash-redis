# log4js-logstash-redis
[![node version][node-image]][node-url]
[![build status][travis-image]][travis-url]

[node-image]: https://img.shields.io/badge/node.js-%3E=_6.0-green.svg?style=flat-square
[node-url]: http://nodejs.org/download/
[travis-image]: https://travis-ci.org/beyond5959/log4js-logstash-redis.svg?branch=master
[travis-url]: https://travis-ci.org/beyond5959/log4js-logstash-redis

A simple log appender for log4js that sends the data to logstash by redis.


Installation
------------
```
npm install log4js-logstash-redis --save
```

Usage: logstash configuration
-----------------------------
In the "input" part of the logstash server conf :
```
input {
  redis {
  	codec => json
  	data_type => "list"
  	key => "YOURKEY"
  }
}
```

Usage: log4js configuration
---------------------------
Plain javascript
```javascript
  const log4js = require('log4js');
  log4js.configure({
      "appenders": [{
          "type": "log4js-logstash-redis",
          "key": "YOURKEY",
          "redis": {
              "host": "localhost",
              "port": 6379,
              "db": 0 // default 0
          }
      }]
  });

  const logger = log4js.getLogger('tests');

  logger.debug('hello hello');
```
