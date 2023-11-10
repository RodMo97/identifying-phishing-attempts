# identifying-phishing-emails

![phishing-6573326_1280](https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/a59c7964-c713-4b1d-b08d-ebc96c09854a)


* [Overview](#overview)
* [Artifact Collection](#artifact-collection)
* [Message Source](#message-source)
* [Reverse IP Lookup](#reverse-ip-lookup)
* [Domain Reputation Lookup](#domain-reputation-lookup)
* [URL Extractor](#url-extractor)
* [Code Inspection](#code-inspection)
* [Malware Scanning](#malware-scanning)
* [Hash Value Check](#hash-value-check)
* [Conclusion](#conclusion)

# Overview 

Phishing is a social enginnering attack used to divulge sensitive information or trick victims into downloading/installing malicious malware. There are different forms of phishing which include email, voice, and text message.

For this topic, we will cover over how to spot phishing emails and the some of the tools used in investigations. The email service being used is Outlook.

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
<img width="713" alt="Drawing-1 sketchpad" src="https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/870d2a46-3798-426e-b3bb-f8796766da07">


# Message Source

Unless an SMTP header analysis tool is used, it is not always as straightfoward to find the Sender IP and/or reply-to as it is the other information mentioned, By reviewing the source of the message, it gives a more detailed look into an email.

Most of the information needed is provided in the screenshot, but for learning purposes, I will only use the Sender's IP address (209.85.222.195) to find the other pertinent information.

### Source Example
<img width="823" alt="Screenshot 2023-11-07 at 7 37 03 PM" src="https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/82520670-549e-42eb-a1dc-e74655719c25">

# Reverse IP Lookup

The sender's IP from the message source can be used to locate the domain name. The tool used in the example is: https://mxtoolbox.com/SuperTool.aspx

### MXtoolbox
<img width="1512" alt="Screenshot 2023-11-07 at 7 40 44 PM" src="https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/fc55d389-c973-452a-b6a3-d770ba8c026b">

### Reverse Lookup Tools

       - https://viewdns.info/
       - https://hackertarget.com/reverse-dns-lookup/
       - https://reverseip.domaintools.com/

# Domain Reputation Lookup

After using reverse lookup to trace the IP to the domain name, it a good idea to find out if it has a bad reputation or not.

Let's use a reputation tool: https://talosintelligence.com/reputation_center/lookup?search=mail-qk1-f195.google.com#ip-addresses

### Talos
<img width="737" alt="Screenshot 2023-11-09 at 3 47 09 PM" src="https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/1830aaee-c586-4248-81a6-6b14e68073bf">

### Reputation Lookup Tools

      -https://urlscan.io/
      -https://easydmarc.com/tools/ip-domain-reputation-check
      -https://www.ipvoid.com/domain-reputation-check/
      
# URL Extractor

Now that artifact information has been collected from the email header, it is time to find artifacts located in the email body. The message source holds all information pertaining to an email, including URLs.

A SMTP header analysis tool can be used to locate URLs as well, but we will use an URL ectrator to obtain information instead. After copying and paste the message source into the extractor, here are the URLs found using: https://www.convertcsv.com/url-extractor.htm

### Convertcsv
<img width="1512" alt="Screenshot 2023-11-07 at 7 42 48 PM" src="https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/a270dd20-6acb-482c-b97e-8ed61aab75b8">

### URL Extractor tools

      - https://gchq.github.io/CyberChef/
      - https://miniwebtool.com/url-extractor/

# Code Inspection

The URL button is another artificate that was highlighted at the beginning of collection process. 

The sender is masquerading as the IRS and is actively trying to get the recipient of the email to fill out the attached document and submitting information to the URL that the "Submit Now" button is attached to.

How do I know that the link will direct to an URL not owned by the IRS? Firstly, the IRS will never ask for sensitive information over email and and secondly, checking the developer code will tell you what URL the "Submit Now" button is associated with.

### Developer Code Example
<img width="1331" alt="Screenshot 2023-11-07 at 5 02 53 PM" src="https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/cf695884-da92-417b-8e88-99b13af0183d">

# Malware Scanning

The developer code revealed that the "Submit Now" button is linked to Google Drive folder which a big red flag. That folder may be used to capture information, or could have malware attached it. That is why it is not ideal to click on any links in untrusted emails.

Now that we have the link, let's run it through a malware scanner to see if it is malicious: https://www.virustotal.com/gui/home/upload

### VirusTotal
<img width="1512" alt="Screenshot 2023-11-07 at 5 10 28 PM" src="https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/9f0ef50b-b7a0-426f-9f45-3fca5ac13a97">

VirusTotal has flagged the link as malicious and it should be avoided at all cost or blacklisted along with any other associated emails, IP's and domains.

### Malware Analysis Tools

      - https://app.any.run/
      - https://www.hybrid-analysis.com/
      - https://www.joesecurity.org/

# Hash Value Check

The attached document could also be malicious. Obtaining the hash of the file could reveal if there are any CVEs (Common Vulnerabilities and Exposures).

In the example, I downloaded to my desktop, ran terminal, accessed the path and typed the following command to reveal the hash of the file.

### Terminal
<img width="769" alt="Screenshot 2023-11-07 at 7 26 29 PM" src="https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/257b9ea5-a882-4d67-97b1-b38a9d7be8cb">

### CVE Check

Followed by that, I ran the hash in VirusTotal to see if it comes back as malicious with any CVEs

<img width="1512" alt="Screenshot 2023-11-07 at 7 59 15 PM" src="https://github.com/RodMo97/identifying-phishing-attempts/assets/124803297/6d47282f-7728-4280-9f49-6c00933d0eca">

# Conclusion

The investigation revealed that the phishing attempt is categorized malicious.  The sender is masquarding as the IRS to collecting sensitive information by instilling fear and urgency into recipients of the email.
