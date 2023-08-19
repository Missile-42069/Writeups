
An Ordinary Midsummer Day...

As an IT department personnel of SwiftSpend Financial, one of your responsibilities is to support your fellow employees with their technical concerns. While everything seemed ordinary and mundane, this gradually changed when several employees from various departments started reporting an unusual email they had received. Unfortunately, some had already submitted their credentials and could no longer log in.

You now proceeded to investigate what is going on by:

    Analysing the email samples provided by your colleagues.
    Analysing the phishing URL(s) by browsing it using Firefox.
    Retrieving the phishing kit used by the adversary.
    Using CTI-related tooling to gather more information about the adversary.
    Analysing the phishing kit to gather more information about the adversary.

Connecting to the machine

Start the virtual machine in split-screen view by clicking the green Start Machine button on the upper right section of this task. If the VM is not visible, use the blue Show Split View button at the top-right of the page. Alternatively, using the credentials below, you can connect to the VM via RDP.
THM key
Username 	damianhall
Password 	Phish321
IP 	10.10.207.146

Note: The phishing emails to be analysed are under the phish-emails directory on the Desktop. Usage of a web browser, text editor and some knowledge of the grep command will help.

**Answer the questions below**
Who is the individual who received an email attachment containing a PDF?
Answer: William McClean
I opened all of the emails inside the directory using Mozilla Thunderbird and found the the user

![[Pasted image 20230714202536.png]]



What email address was used by the adversary to send the phishing emails?
Answer:  Accounts.Payable@groupmarketingonline.icu
Under the "From" field of the email, we can find the email used by the adversary
![[Pasted image 20230714202737.png]]

What is the redirection URL to the phishing page for the individual Zoe Duncan? (defanged format)
Answer: http[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error'

The redirection URL can be found in the file attached to the email of Zoe Duncan as shown in the picture below

![[Pasted image 20230726205211.png]]

not gonna lie, I almost lost my mind trying to enter this URL (http[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/enterpassword[.]php?H5A7e31690374673805cff91fc14a1c80892b589da7766c6805cff91fc14a1c80892b589da7766c6805cff91fc14a1c80892b589da7766c6805cff91fc14a1c80892b589da7766c6805cff91fc14a1c80892b589da7766c6&email=zoe[.]duncan@swiftspend[.]finance&error=) I thought this is the redirected URL

What is the URL to the .zip archive of the phishing kit? (defanged format)
http[://]kennaroads[.]buzz/data/Update365[.]zip

After messing around with the URL, by removing some stuff, I found this
![[Pasted image 20230726205815.png]]

Then I thought to myself, lemme try to go to kennaroads.buzz to see if it will show something then it sure did, below is the picture of the website:

![[Pasted image 20230726210345.png]]

then I pretty much messed around with the URL until I found the  /data directory. then I remembered that by putting the file name after the URL, it will download the said file so that is how I arrived with the answer

![[Pasted image 20230726205624.png]]

What is the SHA256 hash of the phishing kit archive?
Answer: ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686

Run the sha256sum command on l Linux on Update.zip file, it pretty much will give you the answer, no image needed just see it for yourself

When was the phishing kit archive first submitted? (format: YYYY-MM-DD HH:MM:SS UTC)
Answer:  2020-04-08 21:55:50 UTC 

After submitting the file hash to Virus Total, I saw that the file was submitted on 2020-04-08 at almost 10 pm in UTC as shown below

![[Pasted image 20230727231044.png]]

When was the phishing domain that was used to host the phishing kit archive first registered? (format: YYYY-MM-DD)
Answer: 2020-06-25

After pasting the link on virus total, we can see the Historical SSL certificates, we can see that there are two instances of it, I chose the earlier date since it is older than the two and got the correct answer
![[Pasted image 20230727232601.png]]

What was the email address of the user who submitted their password twice?
Answer: michael.ascot@swiftspend.finance

If we go to the logs.txt on http://kennaroads.buzz/data/Update365/ we can see that there are a lot of emails that either trolled the cybercriminal or pretty much submitted their passwords as shown below 

```
---------+ Office365 Login  |+-------
Email : isaiah.puzon@gmail.com
Password : PhishMOMUKAMO123!
-----------------------------------
Client IP: 158.62.17.197
User Agent : Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/112.0
Country : Philippines
Date: Mon Jun 29, 2020 10:00 am
--- http://www.geoiptool.com/?IP=158.62.17.197 ----
--+ Created BY Real Carder +---
---------+ Office365 Login  |+-------
Email : michael.ascot@swiftspend.finance
Password : Invoice2023!
-----------------------------------
Client IP: 64.62.197.80
User Agent : Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36
Country : United States
Date: Mon Jun 29, 2020 10:01 am
--- http://www.geoiptool.com/?IP=64.62.197.80 ----
--+ Created BY Real Carder +---
---------+ Office365 Login  |+-------
Email : zoe.duncan@swiftspend.finance
Password : Passw0rd1!
-----------------------------------
Client IP: 64.62.197.80
User Agent : Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36
Country : United States
Date: Mon Jun 29, 2020 10:01 am
--- http://www.geoiptool.com/?IP=64.62.197.80 ----
--+ Created BY Real Carder +---
---------+ Office365 Login  |+-------
Email : michael.ascot@swiftspend.finance
Password : Invoice2023!
-----------------------------------
Client IP: 64.62.197.80
User Agent : Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36
Country : United States
Date: Mon Jun 29, 2020 10:01 am
--- http://www.geoiptool.com/?IP=64.62.197.80 ----
--+ Created BY Real Carder +---
---------+ Office365 Login  |+-------
Email : derick.marshall@swiftspend.finance
Password : lol
-----------------------------------
Client IP: 64.62.197.80
User Agent : Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36
Country : United States
Date: Mon Jun 29, 2020 10:01 am
--- http://www.geoiptool.com/?IP=64.62.197.80 ----
--+ Created BY Real Carder +---
---------+ Office365 Login  |+-------
Email : michelle.chen@swiftspend.finance
Password : testing123
-----------------------------------
Client IP: 64.62.197.80
User Agent : Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36
Country : United States
Date: Mon Jun 29, 2020 10:01 am
--- http://www.geoiptool.com/?IP=64.62.197.80 ----
--+ Created BY Real Carder +---
---------+ Office365 Login  |+-------
Email : zoe.duncan@swiftspend.finance
Password : fdsa
-----------------------------------
Client IP: 172.67.216.206
User Agent : Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/112.0
Country : Unknown
Date: Wed Jul 26, 2023 11:40 am
--- http://www.geoiptool.com/?IP=172.67.216.206 ----
--+ Created BY Real Carder +---
```
as we can see,  michael.ascot@swiftspend.finance submitted his password twice


What was the email address used by the adversary to collect compromised credentials?
Answer: m3npat@yandex.com

in the resubmit.php script or file, we can see that the adversary used m3npat@yandex.com as the email to collect compromised credentials as shown in the picture below

![[Pasted image 20230727233251.png]]

The adversary used other email addresses in the obtained phishing kit. What is the email address that ends in "@gmail.com"?
Answer: jamestanner2299@gmail.com

Below is the image from script.st in the .zip file of the phising kit. it says that it will send to the email address jamestanner2299@gmail.com everytime someone send their password on the phising link

![[Pasted image 20230726211735.png]]







What is the hidden flag?
Answer: THM{pL4y_w1Th_tH3_URL}


Honestly this thing almost made me gave up and never return again. In fact I had to look at a writeup for me to solve this

as the image shown below, before slapping enter on office365 directory on the url, enter flag.txt as shown on the image below: 
![[1 xgSGeBZ_sbTUW3A7IfxNAg.webp]]
Source: https://infosecwriteups.com/tryhackme-snapped-phish-ing-line-93e98935a671

then after that I decoded string by piping the string to  `base64 -d` 

![[Pasted image 20230804222501.png]]

but for some reason, it is reversed so I decoded the output string on Cyberchef
and reversed it and I finally solved it

![[Pasted image 20230804222623.png]]

