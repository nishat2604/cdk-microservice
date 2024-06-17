# Initial commit
The  code is written in .Net Core  8.0  which basically  Create SQS and than  connected to Lambda function  which  write some smessage to DynamoDb  . There is another Lambda function  had been create which  regad the message from Dynamo Db  and send to  Geway API 
The CDK  Environment create the CDK
1) SQS creation
2) Lambda Function  read from SQL  and write to  Dynamo DB
3) Lambdat Fucntion  which  read from  Dynamo  DB and send to  API gateway
4) The API Gatway with  all the policy setting

Commnad used here 
dotnet build
dotnet run Src 

Package used here 
cd src
dotnet new lambda.SQS -o lambdas/SavePolicy
dotnet sln add .\lambdas\SavePolicy\src\SavePolicy
dotnet add .\lambdas\SavePolicy\src\SavePolicy package AWSSDK.DynamoDBv2

cd src
dotnet new lambda.EmptyFunction -o lambdas/ReadPolicy
dotnet sln add .\lambdas\ReadPolicy\src\ReadPolicy
dotnet add .\lambdas\ReadPolicy\src\ReadPolicy package AWSSDK.DynamoDBv2
dotnet add .\lambdas\ReadPolicy\src\ReadPolicy package AWSSDK.Lambda
dotnet add .\lambdas\ReadPolicy\src\ReadPolicy package Amazon.Lambda.APIGatewayEvents

# cdk-microservice
mkdir microservice
cd .\microservice\
cdk init -l csharp
cdk bootstrap
cdk synth
cdk diff 
cdk deploy
cdk destroy --  To clean  the infrastructure
 
# cdk-microservice
