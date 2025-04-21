# Serverless-Architecture-Diagram-for-Hotel-Website

Summary
The following diagram represents a serverless architecture design that may be used for a hotel booking website, where a user may book a hotel room on a company's website. This design makes it easy to manage on aws as aws manages a lot of the serverless architecture while remaining cost effective. The website will be hosted on AWS and use only AWS services

Step by Step Process
1. Domain Resolution via Amazon Route 53
When a user enters the hotel's domain name into their browser, Amazon Route 53 resolves the DNS request and directs the user to the application’s CloudFront distribution endpoint.

2. Content Delivery and Access Control with Amazon CloudFront
CloudFront acts as the content delivery network (CDN), providing low-latency access to the web application’s static assets. It also serves as a secure layer between the user and the Amazon S3 bucket by restricting direct public access through Origin Access Control (OAC).

3. Application-Level Security with AWS WAF and AWS Shield
AWS Web Application Firewall (WAF) is integrated with CloudFront to protect against common web exploits such as SQL injection and cross-site scripting (XSS). AWS Shield 
Standard is also used to provide protection against distributed denial-of-service (DDoS) attacks.

4. Static Web Hosting with Amazon S3 and Encryption
Static web content (e.g., HTML, CSS, JavaScript) is hosted in an Amazon S3 bucket. Server-side encryption with AWS Key Management Service (SSE-KMS) is enabled to ensure that stored data remains secure at rest.

5. User Authentication with Amazon Cognito 
When a user logs into their account, authentication is handled by Amazon Cognito. Upon successful login, Cognito issues a JSON Web Token (JWT), which is used to authorize subsequent interactions with backend services.

6. API Management with Amazon API Gateway
The frontend application communicates with backend services via Amazon API Gateway. API Gateway uses a Cognito authorizer to validate the JWT token included in each request, ensuring that only authenticated users can access protected endpoints.

7. Payment Processing via AWS Lambda and Stripe
 An AWS Lambda function integrates with the Stripe API to process payment transactions. This function is invoked only after the user initiates a booking and provides payment details.

8. Booking Confirmation Storage in Amazon DynamoDB
Upon successful payment, a separate Lambda function is triggered to record the booking details such as customer name, contact information, room type, and booking dates into an Amazon DynamoDB table.

9. User Notification via Amazon SNS
A final Lambda function sends a booking confirmation notification to the user through Amazon Simple Notification Service (SNS), either via email or SMS, confirming the successful reservation.

Amazon Cloudwatch and Cloudtrail will monitor all lambda functions for monitoring and auditing purposes


Highlighted Security Features
Using AWS Cloudfront restricts public access to the s3 bucket, serves as a secure layer
AWS WAF and AWS Shield help prevent against common application level attacks such as SQL injection and DDoS attacks
AWS Cognito handles authorization when users login to their account and sets up JWT tokens.
AWS API Gateway validates JWT token produced by Cognito to ensure only authenticated users can access protected endpoints
Amazon Cloudwatch and Cloudtrail will monitor all lambda functions for monitoring and auditing purposes


