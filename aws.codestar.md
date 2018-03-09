## [AWS CI, CD workflow](https://www.udemy.com/continuous-delivery-on-aws/learn/v4/t/lecture/6592220?start=0)

### CodeCommit
- Git Basics
  * Git keeps snapshots, not differences

### AWS_IAM
- Attach Policy
  * IAMSelfManageServiceSpecificCredentials: enable https

### CodeBuild
- sources:
  * CodeCommit
  * Github
  * S3: should be in the same region
- build environment
  * pre-configured docker images
  * go, java, nodeJs, python, ruby, android
- buildspecs.yml
  * Main sections:
    + version
    + variables: optional
    + phases
      - install
      - pre_build
      - build
      - post_build
    + artifacts: optional

### Serverless Application Model

### Lambda
- Lambda Versioning
  * alias is associated with a version
  * clients use aliases instead of version
  * version is recommended when automating lambda deployment

### CodePipeline
- Usage
  * Use CodePipeline for
    + Infrastructure updates
    + Applications on managed servers
    + Serverless stack-level updates
    + When a release workflow is needed
  * Do NOT use CodePipeline for
    + Serverless components code updates
    + Static content updates, content delivery
    + When workflow is not needed
- Types of Serverless Apps Changes
  * Serverless stack updates(SAM)
    + Adding resources (lambda, API or tables)
    + Changing source code file in SAM
    + CodeBuild and CodePipeline could be utilized
  * Serverless resources updates
    + Update lambda code
    + Update API swagger definition
    + CodeBuild and CodePipeline can't be used
    + CLI, S3, lambda are faster approaches for CD

### CodeStar
