## Chris Munns
- [Local Testing and Deployment Best Practices for Serverless Applications](https://www.youtube.com/watch?v=QRSc1dL-I4U)
- [Building CI/CD Pipelines  +for Serverless Applications](https://www.youtube.com/watch?v=dCDZ7HR7dms)
  * CodeStar
  * api gateway canaries
  * https://aws.amazon.com/serverless/serverlessrepo/
- [Building a Development Workflow for Serverless Applications](https://www.youtube.com/watch?v=e3lreqpWN0A)
  * Model your application and infrastructure resources
    + [AWS Serverless Application Model (SAM)](https://youtu.be/e3lreqpWN0A?t=577), released in fall 2016
    + ![SAM template](images/2018/01/sam-template.png)
  * [Configure multiple environments](https://youtu.be/e3lreqpWN0A?t=1163)
    + Same account, different stacks
    + Multiple account
      - AWS Organizations, released in 2017
  * Establish your testing/validation model
    + Code Inspection/Test Coverage:
      - Landscape https://landscape.io only for python
      - CodeClimate https://codeclimate.com
      - Coveralls.io https://coveralls.io
    + Mocking/stubbing tools
      - https://github.com/atlassian/localstack
        * https://github.com/spulec/moto
        * https://github.com/mhart/dynalite
        * https://github.com/mhart/kinesalite
    + Api UI testing
      - Runscope https://www.runscope.com
      - Ghost Inspector https://ghostinspector.com
  * Automate your delivery process
    + [An example minimal pipeline](https://youtu.be/e3lreqpWN0A?t=2186)
    + ![minimal pipeline](images/2018/01/minimal-pipeline.png)
  * [Demo](https://youtu.be/e3lreqpWN0A?t=2318)
    + [aws-serverless-samfarm](https://github.com/awslabs/aws-serverless-samfarm)

## Orr Weinstein
- [Authoring and Deploying Serverless Applications with AWS Cloud9](https://www.youtube.com/watch?v=pMyniSCOJdA)
  * Serverless IDE for Serverless development. Github integration already included and compatible with Eclipse via CodeStar! Also SSH from Cloud9 to EC2 instance
  * Useful keyboard shortcuts
    + Full screen (`Cmd + Shift + F`)
    + Cache file locally (`Cmd + S`)
    + Save UpdateFunctionCode (`Cmd + Shift + U`)
    + Test (`Cmd + I`)
    + Configure test event (`Cmd + J`)
  * [SAM Local](https://github.com/awslabs/aws-sam-local): CLI tool for local testing of serverless apps
    + leverage docker images to mimic Lambda's execution environment
    + `sam local generate-event s3 --bucket <bucket> --key <key>`
    + `npm install -g aws-sam-local`
    + written in go
      - `sam local`
      - `sam validate`
      - `sam package`
      - `sam deploy`
      - `sam help`
    + available in AWS Cloud9

## Serverless Sample app
- [Amazon Web Services - Labs](https://github.com/awslabs?utf8=%E2%9C%93&q=serverless&type=&language=)
  * [SpaceFinder - Serverless Auth Reference App](https://github.com/awslabs/aws-serverless-auth-reference-app)
    + How to Generate Client Code?
  * [AWSCognitoSampleDeveloperAuthenticationSample](https://github.com/awslabs/amazon-cognito-developer-authentication-sample)
  * [AWS Serverless Application Model (AWS SAM)](https://github.com/awslabs/serverless-application-model/blob/master/HOWTO.md)
    + AWS Serverless Application Model (AWS SAM) allows you to easily create and manage resources used in your serverless application using AWS CloudFormation.
  * [aws-cognito-apigw-angular-auth](https://github.com/awslabs/aws-cognito-apigw-angular-auth)
  * [aws-cognito-quicksight-auth](https://github.com/awslabs/aws-cognito-quicksight-auth)
    + [Secure API Access with Amazon Cognito Federated Identities, Amazon Cognito User Pools, and Amazon API Gateway](https://aws.amazon.com/blogs/compute/secure-api-access-with-amazon-cognito-federated-identities-amazon-cognito-user-pools-and-amazon-api-gateway/)
  * Android example code: https://docs.aws.amazon.com/cognito/latest/developerguide/using-amazon-cognito-user-identity-pools-android-sdk.html
  * how to use Cognito from the server side: https://github.com/kdgregory/example-cognito-java
    + example-cognito-java $ src/scripts/cognito-create-userpool.sh Example Example
    + User Pool ID:  us-east-1_2wc4ItB7S
    + Client ID:     6ejs2tnq2uopa4cjhiet7pvei9
      - The AWS Java SDK includes APIs to authenticate users in a User Pool. You can authenticate a user using either the InitiateAuth api or AdminInitiateAuth api of the AWSCognitoIdentityProviderClient class. The difference between these two API is explained in the documentation. In short, for InitiateAuth, you need to perform SRP calculations and then pass it to the API, while in AdminInitiateAuth you can directly pass the username and password. You can read about the security implications in both cases and decide which one to use.

## API reference
- **Read** the [Amazon Cognito Developer Guide](http://docs.aws.amazon.com/cognito/devguide/)
- **Read** the [Identity API Reference](http://docs.aws.amazon.com/cognitoidentity/latest/APIReference/Welcome.html)
- **Ask us questions** on the [Amazon Cognito Forums](https://forums.aws.amazon.com/forum.jspa?forumID=173) or open an issue on Github
- https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-integrate-with-cognito.html
  * **To use Amazon Cognito Federated Identities. Set the authorization type of your API to AWS_IAM**
    + Verify that AWS_IAM authorization settings are in effect by making a SigV4 signed request (such as through the Postman application using AWS Signature Authorization type) to the URL using IAM credentials from an IAM user that is a member of the group with the attached AmazonAPIGatewayInvokeFullAccess policy.
  * [Call an API Integrated with a User Pool](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-invoke-api-integrated-with-cognito-user-pool.html)
- [AWS Signature Version 4](https://docs.aws.amazon.com/apigateway/api-reference/signing-requests/)

# Amazon lambda
- Synchronous(push): Amazon API Gateway->lambda
- Asynchronous(event): Amazon SNS / S3 -> lambda
- Stream-based: DynamoDB / Kinesis -> lambda

AWS Lambda quickstart:
- https://www.youtube.com/watch?v=zaWxdVUFFcE
- /Users/xxiong003c/scala.workspace/HelloTest

# Amazon API gateway:
- https://www.youtube.com/watch?v=hUbS7-Jfhgs
- https://app.pluralsight.com/library/courses/scalable-aws-api-gateway/table-of-contents
- AWSCredentialsProvider https://youtu.be/e9B-eIAirZ4?t=1197
  * https://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/auth/AWSCredentialsProvider.html
  * [CognitoCredentialsProvider for android](https://github.com/aws/aws-sdk-android/blob/master/aws-android-sdk-core/src/main/java/com/amazonaws/auth/CognitoCredentialsProvider.java)
- [SwaggerHub AWS API Gateway Integration](https://www.youtube.com/watch?v=qsTKxD7pkPk)
- Kenn Brodhagen
  * [How to create a Request object for AWS API Gateway & Lambda](https://www.youtube.com/watch?time_continue=38&v=2Z-Utw_xl4c)
- Justin Pirtle
  * Intro: https://www.youtube.com/watch?v=AV24RTvbgWA
  * 2016 Demo: https://www.youtube.com/watch?v=n4hsWVXCuVI
  * 2017 Demo: https://www.youtube.com/watch?v=VZqG7HjT2AQ
  * MBL305
  * SID332: A Deep Dive on Amazon Cognito
    + https://www.youtube.com/watch?v=wlSba1dXAhc
  * SID343 Tim Hunt: User management and app Authentication with Amazon Cognito
  * SRV425: Serverless OAuth: Authorizing 3rd party app to your Serverless API
- API Gateway Access Policies
  * Action
    + "apigateway:\*"
    + "apigateway:GET"
    + "apigateway:POST"
  * Resource
    + arn:aws:apigateway:region::api-id:/stage-name/resource-path-specifier
  * AWS signature V4, required code included with SDK
  * API Key
    + writes to CloudWatch Logs
    + Per method
    + Not for authorization, better use the followings:
      - signed API calls
      - OAuth
      - Amazon Cognito user pool
      - https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-to-api.html
  * Throttling is achieved using API Keys
  * Three types of authorization
    + Amazon Cognito User Pools -> User Pools Authorizers
      - compatible with OpenId / SAML based
      - Cognito User Pools returns a JWT tokens {Identity, Access, Refresh}
      - Can't answer: Is this user an admin or basic user.
      - Can't answer: Can this user access certain type of operations
    + Amazon Cognito Federated Identities -> AWS IAM authorization
      - JWT
        * POST https://cognito-idp.us-east-1.amazonaws.com/
          + Headers
            - X-Amz-Content-Sha256:1f04075c3bb71ecc150421102cdf3d8fc57918316126e9d449c380b554e12abb
            - X-Amz-Target:AWSCognitoIdentityProviderService.InitiateAuth
            - X-Amz-User-Agent:aws-sdk-js/2.6.4
          + Request Body:
            ```json
            {
               "AuthFlow":"USER_SRP_AUTH",
               "ClientId":"2v9jjjin7sspgics9r9od61rve",
               "AuthParameters":{
                  "USERNAME":"user1",
                  "SRP_A":"a32e12f6d5c3bbc22380ae4ceb8726b147be24928b0639b9bdcb3b83f78cc7b162f83be58729102dc716e8048723f838d61503ae34f8cc6586eb39aa1f264d90f436f3cafc4ccbf10ca01ced8d22d9d020735d98ff41e90855e597f714b61afe3fed5202c4b5af6b7af70a77e7d7431b356d830735f32ea8e825c7a565bbd803e6eea1ae8738fe7d9906ab1f60ed213574c58c173f912d3a682003270e80934415c79a207896f97d8746eacdc8cd889a4a540b560f87884271b507018f3be10c6cd302a886ab8535424a78dedcbf7108bf37291a589b6bd0d9949fcc5e04a0132c591d76f75c483cb4ca13a2a9214cb3504c3c7c5fee2d05a73e76fc15bfa0d17026cca90aa0196e022b350b2b4a757096cbcd6092def8f11d381e191cba450051f9744903d0b21a8f63a8d6660ec7713379bca858bd12f821c131e8bac1e1ace03e5cd7039f2a4dbb6a979c5e2fbb2bd588a972df85d6d9ce266445f9e11016869a20cbd2a2a845658b093fc3db87e05a9eda8049c85eac1167e61aaae3695a"
               },
               "ClientMetadata":{

               }
            }
            ```
          + Response Body:
            ```json
            {
               "ChallengeName":"PASSWORD_VERIFIER",
               "ChallengeParameters":{
                  "SALT":"e59c6f9f14feb09fff6c7cbdec3c1b67",
                  "SECRET_BLOCK":"yFp55B9LuPaVIIYWE2xgyvRwyr16hy6r+eAfcKqwO7XTQyMSNQhOORmh3NxW3/Z/Won5BZGhtQNnVu8y4mosGpgWjhTSq6W9Apt/a26Se+tzuDDVegfsYOgXObCkv4zVOepE7IVu326bhYyLF1Kx9Tbv5bEHishu6bSD90e+MMP19mgTK0kcGhwh4P/39ClqXckVmxNA9hlF1YCZGbxgHAns3na8l1frBCFn6f4ix9TKsCYeWQgIACjl5XPdhHzfRWHXc0qTJtTwrnJSY9f79JZyjnxbi0U+C85wnoLhJzf3nVM85HQzcbIM7gaIwZPhSoZhEeGybWkvXfr529kVvtVSp0D8aNeFAG+LBEdT61JjpHHn22JSd0SzMGSTy0ue0mrd6n96eew36vxJnkljIM8TGzoVSwXMAPa2QWdhICNzURf4SIqgtmqkttZk/pK54F5lMayaEqA7LMS5OFJD25SueNv9W2SudNDZnfofAr9B3ecLP91zCwsGTNCFV0dpruMWA77fPq+kzXDFyAa056CGyZyTK9CEfYSbU+PgsOYJjgKLQ/LudDOyQCkvHzQSa8kRIjmVkVcIQhUseNY3urdzR6/zI36/GePSMgiRFC1KUaadqB7ZVypLAVK/bCOMo4Xdgb2GAehFZs75MRDUwr7jfKvOJ9K5Jtdq3yYgHhTQMr+JmSuP25BvZ+xmtbQqv7HmlsoFgsXvqTFlxCBhSjwatbDk+VbQ56m7BSPU1yflQQL5rEtALsTDGl38bCa306gCULiqzKc7fPFnb0Q/VvdA+JciR0X0ta43sUgMCrC/2YyyTgnLy23ktjFbr3IusOoWXgWuGyKP5ANhWRPDN+hH5cCAkc+XKWZlzBb+fccZSSZhCMneOzYe8Jb1giyEJZLciir5LIt+W+j8y9RSHP8Bp3i33wd9bfaYvoDPtNzUD7d3tjmICJ7PTB1odwVTlQMxk4RHAnYLgzRP2Lfe3vhNtW2RmY37zoiJ/lExl6DqEgxyeurh/3sHDgkb7q5+nAsNFDKYs1ghyQ2McCtdWRdtjtPkVJ9hnMCRBmMFEAos2RZTdfDjzSA0pAYILC2+J3mX1/6vc4jHoICrRn1FoPBZ1sBj9oy9Jz5Tf2CWX7yNfTnZk47s3L2yzx1Mx6MlIHXb7cnXAZrbq2FUDhgY578yQYWYfyXPRbsKIaqV0n7g98EXGXA5L+cXoil+7FG5JZNpHsnLJtwfLsLrSI8bFUXZpoZAiDSlaLGFGlMlAfD3areEL3i5rVZem6LeeE8cz/hEOhb4CnJWe0b57leEqzW7v7ZCCWSj31iCfErw5vkw4YKXF+4G8Kw1cNMbJsAi5kMf95oL88r4+Ua/lTdvOedudj5E5habEa4QAib+vQtiWktiWuY2JGaoRrd/6STn3xZo9rdBmai9XZIr/d8xmLx5mtgrpg4UIr7YFR155yeGPDt2SGIHaEqrNImiiakjwsk6R4zX1bS1mhxQpYFruscgxhCFF0XckROKi1sqxw9NBPG/nNs+vHh37t3r0Zh1hhD46XVDns8ZTy8GSr1/mJ2rOqjg4zMoanpalGJDNos6JgwEfm0zNhrKaI4f/419RSSwYt7rbW8TRE64hj1y+oGD8LE80RESmSbc26N0NDpsXXkasmC+wtlrOScfGlSKX8GDutapI4BRdmsOU1CPIXsi//aU2ogoHXqDedPCwfNYYFzi",
                  "SRP_B":"c69f27eb53ae4f3f9d556d7961a4ee26ecbe23e3f479c2801b8c18f35d09bcde2d6a1b921721600f8710b25b2fdc2ff3e06e8449e8d0b52f94f17c9703199d05c49c31847e0b611f5b3909d3c438b9777b90058b8813d49effa3a0302549e1c746f022db6b88675c6da811fbe6d2ff1d97ac182b9239b514d6f16193e25fb14b1e888a28ff2752e9c0b50926985706d05922e596028d3aef22ede5eeb7ec3a522a47455154307e0780fe7df80c6544be53c132dcbca63f5eb37dae61541dd3ad63e3d6110a3e2d84a72d4a8551da584024b70b402e5048e2c871193821008658793be56af873cd5e24c559ca0cc74acf24dfacff54a9cdae02cba08cfe4d4dc267b3ac9dc55fe20de125525b984df540deeef806ea1c3a87f06403bdac1ea2815c9969faac93db2f65c04b47e8035c22e7a88889c34d23ce9d34b8c73609faab5a3e4d17ac6aab7bc733fb2cb22043d5a87950fa011dbdadc20adf2fbc6d416706ee20fc4a52f996ff263a8ec6c08fe0fe7f01739521d2dd9dfcac09150c8c5f",
                  "USERNAME":"user1",
                  "USER_ID_FOR_SRP":"user1"
               }
            }
            ```
        * POST https://cognito-idp.us-east-1.amazonaws.com/
          + Headers
            - X-Amz-Content-Sha256:2e95578e9d942f8a54ad709e7b52f04497a9c0e1c5d02b064bf527d21e1d2a3d
            - X-Amz-Target:AWSCognitoIdentityProviderService.RespondToAuthChallenge
            - X-Amz-User-Agent:aws-sdk-js/2.6.4
          + Request Body
            ```json
            {
               "ChallengeName":"PASSWORD_VERIFIER",
               "ClientId":"2v9jjjin7sspgics9r9od61rve",
               "ChallengeResponses":{
                  "USERNAME":"user1",
                  "PASSWORD_CLAIM_SECRET_BLOCK":"yFp55B9LuPaVIIYWE2xgyvRwyr16hy6r+eAfcKqwO7XTQyMSNQhOORmh3NxW3/Z/Won5BZGhtQNnVu8y4mosGpgWjhTSq6W9Apt/a26Se+tzuDDVegfsYOgXObCkv4zVOepE7IVu326bhYyLF1Kx9Tbv5bEHishu6bSD90e+MMP19mgTK0kcGhwh4P/39ClqXckVmxNA9hlF1YCZGbxgHAns3na8l1frBCFn6f4ix9TKsCYeWQgIACjl5XPdhHzfRWHXc0qTJtTwrnJSY9f79JZyjnxbi0U+C85wnoLhJzf3nVM85HQzcbIM7gaIwZPhSoZhEeGybWkvXfr529kVvtVSp0D8aNeFAG+LBEdT61JjpHHn22JSd0SzMGSTy0ue0mrd6n96eew36vxJnkljIM8TGzoVSwXMAPa2QWdhICNzURf4SIqgtmqkttZk/pK54F5lMayaEqA7LMS5OFJD25SueNv9W2SudNDZnfofAr9B3ecLP91zCwsGTNCFV0dpruMWA77fPq+kzXDFyAa056CGyZyTK9CEfYSbU+PgsOYJjgKLQ/LudDOyQCkvHzQSa8kRIjmVkVcIQhUseNY3urdzR6/zI36/GePSMgiRFC1KUaadqB7ZVypLAVK/bCOMo4Xdgb2GAehFZs75MRDUwr7jfKvOJ9K5Jtdq3yYgHhTQMr+JmSuP25BvZ+xmtbQqv7HmlsoFgsXvqTFlxCBhSjwatbDk+VbQ56m7BSPU1yflQQL5rEtALsTDGl38bCa306gCULiqzKc7fPFnb0Q/VvdA+JciR0X0ta43sUgMCrC/2YyyTgnLy23ktjFbr3IusOoWXgWuGyKP5ANhWRPDN+hH5cCAkc+XKWZlzBb+fccZSSZhCMneOzYe8Jb1giyEJZLciir5LIt+W+j8y9RSHP8Bp3i33wd9bfaYvoDPtNzUD7d3tjmICJ7PTB1odwVTlQMxk4RHAnYLgzRP2Lfe3vhNtW2RmY37zoiJ/lExl6DqEgxyeurh/3sHDgkb7q5+nAsNFDKYs1ghyQ2McCtdWRdtjtPkVJ9hnMCRBmMFEAos2RZTdfDjzSA0pAYILC2+J3mX1/6vc4jHoICrRn1FoPBZ1sBj9oy9Jz5Tf2CWX7yNfTnZk47s3L2yzx1Mx6MlIHXb7cnXAZrbq2FUDhgY578yQYWYfyXPRbsKIaqV0n7g98EXGXA5L+cXoil+7FG5JZNpHsnLJtwfLsLrSI8bFUXZpoZAiDSlaLGFGlMlAfD3areEL3i5rVZem6LeeE8cz/hEOhb4CnJWe0b57leEqzW7v7ZCCWSj31iCfErw5vkw4YKXF+4G8Kw1cNMbJsAi5kMf95oL88r4+Ua/lTdvOedudj5E5habEa4QAib+vQtiWktiWuY2JGaoRrd/6STn3xZo9rdBmai9XZIr/d8xmLx5mtgrpg4UIr7YFR155yeGPDt2SGIHaEqrNImiiakjwsk6R4zX1bS1mhxQpYFruscgxhCFF0XckROKi1sqxw9NBPG/nNs+vHh37t3r0Zh1hhD46XVDns8ZTy8GSr1/mJ2rOqjg4zMoanpalGJDNos6JgwEfm0zNhrKaI4f/419RSSwYt7rbW8TRE64hj1y+oGD8LE80RESmSbc26N0NDpsXXkasmC+wtlrOScfGlSKX8GDutapI4BRdmsOU1CPIXsi//aU2ogoHXqDedPCwfNYYFzi",
                  "TIMESTAMP":"Mon Jan 8 19:43:42 UTC 2018",
                  "PASSWORD_CLAIM_SIGNATURE":"cSDoFZLXDui+tR6LtT1NJX0LNWHmpyg0ojAbEZAzkP8="
               }
            }
            ```
          + Request Response
          ```json
          {
             "AuthenticationResult":{
                "AccessToken":"eyJraWQiOiJYMitiWWJTclI3ZDIyTkVVUThoMFV4SzdxR2tRSVZZRkFmY0p4Vm5RUUhBPSIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiI2MzdiYmZhMC1mNjhjLTQ0NGEtYTc1Yy05ZmQ5ZDM2OGY2YTciLCJjb2duaXRvOmdyb3VwcyI6WyJjbGllbnRHcm91cCJdLCJldmVudF9pZCI6IjNiOTI1ZmI4LWY0YWMtMTFlNy1hYWQ3LTU1ODI1MTZkYmIxMSIsInRva2VuX3VzZSI6ImFjY2VzcyIsInNjb3BlIjoiYXdzLmNvZ25pdG8uc2lnbmluLnVzZXIuYWRtaW4iLCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAudXMtZWFzdC0xLmFtYXpvbmF3cy5jb21cL3VzLWVhc3QtMV94d0hnNU1XdnIiLCJleHAiOjE1MTU0NDQyMjMsImlhdCI6MTUxNTQ0MDYyMywianRpIjoiNjlkMzFlMGMtOTM0NC00YjIzLTkxNmQtYzUxMjQ0MTlhMjQyIiwiY2xpZW50X2lkIjoiMnY5ampqaW43c3NwZ2ljczlyOW9kNjFydmUiLCJ1c2VybmFtZSI6InVzZXIxIn0.lcL30jWH0IBQa1Lah_TMTX3EQ8MEwYy3oCyU0-Uta9-ftXg1KiA-G6yi4cmbj8ZNrw28LBAsI5vXBDjeXxvcF1EXi0Ql5vbt0Imsuw1gNoJ2uRQWmSkcl57RpSZgtf5RYgIZG4PXmmONy8hBRaNAagI-f3wM82FvAAFdOnGeGud1emgRPPK_XrYNJwVRoEp0AiBI-HQ8q5Zd07hhi9gM5qUNfSV-ECNwi2Jr7j_KCmYo22JnHfBMU3TCUAB1MPCBktTVApUWIAW3PH9O3fqJVjM3QxLkVa4pzOXcE6eevVWsgHFjxwk1qkcdEegb9jHBIlfVkV3Ig4CjuJxySanRVQ",
                "ExpiresIn":3600,
                "IdToken":"eyJraWQiOiJaQ2t3NEU2eHVxMU5ISlwvTWl0bEJuR2lta21YSFQzN3NXcXZvZWs5WkdWUT0iLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiI2MzdiYmZhMC1mNjhjLTQ0NGEtYTc1Yy05ZmQ5ZDM2OGY2YTciLCJjb2duaXRvOmdyb3VwcyI6WyJjbGllbnRHcm91cCJdLCJjb2duaXRvOnByZWZlcnJlZF9yb2xlIjoiYXJuOmF3czppYW06OjUyNDU5NDA1MDE4OTpyb2xlXC9zcGFjZWZpbmRlci1kZXZlbG9wbWVudC1zLUNvZ25pdG9JZGVudGl0eVBvb2xBdXRoUy1RMUVKU0RKM1VBNDEiLCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAudXMtZWFzdC0xLmFtYXpvbmF3cy5jb21cL3VzLWVhc3QtMV94d0hnNU1XdnIiLCJjb2duaXRvOnVzZXJuYW1lIjoidXNlcjEiLCJnaXZlbl9uYW1lIjoiU2FtcGxlIiwiY29nbml0bzpyb2xlcyI6WyJhcm46YXdzOmlhbTo6NTI0NTk0MDUwMTg5OnJvbGVcL3NwYWNlZmluZGVyLWRldmVsb3BtZW50LXMtQ29nbml0b0lkZW50aXR5UG9vbEF1dGhTLVExRUpTREozVUE0MSJdLCJhdWQiOiIydjlqamppbjdzc3BnaWNzOXI5b2Q2MXJ2ZSIsImV2ZW50X2lkIjoiM2I5MjVmYjgtZjRhYy0xMWU3LWFhZDctNTU4MjUxNmRiYjExIiwidG9rZW5fdXNlIjoiaWQiLCJhdXRoX3RpbWUiOjE1MTU0NDA2MjMsImV4cCI6MTUxNTQ0NDIyMywiaWF0IjoxNTE1NDQwNjIzLCJmYW1pbHlfbmFtZSI6IlVzZXIiLCJlbWFpbCI6InVzZXIxQGV4YW1wbGUuY29tIn0.WFYuIyDYgzmgXUzgYQAdSWdQCBTNMZJQutQXl4z2LcJQvfEsXO-wslyXKLuRXj1G4CDbknTxyOTg9djYYdzP_HAdL-3pumEdIIpw0KMiwYrnQhzvmmTVuFPY_I9YkNhRx0vky75Dj46trCpv8DmD1SK7mbqrGXkkPzdtM-3-j6Ep3mrErkQQDKMXsEUvkOIue6BAjgI4Y9BZKu_tgHfEDXHfPtRy4S7QXVdvWohrNeLaOOk377MA8gum0VBr2NB88px40Pf3ENjj6eK4aLLcye-o4WRTik2xuPyAH5la3yUNWKKfSZAGnSqnmkWYmRL9Csh3Ckga_jsnKOMWnZ02nQ",
                "RefreshToken":"eyJjdHkiOiJKV1QiLCJlbmMiOiJBMjU2R0NNIiwiYWxnIjoiUlNBLU9BRVAifQ.lQRiRvb5M4PYlyTnf_PGT_scnleYxdcNwEHl4Y-bqj-fS_9Fo74dSPCar7bj84DSUbMKPOSGgZrONkUOzuTgrE_txcRRFjSE7mXaPqHbuvDhFG_rVEeqrPoeTYifYnItb-UFalwLYOrdhkyik7lrXpVCxWES3QJ0aGB51vXGsPJf7LsTgVHxHgPOW6Qpnh5XsoBqD8eit1nExzcDUUc5AUjqTAYAwsjCIztbuPk0E9utsJerALZgdAf6VzY4lPJOBvGhV8cwwB4sDwLthiayEFoTI6v95baYozvL-PpMdZDn0DGANs4bdtHRzoaWWTYw2C8maNni1-pHsFK9NXViTw._qkVFqSbEyMwA08B.ybxp9aa0Q0F00sEaxd0RLZOR8_qK_73_M-OrSulxcE-jqGO6e6BHfVtcDucHhmNM5IjPgl18lXr-RB9QwRRJocQtCAF5_h75MviD1JmPX1fg9oES6VZD52rWI6XL9kivI9Y2zUqL8j1rLp2ukNA31AwzRiSEhRnvTJjHmO7OLXhmBuCp0Tm1ipcN0yjAGsi2D7lrHsNVSjtAgAsx7oI03mtpi09GRegU2AhhhUGJ9ltXIl8jqWLRf8J26hJChNaMUZ-ErqG3ocsiezOYpSh3RdliiwZOdJYAPbixi5WniaovfybxwdvcH_4kGwFfgmEXWGYKeItbV7q7mXlFIttWa0yEA31hFmSAN2_dF1xJPw_Ws9ZAtEj0an4HH2Y4kQsE5kW8Esy8rQGyqEjglU4EgHbayjxL4ngcEG1DaljVAvh-W_OjZ70c6-ClBGbqAmfizTEymwUvQ2WoGMmS4qIONy2eASjroR60kGurk6krhrDpwL9sXIWtB9HO_k-dUCGmiDGHVp_qHoFwEyq1dvraZ4kcC_r27LLWu4W_4iFsLaWk5_Bu8hOb1vw20NGlsQikMRy1KcJUwaNp76BRPfLI7epCkXYGYeEZLHTIFWdA2XRItdEylhQO9flnXzgvy7J1YJVadhKSiG1-9pCXtetwklG91xLTx1Oc0PRjQ_wjKod7UMa6_mEdVyMemurjX6TuO9rUlmtDFPrGceFYzmRGL3xqsDyWVxYmtT_7f3AvkHpWKVPPzAAHp4ijINwjDSw-OeCDwQRaFiiQfj4IoAmVga0yx8Ix-H2Us2jVN6G7Qb_GJ1Hjh-zj3S-i0n2PTJkXISuxQasPCNGEA8hBmQewxlEf4iD10KUrq39Jy8l2VCSyQSqe1AMovYXBRDKkDkfDLMq0PrYCJNtXiADnXxqqF3SC93jl1Ukp7VqaEzipZ37DDg8WWx6aehFhXxcwv9nL7wtn8tBo5oDgAI0lyz3UeTHqj-pgFSSmw4Yiy2kPwiceOmTVOR7rZimoUttBPbaiPJk-1mJcxyYspxL0LbgGttzbzUe13DfkP5gHafAC4JHYsWNWoWEfV80-nDoYCl4say-SwPS0-bwh9xYZPypku43JYlfEbLpc07U8tIKSJ5JKnOFokx9cDy8M0z8iVkAmlLCidS1-sP2jLEHKrcgYurNfWWSsX4ApEoZskY4HvXA9Kelj_aqbhiIrvnhcX4Dv_6mr71DGiOWW0CST-a2cTGpF6Dc.jrpbvOCHTQwRO1W5nsbFbw",
                "TokenType":"Bearer"
             },
             "ChallengeParameters":{

             }
          }
          ```

      - after JWT token, client request AWS scoped credentials
        * POST https://cognito-identity.us-east-1.amazonaws.com/
          + Request Headers:
            - X-Amz-Content-Sha256:08eeeb9126b9ce8e65a1e8ac4b1889e5e3ea2e6d848208e529523ebdf7a24cc3
            - X-Amz-Target:AWSCognitoIdentityService.GetId
          + Request Body:
            ```json
            {
               "IdentityPoolId":"us-east-1:36d52ea3-26a9-4d70-9ba9-a75c75c69efb",
               "Logins":{
                  "cognito-idp.us-east-1.amazonaws.com/us-east-1_xwHg5MWvr":"${Cognito User Pools Identity Token}"
               }
            }
            ```
          + Response Body:
            ```json
            {
               "IdentityId":"us-east-1:1666ff8c-8ddf-42c8-9109-07e2dfd3848c"
            }
            ```
        * POST https://cognito-identity.us-east-1.amazonaws.com/
          + Request Headers:
            - X-Amz-Content-Sha256:d974d5d5221000d6b6a8fdc76188a2ac23a229b592ce61cfebd7ee771d7ef515
            - X-Amz-Target:AWSCognitoIdentityService.GetCredentialsForIdentity
          + Request Body:
            ``` json
            {
               "Logins":{
                  "cognito-idp.us-east-1.amazonaws.com/us-east-1_xwHg5MWvr":"${Cognito User Pools Identity Token}"
               },
               "IdentityId":"us-east-1:1666ff8c-8ddf-42c8-9109-07e2dfd3848c"
            }
            ```
          + Response Body:

            ```json
            {
               "Credentials":{
                  "AccessKeyId":"ASIAJD46T43UEJKFRHIQ",
                  "Expiration":1.515115602E9,
                  "SecretKey":"5bGQfuq+NTWlSxp99smYvNrBfSDa6yEb/ECZsabX",
                  "SessionToken":"AgoGb3JpZ2luENT//////////wEaCXVzLWVhc3QtMSKAAnv+8hR1wNYao/69bjkR+fh85Ylsi0hRIzOkONt1WBdgbjMZF/LkllUjM12veheuD0nEiwMOS5K4LYZ7NKFv/pMVi8t3+K9jx5oAqOvqdmZj3eQOofkpot7ZZu55d84lpPHvuMG95hhKhaVKfdCd6dxZp3RpF9ovpRw0z9YZWf2xUcL701+9HJhqM5TXMHe0BwC6mrd7ZiokcdGJ2MY6N/qEQ2IcWFV5Duq6qIsV+x1xelvkmgIQiwcwTNvth9kcurndDDYOjiqp3MyPqGx1PkzFqo8ruvgMSOZWys4R5/oETPWa15gj26kK5A8EdPOFgghT8wC8UnQE2dO5tW4RI20qpgUIahAAGgw1MjQ1OTQwNTAxODkiDCumUcMgdH/sLtRxbiqDBciISBFmweIRwfL/Hz4Ae+Hdjgz4gPnXTeFbbWroWrBmsgcXiUyJ0PCLkFKqIfR5UmeHciycn0CKUXpFcPJHVzEJVH1X5YMvYsNHDaNKRF+QHr7ZJFbc0k7HhryDJ0tNeK7fpuydYY2pzHfmdy6plSVD7FSpcZ+Im/noXnpY1ygVAwH59PzE4VBf7dTwOH0ZoL/1U1LCOTHnnTsq+0Zx1itavE7RtW/YZETtmVukuvsxrLSreXVolrMkrL6F529aUNZtmiCDZ+cwCnzRzsEdJXe2bXMORHrM7rIVx32FJICT3Ndu+bj60ZAGWIkH/FbsYx+QHEzDeIYOc6E5QnIgHxC9Yg3bWvUfjQwZHXSvgn8cyDZuNSaQJnueIWmly41R2lW/euMi5JXgqxEgw7yjoZptwULOtnhKzyik1VUBLyV1jzUyFjtcSwu/tZF75fahs6wF1/weaMB0Ys4MCwdyVynX88xerdybVCy4DV9rQxJQKboHyFhewKrjyQvHp/LOirduFZafS+0R6FEEvhtkj1vxnobOca8pv3YA7xnaz9aendcO4dXcLIhdtHKkfdQWCEBc0mXSmtdbF7MyPtv+HKPfv9Sv/wQUHCtfyX/Sxx06Wa9JsBLDpiXdvDD+E453M/YesM+vs/sJ6KmdBaKBH+OACVYsi7gbOIIMOBUZft99KJw1aBqKB9lTyEp9tBQ5J/6lnrhnwuRRRWge2MZmRb45tf0cP2Q79335muBKvar8S+kPDva40HVtyOY9QP2ixp+sFELWUEifbiX9T5NMjbxF0S0yPuu4+EMQiLWGGcLQUuGtVMj57IYXZUxY9N2+5gYYIv4TqifB3smeY+uW8cdwun8wwoy70gU="
               },
               "IdentityId":"us-east-1:1666ff8c-8ddf-42c8-9109-07e2dfd3848c"
            }
            ```

      - Cognito Federated Identities returns Temp AWS credentials
      - Client sign (Sig V4) the request, API gateway check IAM policy
        * Request headers:
          + authorization: AWS4-HMAC-SHA256 Credential=ASIAJD46T43UEJKFRHIQ/20180105/us-east-1/execute-api/aws4_request, SignedHeaders=accept;content-type;host;x-amz-date, Signature=7b9329254adf55e948d2cdd70a3fa5f94940fefa4bfe72c85e4c413a07626e86
          + x-amz-date: 20180105T002642Z
          + x-amz-security-token: SessionToken from previous response
        * Authenticated Users
          + Default role
          + Choose role from rule
          + Choose role from token (particularly for Cognito User Pools)
            - Cognito Groups: a user can be in more than one group
    + Custom Identity Provider -> Custom Authorizers

# [Auditing and Logging](https://youtu.be/AV24RTvbgWA?t=2166)
## [AWS CloudTrail (Records AWS API calls for your account)](https://youtu.be/AV24RTvbgWA?t=2279)
- Who made the API call?
- What was the API call?
- When was the API call made?
- Where was the API call made from and made to?
- Which resources were acted upon in the API call?


## [AWS config](https://youtu.be/AV24RTvbgWA?t=2302)
- Get inventory of AWS resource
- Record configuration changes continuously
- Discover new and deleted resources
- Get notified when configuration change

## Programming Amazon Cognito ([by far the worst-documented Amazon service](https://github.com/kdgregory/example-cognito-java))

## AWS Step Functions
Andy Katz: [Serverless Orchestration with AWS Step Functions](https://www.youtube.com/watch?v=8rmgF-SbcIk)
