## [Code Along - AWS Lambda, Step Functions and Serverless](https://www.udemy.com/code-along-serverless-framework-step-functions/learn/v4/overview)
- [code](https://bitbucket.org/shreya5/atm-finder-serverless-step-functions/overview)
- [test data](https://gist.github.com/runtimeZero/06e75fd7865320c9cb5c1c0f30d3a078)
- [slack incoming webhooks](https://api.slack.com/incoming-webhooks)

```bash
# install nvm https://github.com/creationix/nvm/blob/master/README.md#installation
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
# install node 6.10.3 LTS which amazon uses
nvm install 6.10.3
# change the default node version to 6.10.3
nvm alias default 6.10.3

# install serverless to ~/.nvm/versions/node/v6.10.3/bin/serverless
npm install -g serverless
serverless config credentials --provider aws --key ################# --secret #################
# or add a default profile manually at ~/.aws/credentials
# Lodash makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, strings, etc
npm init
npm install aws-sdk lodash request --save
npm install @google/maps --save
npm install algoliasearch --save
# create a serverless project
mkdir atm-finder
cd atm-finder
serverless create -t aws-nodejs
serverless deploy
serverless invoke -f firstRun
serverless deploy function -f firstRun
```

- callback
  * when in Step Function, callback is where you pass info to the next function
  * callback will not be returned until event queue is cleared

```javascript
module.exports.firstRun = (event, context, callback) => {
  // event is the input to the function
  console.log(context.functionName); // context has info about memory, timeout and other settings etc.
  fetch(url, function(data){}); // callback will be called after fetch finish
  callback(null, "First Excution"); // first item is error
};

module.exports.firstRun = (event, context, callback) => {
  let i = 5;
  setTimeout(function(){
    i = 10;
  })
  callback(null, "First Excution: " + i); // "First Excution: 5"
  // callback is evaluated but not returned
};

```


### serverless meetup March 29, 2018
- serverless features
  * pay-per-execution
  * auto-scaling
  * zero-administration

- component
  * APIGateway
  * Lambda
  * DynamoDB

- benefits
  * reusability
    + cost
    + scale
    + overhead
  * cloud abstraction
    + AWS
    + azure
    + gcp
  * vendor choice
    + Route53
    + Netlify
    + FireStore
    + Event APIGateway
    + Auth0

- component, search github retail-app/serverless.yml
  * github.com/serverless/serverless-components
  * serverless.yml
    ```ymal
    type: my-component

    inputTypes:
      bar:
        type: numbers
        required: false
    ```
  * index.js (optioal)
    ```javascript
      const deploy = (input, context) =>{
        // provisioning logic goes here
      }
      const remove = () => {
        // unprovisioning logic goes here
      }
      module.exports = {
        deploy,
        remove
      }
    ```

- Node.js and IoT is like peanut butter and jelly
  * Johnny-Five
  * Cylon.js
  * awesome-iot
  * resin.io
  *
