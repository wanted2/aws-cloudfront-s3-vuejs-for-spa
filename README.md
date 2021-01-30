An example of Single Page App with CloudFront and S3
====

In this tutorial, we will build a simple SPA with CloudFront, S3 and Vue.
For SPA part, we reuse the example in [`vue-blog-demo`](https://github.com/snipcart/vue-blog-demo).

# Introduction

## App structure

```
root ------- serverless.cf.yaml     # AWS Cloudformation template (in YAML)
     ------- www/                   # the SPA content
                  ----- blog/       # Vue-blog code 
```

Services you will need access:

* S3
* Cloudfront

# Deployment
You will need [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html) for the deployment.

* Step 1: Using CloudFormation to deploy the template. 
```
$ aws cloudformation deploy \
  --template-file serverless.cf.yaml \
  --stack-name myblog-spa
```
* Step 2: Build Vue code
```
$ cd www/blog
$ node build/build.js
```
* Step 3: Upload the content in `www/blog/dist` to S3.
```
$ aws s3 cp --recursive www/blog/dist/ <your_s3_bucket_in_step_1>
```
* In the AWS Cloudfront console, you will find the Cloudfront domain name to access your deployed website.

# Contact

If you have any questions, feel free to reach me at [tuan.nguyenanh.brse@gmail.com](mailto:tuan.nguyenanh.brse@gmail.com).