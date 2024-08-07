# AWS-StaticHosting-CustomDomain-TLS

## Overview

In this document I will explain the success and troubles I had while hosting a static webpage on AWS 
with a custom domain using AWS Route 53 and how I secured the webpage using AWS Cloudfront w/ TLS cert.

## Files
- **HTML**: Contains the Hypertext Markup
- **CSS**: Contains the multiple Stylesheet to design the HTML
- **JAVASCRIPT**: Contain the JavaScript file for the functionally

Click 👉 [Here](https://drive.google.com/drive/folders/1ke68Wl1ANy_0iNMuR602EU-rI0r_W5JP?usp=sharing) 👈 to see these files

## Create an AWS account and create first bucket
- **1**: Got to https://aws.amazon.com and create an account. It is free but you'll need to add a card just incase you are billed.
- **2**: Navigate to the AWS S3 console. Once here you will need to click "Create Bucket.
- **3**: Give your bucket a name. To make things easier, this bucket name should be the same as your domain "We'll get into choosing a domain later in this tutorial.Ex: "www.FollowByCloud.com" or "s3.followedbycloud.com"
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

## Using Route 53 to Add Custom Domain

Now that you've gotten your webpage up and running, it's time to add your custom domain!! 

If you already have a domain you can skip this part. If not, you will need to follow along.

## Creating Domain

Firstly, we'll need to navigate to the Route 53 console. From there, you'll need to select "Registered Domains." Once on the homepage you will need to click on the "Register Domain" tab. Here is where you will insert whatever name you want. (*I suggest you use the same name as your S3 bucket*) search to see the availabile options. 

Once you select the domain that fits you add you your cart and enter your details. After you've entered your details you wil need to accept the terms and conditions. If you dont want to auto renew you domain make sure you select to disable that option and complete the order. Once you complete the order you will need to wait until Amazon register the domain. 

It states it take up to three days but it usually takes around 10 mins. Once your domain is registered you'll recieve an email stating so.

## Connecting Custom Domain to S3 using Route 53

Once your domain is registered you can now begin the process of connecting it to your S3 bucket. (*I Suggest you open your S3 bucket in another tab so you can work on both at the same time*)

Going back to your S3 bucket, you will need to copy your "Bucket website endpoint URL" 

(*If you dont remember where that was it was: S3> Bucket > Bucket name > Properties then scroll to the bottom*)

Then go back into the "Route 53" Console and select your hosted name that was created for your domain.

Once inside of your domain, select "Create record." Here you'll create a cname by click on the dropdown menu labeled "Record type"

In the "Record name" section you can add either "www" or "s3" all depends on how you labaled your S3 bucket in the beginning.

Under "Value" place the "Bucket website endpoint URL" you copied earlier. (*Delete the http part of the URL*) Leave everything else default and create the record.

You should be brought back into the listed Domain name homepage where you will see the new record you just created.

Open up and incognito browser and type in the url you just create and you should be able to see that its live and working. But just one thing the webpage its not secured!!

## Securing you S3 webpage with Cloudfront w/ TLS Cert

Nagivate to Cloudfront console

Once in the console find and click on "Distributions" tab. (*Its should direct you into the distrubutions automatically but if not it will on the lefthand side*)

In "Distributions" tab select the "Create distributions" tab. Under "Origin domain" your bucket should pop up there. Select the correct bucket. Since we are using static website hosting, click on the button that states " Use website endpoint"

Scroll down until you see the "Default cache behavior" section and look under where you see "Viewer" select to rediect HTTP to HTTPS" (* This means if someone tries to enter your webpage using HTTP they will be automactially be redirected to HTTPS and use the TLS cert*)

Leave everything default until you reach the section named "Web Application Firewall (WAP)" make sure to enable this section.

Scroll towards the bottom until you see the "Settings" section

In the "Price class" section I will sugggest using "North America and Europe" for low cost.

Under "Alternate domain name (CNAME)" enter the name of the domain you created. (Will add as a alternaive name when you create the SSL Cert)

Under "Custom SSl certificate" you don't have one yet, so click on "Request certificate" You will be directed to "AWS Certificate Manager (ACM)" console 

select on "Request a public certificate" and click next

Under "Fully qualified domain name" enter the domain you created. Everything else is left as default. Click request.

You will be directed to the "Certificates" page where you will see your certificate ID has a status of "Pending Validation" (*If you dont see your certificate ID refresh the page and it will appear*)

While waiting for the pending validation you will need to select the certificate ID and add your CNAME into the certificate ID. Since we are using "Route 53" we already have a CNAME created. You will see a tab thats named "Create records in Route 53" Select that and it will redirected you to your CNAME that has been created. Select "Create records" You have add your CNAME into certificate ID. 

(*If you want to see that you can head back to the Route 53 console, into Hosted zones, into your domain and you'll see the new CNAME thats been added  *)

(*The Validation state will take a while so you can go and get a few things around the house down. Like remove those chip crumbs off your desktop or laptop. 😆😆😆*)

One Amazon has issue the validation head back into your distributions and refresh the "Custom SSL certificate" you will see the new certificate thats been created with the domain. Everything else is left as default. Click on "Create Distributions"

Your distributions should be created and your webpage will be secured!! 🎉🎉

Open incoginto and type domain into the address bar, there you will see your webpage up and running with a secure certification!! 

CONGRATS ON COMPLETING THIS TUTORIAL WITH ME!!! 
