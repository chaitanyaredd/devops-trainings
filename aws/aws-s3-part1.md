# AWS S3
- AWS s3 is an object storage service designed to store & retrive the any amount of data from anywhere from the web.
- It's used for storing the
    -   Hosting website
    -   storing backups
    -   data lakes

# Features of AWS S3
- Scalability: We can store data as much as needed without worrying about infrastructure. Only one constraint is that we can't upload a file which a more that 16TB.

- Durability: AWS S3 provides 99.99999999999 (11-9's) durability, so chances loosing data almost negligible. When we create a bucket in a region the data will be replicated in almost 3 regions, so the durability is very high.

- Security: We an secure the data on s3 using better encryption polocies & also we can provide granular level of access.


# Rules while creating S3
- S3 buckets names are unique across the global.

- We have to create the buckets in region

- The size of the file should not exceed 16 TB

# How to access the AWS S3 buckets using CLI
- Setup AWS CLI

- AWS configure using access & secret key

- **To test connectivity from AWS CLI to AWS**
    aws sts get-caller-identity

- **List S3 buckets**
    aws s3 ls

- **List contents of s3 buckets**
    aws s3 ls s3://my-bucket-contents-2024-apr

- **Move the contents from one bucket to other bucket**
    aws s3 mv s3://bucket1/sample.zip s3://bucket2/

- **View all the child content from s3 bucket**
    aws s3 ls s3://bucket1 --recursive

# AWS S3 Storage classes
- There are total 7 storage classes in AWS s3

- **s3 standard:**
    - This is the default storage class if we don't specify any storage class for s3 bucket
    - High durability.
    - It's mainly used for applicaitons that will **access the objects frequently**.
    - This storage class offers very good **low latency** compared to other storage classes.

- **S3 standard IA**
    - It's mainly used for storing the objects that are infrequently accessed.
    - High availability
    - It's cost charges are less compared to the S3 standard storage class.

- **s3 Intelligent Tiering**
    The cost for the bucket is varies based on the usage, if we are highly accessing the cost of the bucket  charges will be high & if we are accessing the data very low the cost of bucket charges are low.

- **s3 one zone - IA**
    - The objects data placed into one zone.
    - Low durability
    - cost low
    - Mainly used to store the Infrequent access objects.

- **s3 glacier instant retrival**
    - Used mainly for archival data storage.
    - We can retrive the data from this storage class buckets in **milliseconds**

- **s3 glacier flexible retrival**
    - Used for storing the archival storage
    - Retrival time for archival data should be from **mins to hours**

- **s3 glacier deep retrival**
    - Used for storing the archival storage
    - Retrival time within 12 hours.


# TASK: Prepare table & pie chart to calculate the price of each storage class for 1TB for 1 month.

# Requestor pay option
    - In account1 s3 bucket created & account1 is charged only for storgage utilized for stoing objects in S3 bucket.

    - If account2 want to access the objects of s3 bucket of account1 & these charges has to be paid by the account2.

    - AWS S3 ==> Bucket ==> Properties ==> Enable requestors pay

# S3: Object Tagging
    - Used to keep the tags for the objects that are present in s3 bucket.
    - AWS S3 ==> Bucket ==> Object ==> Tag(Object png)
    - Used to copy the objects that belongs to particular tag from one bucket to other bucket.

# S3: Bucket policy
    - Create IAM user[chaitu.dev] without any privilges
    - Create a bucket [app.bdx-nonprod-report] in root account
    - Create IAM policy to list the s3 buckets & attach to IAM user.
    - Check whether IAM user able to access the S3 buckets or not.

# S3: How to make S3 bucket publically accessible
    - To make s3 bucket publically accessible we have to turn off public acess for S3 bucket.
    - Create a bucket policy & attach to bucket, which can help you to decide who can access the s3 buckets & its objects & what actions they can do.
    - Sample bucket policy is in format
        {
            "Version": "2012-10-17",    # Policy langugage version
            "Statement": [
                {
                "Sid": "ExamplePolicy",
                "Effect": "Allow",
                "Principal": "*",  # Refers to all users.
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::your-bucket-name/*"
                }
            ]
        }

# S3: Presigned URL
    -   Give access to the user for particular object to specific duration & post that access will removed.   
    -   S3 ==> Bucket ==> Object ==> Actions ==> Presigned URL ==> Duration

# S3: Securing bucket
    - **AWS SSE S3 Encryption:**
    Default encryption mechanism used to encrypt the data that is placed in s3.

    - **AWS S3 SSE KMS**:
    Using KMS service we can create cryptographic(KMS) keys & attach to S3 buckets to encrypt objects of S3 bucket.

    - **Encryption at transit:**
        -   Basically we can access the objects of S3 bucket via http & https.
        -   To allow only https requests we have to update the bucket policy
            {
                "Version": "2012-10-17",
                "Statement": [
                    {
                        "Sid": "AllowOnlyAWSUsers",
                        "Effect": "Allow",
                        "Principal": "*",
                        "Action": "s3:*",
                        "Resource": [
                            "arn:aws:s3:::your-bucket-name",
                            "arn:aws:s3:::your-bucket-name/*"
                        ],
                        "Condition": {
                            "Bool": {
                                "aws:SecureTransport": "true"
                            },
                            "StringEquals": {
                                "aws:PrincipalType": "User"
                            }
                        }
                    }
                ]
            }

# S3: Bucket versioning
    - Every object that we have uploaded will have previous versions.
    - S3 ==> Bucket ==> Properties ==> Version ==> Enable
