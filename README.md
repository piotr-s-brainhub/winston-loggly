# winston-loggly

A [Loggly][0] transport for [winston][1].

## Usage
``` js
  var winston = require('winston');

  //
  // Requiring `winston-loggly` will expose
  // `winston.transports.Loggly`
  //
  require('winston-loggly');

  winston.add(winston.transports.Loggly, options);
```

Or in the winston@3.0.0-rc1:
```js
const winston = require('winston');
const Loggly = require('winston-loggly');

const logger = winston.createLogger({
  level,
  transports: [
    new Loggly({
      inputToken: process.env.LOGGLY_TOKEN,
      subdomain: process.env.LOGGLY_SUBDOMAIN,
      stripColors: true,
    }),
  ],
});
```

The Loggly transport is based on [Nodejitsu's][2] [node-loggly][3] implementation of the [Loggly][0] API. If you haven't heard of Loggly before, you should probably read their [value proposition][4]. The Loggly transport takes the following options. Either 'inputToken' or 'inputName' is required:

* __level:__ Level of messages that this transport should log.
* __subdomain:__ The subdomain of your Loggly account. *[required]*
* __auth__: The authentication information for your Loggly account. *[required with inputName]*
* __inputName:__ The name of the input this instance should log to.
* __inputToken:__ The input token of the input this instance should log to.
* __json:__ If true, messages will be sent to Loggly as JSON.
* __tags:__ An array of tags to send to loggly.
* __isBulk:__ If true, sends messages using bulk url
* __stripColors:__ Strip color codes from the logs before sending


*Metadata:* Logged in suggested [Loggly format][5]

## Motivation
`tldr;?`: To break the [winston][1] codebase into small modules that work together.

The [winston][1] codebase has been growing significantly with contributions and other logging transports. This is **awesome**. However, taking a ton of additional dependencies just to do something simple like logging to the Console and a File is overkill.

## Installation

### Installing npm (node package manager)

``` bash
  $ curl http://npmjs.org/install.sh | sh
```

### Installing winston-loggly

``` bash
  $ npm install winston
  $ npm install winston-loggly
```

## Run Tests
All of the winston tests are written in [vows][6], and cover all of the use cases described above. You will need to add valid credentials for the various transports included to test/config.json before running tests:

``` js
  {
    "transports": {
      "loggly": {
        "subdomain": "your-subdomain",
        "inputToken": "really-long-token-you-got-from-loggly",
        "auth": {
          "username": "your-username",
          "password": "your-password"
        }
      }
    }
  }
```

Once you have valid configuration and credentials you can run tests with [npm][7]:

```
  npm test
```

#### Author: [Charlie Robbins](http://blog.nodejitsu.com)
#### License: MIT

[0]: http://loggly.com
[1]: https://github.com/flatiron/winston
[2]: http://nodejitsu.com
[3]: https://github.com/nodejitsu/node-loggly
[4]: http://www.loggly.com/product/
[5]: http://www.loggly.com/docs/automated-parsing/
[6]: http://vowsjs.org
[7]: http://npmjs.org
