# Zipkin Instrumentation for Express

## Installation

```bash
npm add @govtechsg/express-zipkin-instrumentation --save;
```

## Usage

```javascript
const server = express();
// ...
const expressZipkinInstrumentation = require('express-zipkin-instrumentation');
server.use(expressZipkinInstrumentation(
  'serviceName',
  'http://zipkin.yourdomain.com'
))
```

- `"serviceName"` is the identifier of the application
- `"http://zipkin.yourdomain.com"` is the domain of the zipkin server. When this is not specified, the instrumentation will send the logs to the trace.

## License

This package is licensed under the MIT license.