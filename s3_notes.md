# AWS S3 Notes

* S3 is storage for the internet!
* S3 has a simple web services interface that you can use to store and retrieve any amount of data, at any time, from any where on the web. 

Advantages to S3
* Create buckets
* Store data in buckets - store an infinite amount of data in a bucket. Each object can contain up to 5tb of data. Each object is stored and retrieved using a unique developer-assigned key.
* Download your data
* Permissions
* Standard interfaces - Use standard-based REST and SOAP interfaces

Buckets
* Container for objects stored in S3.
* Can be created in specific region
* Can generate unique version id for objects

Objects
* Fundamental entities stored in S3
* Consist of object data and metadata
* Metadata describe the data
* Is uniquely identified within a bucket by a key and a version id.

Key
* Unique identifier for an object within a bucket

Regions
* You can choose the geographical region where S3 will store the buckets you create
* You might choose a region to optimize latency, minimize costs, or address regulatory requirements
* Objects stored in a region never leave the region unless you explicitly transfer them to another region.

Storage Classes
* S3 offers a range of storage classes designed for different use cases. These include S3 STANDARD for general purpose storage of frequently accessed data, S3 STANDARD_IA for long-lived, but less frequently accessed data, and GLACIER for long-term archive.

Bucket Policies
* Bucket policies provide centralized access control to buckets and objects based on a variety of conditions, including S3 operations, requesters, resources, and aspects of the request (e.g., IP address).
* The permissions attached to a bucket apply to all of the objects in that bucket.
* Unlike access control lists (described below), which can add (grant) permissions only on individual objects, policies can either add or deny permissions across all (or a subset) of objects within a bucket. 
* Only the bucket owner is allowed to associate a policy with a bucket.

AWS IAM (Identity and Access Management)
* You can use IAM with S3 to control the type of access a user or group of users has to specific parts of an S3 bucket you AWS account owns.

Operations
Most common operations
* Create a Bucket
* Write an Object
* Read an Object Deleting an Object
* Listing keys

Making Requests
S3 is a REST service. You can send requests to S3 using the REST API or the AWS SDK wrapper libraries that wrap the underlying S3 Rest API, simplifying your programming tasks.

IMPORTANT: Every interaction with S3 is either authenticated or anonymous. Authenticated requests must include a signature value that authenticates the request sender. The signature value is, in part, generated from the requester’s AWS access keys (access key id and secret access key). If you are using the AWS SDK, the libraries compute the signature from the keys you provide. However, if you make direct REST API calls in your app, you must write the code to compute the signature and add it to the request

About Access keys
The following review the types of access keys that you can use to make authenticated requests.

* AWS Account Access Keys: The account access keys provide full access to the AWS resources owned by the account. It has an Access Key ID and a Secret Access Key. The access key ID uniquely identifies an AWS account.
* IAM User Access Keys: IMPORTANT You can use IAM to create users under your AWS account with their own access keys and attach IAM user policies granting appropriate resource access permissions to them. To better manage these users, IAM enables you to create groups of users and grant group-level permissions that apply to all users in that group. These users are referred to as IAM users that you create and manage within AWS. The parent account controls a user’s ability to access AWS. Any resources an IAM user creates are under the control of and paid for by the parent AWS account. These IAM users can send authenticated requests to S3 using their own security credentials. 
* Temporary Security Credentials 
    * In addition to creating IAM users with their own access keys, IAM also enables you to grant temporary security credentials (temporary access keys and a security token) to any IAM user to enable them to access your AWS services and resources. You can also manage users in your system outside AWS. These are referred to as federated users. Additionally, users can be applications that you create to access your AWS resources.
    * IAM provides the AWS Security Token Service API for you to request temporary security credentials. You can use either the AWS STS API or the AWS SDK to request these credentials. The API returns the temporary security credentials (access key id and secret access key), and a security token. These credentials are valid only for the duration you specify when you request them. You use the access key id and secret key the same way you use them when sending requests using your AWS account of IAM user access keys. In addition, you must include the token in each request you send to S3.
    * For added security, you can require multifactor authentication when accessing your S3 resources by configuring a bucket policy.

Working with S3 objects
S3 is a simple key, value store designed to store as many objects as you want. You store these objects in one or more buckets. An object consists of the following:
* Key
* Version id
* Value
* Metadata - A set of name-value pairs with which you can store information regarding the object. You can assign metadata, referred to as user-defined metadata, to your objects in S3. S3 also assigns system-metadata to these objects , which it uses for managing objects.
* Subresources - S3 uses the sub resource mechanism to store object-specific additional information. Because sub resources are subordinates to objects, they are always associated with some other entity such as an object or a bucket.
* Access Control Information - You can control access to the objects you store in S3. S3 supports both the resource-based access control , such as Access Control List (ACL) and bucket policies, and user-based-access control.

IMPORTANT Your S3 resources (buckets and objects) are private by default. You need to explicitly grant permission for others to access these resources. For example, you might want to share a video or a photo stored in your S3 bucket on your website. That works only if you either make the object public or use a presigned URL on your website.

Object Key and Metadata
* Object metadata is a set of name-value pairs. You can set object metadata at the time you upload it. After you upload the object, you cannot modify object metadata. The only way to modify object metadata is to make a copy of the object and set the metadata.
* User defined metadata is a set of key-value pairs. S3 stores user-defined metadata keys in lowercase. Each key-value pair must conform to US-ASCII when you are using REST.

Getting Objects
You can retrieve objects directly from S3. You have the following options when retrieving an object.
* Retrieve an entire object - A single GET operation can return you the entire object stored in S3
* Retrieve object in parts - Using the Range HTTP header in a GET request, you can retrieve a specific range of bytes in an object store in S3.
