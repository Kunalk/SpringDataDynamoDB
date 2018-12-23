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

Run the above application on 8080.

Helpful - 

Configure the repository as -->
@EnableScan
public interface CustomerRepository extends CrudRepository<Customer, String> {

@Autowired
	CustomerRepository repository; --> defines the repository for DynamoDB
  
Configure the bean to inject as repository config
@Bean
	public AmazonDynamoDB amazonDynamoDB() {
		AmazonDynamoDB dynamoDB = new AmazonDynamoDBClient(amazonAWSCredentials());

		if (!StringUtils.isNullOrEmpty(dBEndpoint)) {
			dynamoDB.setEndpoint(dBEndpoint);
		}

		return dynamoDB;
	}

	@Bean
	public AWSCredentials amazonAWSCredentials() {
		return new BasicAWSCredentials(accessKey, secretKey);
	}
  
 Operations -->
  
repository.deleteAll(); --> delete all data

-- to save record or list
repository.save(new Customer("JSA-1", "Jack", "Smith"));

repository.save(Arrays.asList(new Customer("JSA-2", "Adam", "Johnson"), new Customer("JSA-3", "Kim", "Smith"),
				new Customer("JSA-4", "David", "Williams"), new Customer("JSA-5", "Peter", "Davis")));
  
 Find a list
 Iterable<Customer> customers = repository.findAll();
  
 find a record
 repository.findOne(id).toString();
 
 custom find methods
 repository.findByLastName(lastName)
 
  -----------------------------------------------------------------
  finally access your application -->
  http://localhost:8080/springdynamo/findall
