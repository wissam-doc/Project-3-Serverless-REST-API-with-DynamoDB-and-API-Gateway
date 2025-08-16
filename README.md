# Serverless-Image-Processing-with-S3-and-Lambda

A serverless project that automatically resizes and optimizes images uploaded to an S3 bucket using AWS Lambda and stores the processed versions in another location within S3.

## 🏢 Architecture Overview


![Manara](https://github.com/user-attachments/assets/daa9129e-2f13-4013-bed6-ff87cd6f6a3d)


```plaintext
User Uploads Image → S3 (original/)
                         ↓ (Event Trigger)
                  AWS Lambda (resizes image)
                         ↓
                S3 (resized/100x100/, 300x300/)

## ✅ Features

* Automatic image resizing (e.g., 100x100, 300x300)
* S3 event-driven Lambda invocation
* Optimized output images stored in `resized/` folder
* Python-based (uses Pillow library)
* Fully serverless and scalable

## 🔧 Key used services 

* AWS S3 bucket
* AWS clound front
* lambda function
* AWS cloud watch 

## 💡 How It Works

1. A user uploads an image to an S3 bucket (`original/` prefix).
2. S3 triggers a Lambda function via event notification.
3. The Lambda function:

   * Downloads the image from S3
   * Resizes it to multiple dimensions
   * Uploads resized images to `resized/` folder in S3
  
The user uploads photos using web or mobile application and it is stored in a S3 bucket.
The S3 bucket has a “object create” trigger configured which invokes a Lambda function whenever a new image is added to the S3 bucket.
The Lambda function performs the required post processing of the uploaded image.
After post processing the image, Lambda function stores the processed image in another S3 bucket and that for do not trigger the lambda function with new processed image like new input (will take about it into details ). 
An image distribution cloudfront then serves the processed images to the web and mobile application.
and for checking and tracking the process , lambda will add logs on cloud watch to notify us if any error appeared while processing.

tracking Serverless Image Processor functionality:
after everything is setup properly, we can test if it is working as expected or not. Upload an image file to the S3 bucket meant for storing original images . After a few seconds check the target S3 bucket meant to store processed images . You will see resized image — and to see the exact steps , you can check logs on cloud watch. So as you can see it is very easy to setup image processing using serverless technologies.

# Why do we need two buckets?
One question you may have is why do we need two buckets ? Can we not work with just one bucket? Well, the short answer — It is a recommended best practice to avoid infinite looping of Lambda execution. imagine the following scenario of using just one bucket:

Image is added to the S3 bucket.
The object created notification Lambda handler function is invoked.
The Lambda function processes the image and save it back into the same S3 bucket.
The saving of object in step 3 above again invokes the object created notification Lambda handler function and the loop continues! and within a few seconds, you will end with thousands of objects in your S3 bucket along with a huge AWS bill!
So in order to ensure that you never end-up in such a situation a safe and “free” way to get around the issue is to use two separate buckets.

# How to build the project:

Create source and destination Amazon S3 buckets and upload a sample image.

Create a Lambda function that resizes an image and outputs a thumbnail to an Amazon S3 bucket.

Configure a Lambda trigger that invokes your function when objects are uploaded to your source bucket.

Test your function, first with a dummy event, and then by uploading an image to your source bucket.

By completing these steps, you’ll learn how to use Lambda to carry out a file processing task on objects added to an Amazon S3 bucket. You can complete this tutorial using the AWS Command Line Interface (AWS CLI) or the AWS Management Console.


## 📋 Optional Enhancements

* Image format conversion (JPG → WebP)
* Add watermarking
* Store metadata in DynamoDB
* Notify via SNS/Email on success

## 📄 License

written by Suzan El-Tayeb 
