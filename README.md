# Module 3.15 Application Logging with Cloudwatch
David Module 3.15 Assignment with OIDC and Cloudwatch Logs on serverless express framework

## What are being used ?
- node.js express
- dependencies : express, jest, winston, and serverless
- OpenID Connect for AWS IAM deployment
- Github actions CI/CD pipeline

## Steps
- Create new IAM Identity Provider with token.actions.githubusercontent.com
- Create IAM role on AWS console with proper permission to run the service involved
- Add application logging source code with winston on index.js
```js
const express = require("express");
const winston = require("winston");
const app = express();
const port = 3000;
const logger = winston.createLogger({
  // Log only if level is less than (meaning more severe) or equal to this
  level: "info",
  
  // Use timestamp and printf to create a standard log format
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.printf(
      (info) => `${info.timestamp} ${info.level}: ${info.message}`
    )
  ),
  
  // Log to the console and a file
  transports: [
    new winston.transports.Console(),
    ],
});


app.use((req, res, next) => {
  // Log an info message for each incoming request
  logger.info(`Received a ${req.method} request for ${req.url}`);
  next();
});

// Handle HTTP GET requests to the root path
app.get("/", (req, res) => {
  // Log messages at different log levels
  logger.log("error", "This is an error message - David Function");
  logger.log("warn", "This is a warning message David Function");
  logger.log("info", "This is an info message David Function");
  logger.log("verbose", "This is a verbose message David Function");
  logger.log("debug", "This is a debug message David Function");
  logger.log("silly", "This is a silly message David Function");
  
  // Send a response to the client
  res.send("Hello, world!");
});

// A route for manually triggering an error
app.get("/error", (req, res, next) => {
  throw new Error('This is a test error');
})

// Handle errors using the logger
app.use((err, req, res, next) => {

  // Log the error message at the error level
  logger.error(err.message);
  res.status(500).send();
});

// Start the app and listen on the specified port
 app.listen(port, () => {
  logger.log("info", `App listening on port ${port}!`);
});
```


## Reference
For OIDC Setup :

- https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services

- https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/


