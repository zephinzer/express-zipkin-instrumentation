# Zipkin Instrumentation for Express

[![Build Status](https://travis-ci.org/zephinzer/express-zipkin-instrumentation.svg?branch=master)](https://travis-ci.org/zephinzer/express-zipkin-instrumentation)

## Installation

```bash
npm add express-zipkin-instrumentation --save;
```

## Usage

### Basic
```javascript
const server = express();
// ...
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
server.use(expressZipkinInstrumentation(
  'service-name',
  'http://zipkin.yourdomain.com',
));
```

> The above will result in a service identified in the Zipkin dashboard as `service-name`.

### Complete
```javascript
const server = express();
// ...
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
server.use(expressZipkinInstrumentation(
  'service-name',
  'http://zipkin.yourdomain.com',
  {
    serviceNamePostfix: 'development'
  }
))
```

> The above will result in a service identified in the Zipkin dashboard as `service-name-development`.

### The API

#### `.constructor()`
Using the following to include the package:

```javascript
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
```

The `expressZipkinInstrumentation` variable will be a function that returns the correct middleware. The arguments are:

- `:serviceName`
  - identifies the current application in the zipkin dashboard.
- `:zipkinHostname`
  - the hostname for the zipkin server. When this is set to `null` (the default behaviour if this is not specified), the trace logs will be routed to `stdout` instead via `console.trace`.
- `:options` (optional)
  - an object that can contain the following properties:
    - `:serviceNamePostfix`: this will be appended to the `:serviceName` parameter in dashed-case.

```javascript
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
const server = require('express')();
server.use(expressZipkinInstrumentation(/* ... */));
// ...
```

#### `.getContext()`

Retrieves the context used to initialise the zipkin instrumentation.

```javascript
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
const server = require('express')();
server.use(expressZipkinInstrumentation(/* ... */));
expressZipkinInstrumentation.getContext();
// ...
```

#### `.getInstance()`

Retrieves the zipkin instrumentation instance.

```javascript
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
const server = require('express')();
server.use(expressZipkinInstrumentation(/* ... */));
expressZipkinInstrumentation.getInstance();
// ...
```

#### `.getParentId()`

Retrieves the parent trace ID of the current request.


```javascript
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
const server = require('express')();
server.use(expressZipkinInstrumentation(/* ... */));
server.use((req, res, next) => {
  console.info(expressZipkinInstrumentation.getParentId()); // matches /[0-9a-f]{16}/gi
  next();
});
// ...
```

> Throws an error if `expressZipkinInstrumentation(/* ... */)` was not called yet.

#### `.getRecorder()`

Retrieves the recorder used to initialise the zipkin instrumentation.

```javascript
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
const server = require('express')();
server.use(expressZipkinInstrumentation(/* ... */));
expressZipkinInstrumentation.getRecorder();
// ...
```

#### `.getSpanId()`

Retrieves the span ID of the current request.

```javascript
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
const server = require('express')();
server.use(expressZipkinInstrumentation(/* ... */));
server.use((req, res, next) => {
  console.info(expressZipkinInstrumentation.getSpanId()); // matches /[0-9a-f]{16}/gi
  next();
});
// ...
```

> Throws an error if `expressZipkinInstrumentation(/* ... */)` was not called yet.

#### `.getTraceId()`

Retrieves the trace ID of the current request.

```javascript
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
const server = require('express')();
server.use(expressZipkinInstrumentation(/* ... */));
server.use((req, res, next) => {
  console.info(expressZipkinInstrumentation.getTraceId()); // matches /[0-9a-f]{16}/gi
  next();
});
// ...
```

> Throws an error if `expressZipkinInstrumentation(/* ... */)` was not called yet.


## Development
### Testing
Run tests using:

```bash
npm run test
```

To run them in watch mode:

```bash
npm run test-watch
```

### Continuous Integration
#### Environment Variables
The following environment variables have to be set in Travis for the pipeline to work

- `GH_USERNAME`: GitHub username
- `GH_ACCESS_TOKEN`: GitHub personal access token
- `NPM_PACKAGE_PUBLISH_NAME`: Package name to publish this as
- `NPM_REGISTRY_URL`: Hostname of NPM registry being used
- `NPM_TOKEN`: NPM access token
- `GIT_ORIGIN_REMOTE_PATH`: Path to repository in GitHub

## License

This package is licensed under the MIT license.