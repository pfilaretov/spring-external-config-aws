# spring-external-config-aws

Sample spring app with a configuration externalised to AWS Parameter Store. 
Based on [this article](https://towardsaws.com/how-to-externalize-spring-boot-properties-to-an-aws-system-manager-parameter-store-2a945b1e856f).

## How to run

1. Login to AWS Console
2. Go to "My Security Credentials"
3. Create and download new Access Key
4. Install [AWS CLI](https://aws.amazon.com/cli/)
5. Configure AWS CLI with Access Key created earlier:
    ```
    aws configure
    ```
   This wil create `<user_home>/.aws/credentials` file with access key details
6. Go to Systems Manager Parameter Store
7. Create three standard string parameters:
   ```
   /config/application/server.port = 8442
   /config/springExternalConfigAws/management.endpoints.web.exposure.include = env
   /config/springExternalConfigAws/my/useful/param = super-value
   ```
8. You may want to add `AWS_EC2_METADATA_DISABLED=true` env var to see less EC2 exception stack traces 
   during the application startup
9. Run spring-boot app
10. It should print values of `my.useful.param` and `management.endpoints.web.exposure.include` properties
11. Variable values can be found at actuator endpoint here: http://localhost:8442/actuator/env