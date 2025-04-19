# PerimeterX-Reverse



Solver ^UPDATED REVERSED/SOLVED SCRIPT^

Contact provided below for inquiries regarding the purchase of newer or older versions of PerimeterX, please reach out via Telegram or Discord (Telegram preferred). Contact details are provided above.

**Tele Contact:** [@sudodaemonn](https://t.me/sudodaemonn)

**Tele Channel:** [Join Here](https://t.me/+qP9G-_ii_XA1MGIx)

## Background Information

This repo is gonna be my progress as I continue to attempt to reverse engineer PerimeterX's challenge untill I can produce a fully unflagged bypass/solver that's completley automated using only request no browser. I plan to scrape Device WEBGL Fingerprints and make my own Motion Data if needed.

## **How can I try to avoid getting prompted with this PerimeterX captcha?**

Use High Quality IP Addresses | low fraud score, residential IP (best)

Use Undetected Drivers | If you're using something such as selenium, puppeteer or even playwright it's very important you use an "undetected" plugin that actually works to try and avoid getting prompted (99% of the time it is very easy for these antibot services to tell you're using a webdriver like selenium, puppeteer, playwright, phantom and etc even when using an "undetected" version, personally i would advise staying away from these when trying to bypass captchas.)

Unflagged TLS | It is important to insure that your request is not being flagged due to its TLS Fingerprint. One way you can try to avoid this is to use a library that allows you to modify your TLS properties such as TLS_CLIENT which allows you to spoof some of your properties such as extension order, supported cipher suites and some basic window properties. Please note this will not always be enough to not get prompted with antibot challenges.

Unflagged WEBGL/Device Fingerprints | If the antibot service you're trying to get around is any good it will check something called a device hash/fingerprint that was computed from data collected from properties it was able to gather from you visiting the site. Suprisingly, the computed fingerprint is usually very unique (only 1 in around 200,000 devices produce the same hash) this makes it easy to tell the antibot services if your request is coming from a client with the same browser properties (CPU, GPU, CanvasFP, Screen Resolution, Screen Dimensions, User-Agent, Browser Extensions, Timezone just to name a few) as you can see you can't spoof these types of things with only a request library which is where things get more complex and why it may be required to reverse engineer the antibot's encryption methods and fingerprint methods so you're able to spoof these properties.

## How it works

PerimeterX Challenge Example (shown on ssense.com)

![image](https://github.com/user-attachments/assets/7efc2c01-e1f3-48b5-9450-271ff1868521)


PX Cookie Gets set by PerimeterX Script

![image](https://github.com/user-attachments/assets/2ee12c20-21d6-493c-823f-4f081cc74ff0)


Script that sets the Cookie gets loaded within HTML <script> tag

![image](https://github.com/user-attachments/assets/2d60d532-8068-4774-bf76-a3e63743ee8c)


As you can see it shows the PxAPPID which is essentially the sites site_key

Request to fetch the challenge script

![image](https://github.com/user-attachments/assets/eb20e1b2-ad0e-45b7-9d07-ad9bcda02eb5)


Source Code of PerimeterX's loaded challenge

![image](https://github.com/user-attachments/assets/6c70530e-ff55-4fef-ab32-2e22f4a06343)

The source code is over 9,000 lines long but this is because it's obfuscated and it has a lot of polyfill functions. one thing you should note is that the source code has VM protection along with obfuscation, meaning that every time you refresh the page the function and variable names will change. PerimeterX along with many other antibot services use this to make it as difficult as possible for people to reverse engineer.

What we need to do

Solve Request

![image](https://github.com/user-attachments/assets/e7ab95aa-d2da-438e-b2a2-ebe57d4c536b)


This request essentially whitelist the set _pxhd cookie so that it is valid. So basically this is the captcha token. all we have to do is reverse the payload values so we can automate this.

Payload Value

![image](https://github.com/user-attachments/assets/bb251066-1810-4cbb-9fdb-a2e7fe6e2904)


These are the payload values

payload Encrypted & Encoded value I will need to reverse engineer (We can tell that base64 was used at some point because we can see an "=" which usually comes from padding) (COMPLETED REVERSE)
AppID this is basically the site key mentioned earlier (each site has a unique one of these)
tag this is the version tag (each site also has a unique version)
uuid randomly generated UUID this is usually just used as a request indentifier
ft A unique 3 digit number (each site has it's unique ft number)
seqrsc - 1.
en NTA always.
pc Generated Value I will need to reverse (NEEDS TO BE REVERSED)
sid TO BE DETERMINED
vid TO BE DETERMINED
pxhd This is the _pxhd cookie value which is basically the captcha token
cts TO BE DETERMINED
rsc This is the Request Count
