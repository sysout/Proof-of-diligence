## [Code Along - AWS Lambda, Step Functions and Serverless](https://www.udemy.com/code-along-serverless-framework-step-functions/learn/v4/overview)
```bash
npm install -g serverless
serverless config credentials --provider aws --key ################# --secret #################
# or add a default profile manually at ~/.aws/credentials
npm install aws-sdk lodash --save
npm install @google/maps --save

serverless create -t aws-nodejs
serverless deploy
serverless invoke -f firstRun
serverless deploy function -f firstRun
```

```javascript
module.exports.firstRun = (event, context, callback) => {
  // event is the input to the function
  console.log(context.functionName); // memory and other settings etc.
  callback(null, "First Excution"); // first item is error
  // when in Step Function, callback is where you pass info to the next function
  // callback will not be called until all event queue are cleared
};
```
