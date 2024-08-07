# AWS-StaticHosting-CustomDomain-TLS

## Overview

In this document I will explain the success and troubles I had while hosting a static webpage on AWS 
with a custom domain using AWS Route 53 and how I secured the webpage using AWS Cloudfront.

## Files
- **HTML**: Contains the Hypertext Markup
- **CSS**: Contains the multiple Stylesheet to design the HTML
- **JAVASCRIPT**: Contain the JavaScript file for the functionally

Click 👉 [Here](https://drive.google.com/drive/folders/1ke68Wl1ANy_0iNMuR602EU-rI0r_W5JP?usp=sharing) 👈 to see these files

## Create an AWS account and create first bucket
- **1**: Got to https://aws.amazon.com and create an account. It is free but you'll need to add a card just incase you are billed. Dont worry this tutorial is free.
- **2**: Navigate to the AWS S3 console. Once here you will need to click "Create Bucket.
- **3**: Give your bucket a name. To make things easier, this bucket name should be the same as your domain "We'll get into choosing a domain later in this tutorial.
- **4**: IMPORTANT!!! Please make sure the region that's selected is the closest region to you. (Ex. I live in Atlanta so the closest region to me would be "US East N. Virginia)
- **5**: Leave the "Object Ownership" as default.
- **6**: On the "Block Public Access" section uncheck the block that says "Block all public access."
- **7**: Everything else is left as default.

  🎉🎉 CONGRATS YOU CREATED YOUR FIRST BUCKET!!! 🎉🎉
