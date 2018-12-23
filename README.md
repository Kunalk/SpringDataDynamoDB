# SpringDataDynamoDB
SpringDataDynamoDB


This project uses springdata jar to connect to dynamo DB instead of explicitly creating connection with aws-sdk files.

This requires runnin dynamodb version locally or on server.

Copy DynamoDB from - https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.DownloadingAndRunning.html

After you download the archive, extract the contents and copy the extracted directory to a location of your choice.

To start DynamoDB on your computer, open a command prompt window, navigate to the directory where you extracted DynamoDBLocal.jar, and type the following command:

java -Djava.library.path=./DynamoDBLocal_lib -jar DynamoDBLocal.jar -sharedDb

Before you can access DynamoDB programmatically or through the AWS Command Line Interface (AWS CLI), you must configure your credentials to enable authorization for your applications. Downloadable DynamoDB requires any credentials to work. For example:

AWS Access Key ID: "fakeMyKeyId"
AWS Secret Access Key: "fakeSecretAccessKey"

You can start writing applications. To access DynamoDB running locally, use the --endpoint-url parameter. For example, use the following command to list DynamoDB tables:

aws dynamodb list-tables --endpoint-url http://localhost:8000
