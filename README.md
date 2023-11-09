# identifying-phishing-emails

![scam-3933004_1280](https://github.com/RodMo97/identifying-phishing/assets/124803297/c892503b-4d93-4850-aef8-77135ee4f248)

* [Overview](#overview)
* [Artifact Collection](#artifact-collection)
* [Message Source](#message-source)
* [Reverse Lookup](#reverse-lookup)
* [Run Snort](#run-snort)
* [Documentation](#documentation)
* [Squeal](#squeal)

# Overview 

Phishing is a social enginnering attack used to divulge sensitive information or trick victims into downloading/installing malicious malware. There are different forms of phishing which include email, voice, and text message.

For this topic, we will cover over how to spot phishing emails and the some of thetools used in investigations. The email service being used is Outlook.

# Artifact Collection

Artifacts are pieces of information/footprints, such as text or a reference to a resource, used to create concreate evidence for an incident. 

When conducting an investigation for artifacts, there are two important areas of interest to review, the email header and email body.

* Email Header

      - Subject line
      - Time/Date
      - Sender and recipient email address
      - Sender IP address
      - Reverse lookup of sender IP
      - Reply-to email address

* Email body

      - Attachments
      - Hash values
      - URL links
                
### Collection Example
<img width="713" alt="Drawing-1 sketchpad" src="https://github.com/RodMo97/identifying-phishing/assets/124803297/e5f135aa-15cc-402a-b083-d87091cb1145">

# Message Source

Unless an SMTP analysis tool is used, it is not always as straightfoward to find the Sender IP and/or reply-to as it is the other information mentioned, By reviewing the source of the message, it gives a more detailed look into an email.

Most of the information needed is provided in the screenshot, but for learning purposes, I will only use the Sender's IP address (209.85.222.195) to find the other pertinent information.

### Source Example
<img width="823" alt="Screenshot 2023-11-07 at 7 37 03ΓÇ»PM" src="https://github.com/RodMo97/identifying-phishing/assets/124803297/5b60af3c-f679-4bf8-b77a-d846f093159b">

# Reverse Lookup

The sender's IP from the message source can be used to locate the domain name. The tool used in the example is: https://mxtoolbox.com/SuperTool.aspx

<img width="1512" alt="Screenshot 2023-11-07 at 7 40 44 PM" src="https://github.com/RodMo97/identifying-phishing/assets/124803297/6e56a669-ecef-47f3-be3f-736fd7beb017">

### Other reverse lookup tools

       - https://viewdns.info/
       - https://hackertarget.com/reverse-dns-lookup/
       - https://reverseip.domaintools.com/

After using reverse lookup to trace the IP to a domain name, using a 


<img width="1512" alt="Screenshot 2023-11-07 at 7 42 48 PM" src="https://github.com/RodMo97/identifying-phishing/assets/124803297/6c4066a3-0070-4baf-8fc4-0c79127d0627">



<img width="1331" alt="Screenshot 2023-11-07 at 5 02 53 PM" src="https://github.com/RodMo97/identifying-phishing/assets/124803297/1b29c370-fe28-4930-8cfb-ea104767bb6f">


<img width="1512" alt="Screenshot 2023-11-07 at 5 10 28 PM" src="https://github.com/RodMo97/identifying-phishing/assets/124803297/da64b121-3beb-48b1-b193-2e64eca83b44">





<img width="769" alt="Screenshot 2023-11-07 at 7 26 29 PM" src="https://github.com/RodMo97/identifying-phishing/assets/124803297/80e34e8b-7224-4a4b-9455-4a78d824f231">


<img width="1512" alt="Screenshot 2023-11-07 at 7 59 15 PM" src="https://github.com/RodMo97/identifying-phishing/assets/124803297/4f6cbd90-d717-40ce-a9c4-60405ac14d8b">
