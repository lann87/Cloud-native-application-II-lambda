Q1: You want to build and deploy code functions in the AWS Cloud, but do not want to manage the infrastructure - Which of the following services can help meet this requirement?

A - AWS EC2

B - AWS API Gateway

C - AWS Lambda

D - AWS DynamoDB

---

Q2: You currently have a set of Lambda functions which have business logic embedded in them. You want customers to have the ability to call these functions via HTTPS. How can this be achieved?

A - Use the API Gateway and provide integration with the AWS Lambda functions.

B - Enable HTTP access on the AWS Lambda functions.

C - Add EC2 Instances with an API server installed. Integrate the server with AWSLambda functions.

D - Use S3 websites to make calls to the Lambda functions

---

Q3: A company wants to build a brand new application on the AWS Cloud. They want to ensure that this application follows the Microservices architecture. Which of the following services can be used to build this sort of architecture? Except?

A - AWS Lambda

B - AWS ECS

C - AWS API Gateway

D - AWS Config

---

Q4: Which AWS CLI command invokes a function?

A - aws lambda invoke --function ReturnBucketName outputfile.txt

B - aws lambda execute --function-name ReturnBucketName outputfile.txt

C - aws lambda invoke --function-name ReturnBucketName outputfile.txt

D - aws lambda execute --function ReturnBucketName outputfile.txt

---

Q5: What adds tracing capabilities to a Lambda?

A - AWS Trace

B - CloudStack

C - CloudTrail

D - AWS X-Ray

---

Q6: How can a developer provide Lambda code?

A - by uploading a .zip file

B - all of these answers

C - by editing inline

D - from an S3 bucket

---

Q7: You are performance-testing your Lambda to verify that you set the memory size adequately. Where do you verify the execution overhead?

A - CLoudWatch logs

B - DynamoDB logs

C - S3 logs

D - Lambda logs.

---

Q8: You need to use a Lambda to provide backend logic to your website. Which service do you use to make your Lambda available to your website?

A - S3

B - API Gateway

C - X-Ray

D - DynamoDB

---

Q9: What is AWS best practice for Lambda configuration?

A - Overprovision memory to run your functions faster and reduce your costs. Do not overprovision your function timeout settings.
 
B - Overprovision memory and your function timeout settings to run your functions faster and reduce your costs.
 
C - Do not overprovision memory. Overprovision your function timeout settings to run your functions faster and reduce costs.
 
D - Do not overprovision memory. Do not overprovision your function timeout settings to run your functions faster and reduce costs.

---

Q10: How do you stop a running Lambda that is stuck in a recursive loop?

A - Delete the function.

B - Set the function concurrent execution limit to 0 while you update the code.

C - Reset the function.

D - Set the function concurrent execution limit to 100 while you update the code.

---
