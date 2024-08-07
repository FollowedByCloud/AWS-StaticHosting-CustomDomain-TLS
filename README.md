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
- **4**: IMPORTANT!!! Please make sure the region that's selected is the closest region to you. (*Ex. I live in Atlanta so the closest region to me would be "US East N. Virginia*)
- **5**: Leave the "Object Ownership" as default.
- **6**: On the "Block Public Access" section uncheck the block that says "Block all public access."
- **7**: Everything else is left as default.

  🎉🎉 CONGRATS YOU CREATED YOUR FIRST BUCKET!!! 🎉🎉

## Upload your files to your bucket and add bucket policy ##

Now that you've created your first bucket, you should be brought to the S3 bucket homepage, here you should see the bucket you just created.

Once you're inside your bucket, here's here you'll be able to upload your files of your website. (*This process should take around 1-7 mins depending on how many files you have*)

If you forgot or missed step 6 in the last section here's the time to go back and make sure you'll unchecked the "Block Public Access" box. You can find this in the permissions tab inside of your bucket. 

There's a few more step to completed this bucket setup...

Now if you go back into your bucket objects and search for your index.HTML file, you can click on it to see your object URL. If you click on that you should be able to see your webpage right? Not quite yet, you will get an "AccessDenied" message that appears. This message appears because your index.html file is not yet public.To fix that you'll first need to navigate back to your bucket page and click on the permissions tab, scroll down until you see "Bucket Policy". Here's where you'll modify your policy!  

(*Dont get nervous or scared, this is a tutorial so we have the bucket policy for you!!*)

Click 👉 [Here](https://drive.google.com/drive/folders/1sUXm8p-S6Wt1Lr1xneI_8Ftb_45j7K7y?usp=sharing) 👈 for the bucket policy

Copy and paste this policy into the text editor. Make sure you replace the "Resource" section with your bucket name orelse it will not work. If you forgot your bucket name, there the Bucket ARN above the text editor that you can easily copy and paste into the section. Save the changes. 

Now lets enable the webpage for static hosting. Go into the properties tab and scroll down until you see the "Static website hoisting" section (*Should be at the bottom of the page*)
Click edit. Once you click on enable there whould be a list of things that pop up. Leave the "Hosting type" section default. In the "Index document" section inset *index.html* If you have an error page for your webpage inset that into the "Error document" section if not leave it blank, Same with "Redirection rules" Save the changes.
 
Now if you scroll back down to the "Static website hosting" section you should be able to a "Bucket website endpoint" if you click on that link you should be able to see your webpage up and running. 
