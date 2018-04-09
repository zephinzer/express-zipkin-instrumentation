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

## Development
### Testing
Run tests using:

```bash
npm run test
```

### Continuous Integration
#### Environment Variables
The following environment variables have to be set in Travis for the pipeline to work

- `GH_USERNAME`: GitHub username
- `GH_ACCESS_TOKEN`: GitHub personal access token
- `NPM_REGISTRY_URL`: Hostname of NPM registry being used
- `NPM_TOKEN`: NPM access token
- `GIT_ORIGIN_REMOTE_PATH`: Path to repository in GitHub

## License

This package is licensed under the MIT license.