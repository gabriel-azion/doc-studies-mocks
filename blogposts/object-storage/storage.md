---
schema: blog_post
title: Enhancing Data Management with Azion's Edge Storage
authors:
    - src/content/authors/gabriel.franca.md
meta_tags: azion, edge storage, object storage, data management, serverless, s3 api
excerpt: >-
    Discover how Azion's Edge Storage simplifies data management and enhances application performance. Learn about the benefits of object storage at the edge of the network and how to leverage it using Azion's REST API, CLI, and Edge Functions Storage API.
description: >-
    This blog post dives into Azion Edge Storage, an object storage solution designed to simplify data management and boost application performance. It covers key benefits, setup, and data management using S3 API, REST API, Azion CLI, and Edge Functions Storage API.
img_featured: >-
    /assets/blog/images/uploads/azion-edge-storage.png
categories:
    - developers
related_content:
namespace: blogpost_azion_edge_storage
date: 2024-05-09T06:00:00Z
date_updated:
resourceHub:
    flags:
        contentType: Blog
permalink: /enhancing-data-management-with-azion-edge-storage/

---

As developers, navigating the complex world of data storage can often seem intimidating. There's a constant need to juggle managing growing data volumes, ensuring quick accessibility, and maintaining system performance.

What if you could leverage the concept of Object Storage, deploying your data at the edge of the network, benefiting from low-latency access, scalability, predictable cost, and high availability without having to wrangle with the complexities of traditional storage systems?

In this blog post, we dive into Azion Edge Storage, an object storage solution designed with developers in mind, simplifying the data management process and supercharging applications' performance.

---

## Leveraging Object Storage at the Edge

Through Azion Edge Storage, managing assets like images and files can be accomplished without getting wrapped up in the complexities of infrastructure management. This allows users to focus on building innovative applications by bypassing any infrastructure obstacles.

Key benefits include:

- S3 Compatible API:this compatibility facilitates migration from other cloud storage systems that use the S3 API, allowing the transition without the need to change the existing application code.
- Scalability: the limitless scalability provided by edge infrastructures removes any restrictions on storage capacity. Users can adjust storage according to their demands.
- Reliability: the edge ensures dependable, consistent performance.
- Cost Predictability: unexpected costs can be avoided by keeping data transfer expenses within predetermined budgets.
- Serverless Architecture: serverless architecture brings a practical application development model, emphasizing simplicity and adaptability.
- Avoid Vendor Lock-in:this flexibility facilitates strategic decision-making and promotes competitive pricing.
- No More Egress Charge: with edge computing, data processing happens closer to the source, greatly minimizing data transfer volumes to and from the central server. As a result, businesses can avoid incurring high egress charges often associated with cloud services, thereby saving on operational costs.

---

## Setting Up and Streamlining Data Management


Edge Storage manages data through discrete objects. Each object includes:

- Data composing the object.
- Associated metadata, such as the media type and object size.
- An object key as the unique identifier.

### S3 API

Edge Storage is S3 API compatible. This feature works as follows:

1.  The credentials can be managed through the `/s3-credentials` endpoint. The methods related to the credentials include:

1.  GET: retrieve data on all S3 credentials registered with Azion.
2.  GET by ID: retrieve data on an S3 credential registered with Azion.
3.  POST: create an S3 credential.
4.  DELETE: remove S3 credentials from the account.

2.  Once the credentials are created, you can use them through:

1.  S3cmd
2.  S3 API through the region endpoint `https://s3.use-east-005.azionstorage.net/`
3.  Libraries related to dealing with S3 for your chosen programming language.

Creating S3 credentials to be used with Edge Storage:

```
curl --location 'https://api.azion.com/v4/storage/s3-credentials \
--header 'Accept: application/json' \
--header 'Authorization: Token xxxxxxx \
--header 'Content-Type: application/json' \
--data '{
  "name": "My S3 Credential",
  "capabilities": ["listAllBucketNames", "listFiles"],
  "bucket": "my-bucket-name",
  // expiration based on the timezone defined in RTM settings
  "expiration_date": "2025-01-31T10:57:00"

}'
```

Configuring your credentials in S3cmd:

```
user@user ~ % s3cmd --configure
Enter new values or accept defaults in brackets with Enter.
Refer to user manual for detailed description of all options.
Access key and Secret key are your identifiers for Amazon S3. Leave them empty for using the env variables.
Access Key: [your-recently-created-access-key]
Secret Key:  [your-recently-created-secret]
Default Region....
S3 Endpoint [s3.amazonaws.com]: https://s3.use-east-005.azionstorage.net/
```

Now, you can access and manipulate objects through S3cmd depending on the capabilities assigned to the S3 credential.

Uploading an object using the S3 API

```
curl --location --request PUT 'https://s3.us-east-005.azionstorage.net/<bucket_name>/<object_key>' \
    --header 'Content-Type: text/plain' \
    --header 'X-Amz-Date: 20240304T125612Z' \
    --header 'Authorization: AWS4-HMAC-SHA256 Credential=<access_key>/<date>/us-east-1/execute-api/aws4_request, SignedHeaders=content-length;content-type;host;x-amz-date, Signature=<encrypted_signature>' \
    --data '<filepath>'
```

A user, as long as they are assigned to a team with the Edit Storage Credentials permission, can create credentials that will be visible to other users on the same account. Once a credential is created, it cannot be edited, and the secret keys will only be presented at the moment of creation. This way, when viewing a credential after it has been created, the keys will be omitted.

The credentials can be assigned to a specific bucket or all buckets created by the account, but not to a group of buckets. Although it is possible to create a set of credentials, these won't have management powers over the bucket or the credentials themselves - management of buckets and credentials can only be conducted through the REST API.

However, the credentials provide a specific set of possible operations concerning the objects in the bucket. With appropriate credentials, it is possible to conduct operations such as listing, reading, modifying, and deleting objects, given that the bucket has the necessary permissions. S3 credentials operate separately from the level of access set for the bucket using the REST API, defined by the `edge_access` property. For instance, if a credential with the `writeFiles` capability is created for a bucket with `read_only` permissions, the credential can still be used to add or modify files in the bucket, whereas the Azion API cannot be used for that same operation.

Even though the bucket and credential management is limited to the REST API, the objects themselves can be manipulated by the permissioned credentials.

---

### Rest API

Azion provides REST API methods to store objects, from creating and modifying buckets and their permissions to object management.

Let's say you wish to use object storage as the origin for a static edge application. To do so, you need to:

1.  Create a bucket.
2.  Upload the file containing your application inside a `src` directory. For example:  
 
  
```
src/index.html
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="styles/style.css">
</head>
<body>
    <h1>Hello world!</h1>
    <p>I am an object from a bucket.</p>
</body>
</html>

```

You can access the step-by-step instructions in this [guide](https://www.azion.com/en/documentation/products/guides/upload-and-download-objects-from-bucket/)to upload and download objects from an Azion Edge Storage bucket.

---

### Azion CLI

Another alternative is to initialize and deploy an [application through Azion CLI](https://www.azion.com/en/documentation/devtools/cli/init/). When you initialize an application via the `azion init` command and deploy it to the edge:

1.  A bucket is automatically created with your chosen name for the project.
2.  Your static application is stored in it.

You can see more information on [how to deploy an application through Azion CLI guide](https://www.azion.com/en/documentation/products/cli/frameworks/react/), which presents the steps to deploy a React application on the platform.

---

### Azion Edge Functions Storage API

The Azion Edge Storage can be accessed through the [Edge Functions Storage API](https://www.azion.com/en/documentation/devtools/runtime/api-reference/storage/). This interface enables you to read and write data in the storage and its associated buckets.

To get started with Storage API, you need to:

1.  Import the APIs inside your edge function:

```
import Storage from "azion:storage";
```

2.  Instantiate a new Storage object:

```
const storage = new Storage(bucket);
```

3.  Choose and implement the [methods listed in the documentation](https://www.azion.com/en/documentation/devtools/runtime/api-reference/storage/).

---

## Conclusion

Azion Edge Storage stands as a solution to data storage and management challenges, transforming how developers approach application performance. By leveraging object storage technologies at the edge of the network, it not only offers key benefits such as scalability, high reliability, and cost predictability, but it also simplifies the development process.

With streamlined data management using Azion's user-friendly REST API, CLI, and Edge Functions Storage API, developers can focus on innovation instead of organizational challenges. As we step into the future with Azion Edge Storage, we're not just overcoming data issues, we're unlocking the tremendous potential lying in our data, ready to supercharge our edge applications.
