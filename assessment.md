## Support Engineer Assessment

---

**Objective:** These questions are designed to start conversations and look into how you explain
your thought process with examples. For the second question there is no “right answer,” but the
idea is to see how you can unpack a problem and understand its parts.
Goals: Answer the question like you are speaking to a customer!

### Question 1:

> I am setting up my docs with images but they will not display on the frontend. I can click through these images via:
> **http://img.kittenmittens.com/kitten.jpg**
> but when I look in the dev console I see:
> **Blocked loading mixed active content http://img.kittenmittens.com/kitten.jpg**

- [x] What does this error message mean and how can I fix it?

#### Answer:

Hi [insert-customer-name] :wave: ,

I'm **Michael**, thanks for reaching out to the Support Engineering team at **ReadMe**. We appreciate you submitting the error information in regards to the images not displaying on your frontend. Let's take a closer look at the issue and see what we can find.

**What this means?**
Since you can access your images via direct url, lets focus on the dev console error **Blocked loading mixed active content**. This error is actually [quite common](https://blog.mozilla.org/tanvi/2013/04/10/mixed-content-blocking-enabled-in-firefox-23/) and what this means is that there are links on your **secure docs (HTTPS)** page that **aren't secure (HTTP)**.

**How to Fix**

1. First, i'd recommend checking the url of the links again. Maybe the domain is https and it was just accidentally left out.
   > Updated Example: https://img.kittenmittens.com/kitten.jpg
2. Second, if we know the url is correct, i'd recommend adding a Secure Socket Layer or SSL certificate to the domain kittenmittens.com as this will add the layer of protection recommended for secure hosting. We can do this in 3 easy steps.
   1. Saving your [Custom Domain](https://docs.readme.com/docs/setting-up-custom-domain) in ReadMe

![example-custom-domain](https://files.readme.io/89ca2e7-custom_domain-2018-12.png)

2.  Add DNS CNAME or DNS record on your registrar to point to ssl.readmessl.com

    -[More Info | What is a CNAME?](https://www.godaddy.com/help/add-a-cname-record-19236) -[More Info | What is a DNS A RECORD?](https://www.cloudflare.com/learning/dns/dns-records/dns-a-record/)

![dig-example](https://img001.prntscr.com/file/img001/hwQkBVDESmqMfMddQ0yuQw.png)

1.  Wait for successful certificate generation
    ==You can check the status of your certificate by navigating directly to your custom domain. If you can access your ReadMe's documentation via your custom domain, and there is a lock in the URL bar, you're good to go!==

If running into anymore **Blocked loading mixed active content errors** i'd recommend checking out our [SSL Setup Documentation](https://docs.readme.com/docs/setting-up-custom-domain) or [SSL Problems](https://docs.readme.com/docs/having-problems-generating-ssl) for more advanced configurations or simply reaching back out to us and we will gladly try to fix any pending or additional issues.

Best,

**Michael**

---

### Question 2:

> We’re a new customer and we’ve added our custom domain recently. We’ve run into a few problems:
> Our team in **New York** can see the domain just fine, but our team in **London** is seeing cert errors such as “ssl_error_bad_cert_domain"

- [x] What does this mean?
- [x] How can we fix this?

> The New York team did notice one error when attempting to load some of our fonts from our hosted site. In the dev console they noticed seeing:
> **“Cross-Origin Request Blocked: The Same Origin Policy disallows reading from remote at https://localhost:3000/superfont.ttf”**

- [x] I’m not very technical so I’m not sure what this means? Is there something we should adjust or fix on our end?

#### Answer:

Hi [insert-customer-name] :wave: ,

I'm **Michael**, thanks for reaching out to the Support Engineering team at **ReadMe**. We appreciate you submitting the error information in regards to your team in **New York** being able to access the custom domain but your **London** team receiving "ssl_error_bad_cert_domain". We also confirmed the **New York** teams error of “Cross-Origin Request Blocked: The Same Origin Policy disallows reading from remote at https://localhost:3000/superfont.ttf”. These may be seperate issues so lets first take a closer look at the first problem.

**What this means? | ssl_error_bad_cert_domain**
When adding, removing or updating a DNS record we have to keep in mind of the [propagation time](https://ns1.com/resources/dns-propagation) it takes for DNS entries to update throughout the web. Essentially when you make changes to an entry it can take anywhere from 5mins to 48 hours for the nodes that make up the internet to receive the updated changes. These changes will also vary from location to location and thus could be the reason why your team in **New York** is able to access while **London** still is recieving errors.

**How to Fix**
If you can confirm that your DNS changes were within that 48hours window i'd recommend waiting or you can run a dig on your new DNS ENTRY. If the Dig is successful we can move to the Next Troubleshooting Step. If not, we wait for the propagation process to complete.

###EXAMPLE DIG
![dig-example](https://img001.prntscr.com/file/img001/hwQkBVDESmqMfMddQ0yuQw.png)

###Additional Troubleshooting Steps
**Clear browser cache**
Even when the SSL certificate name and configuration are correct, still the website may throw errors in the browser. This happens when the browser has a cached copy of the website page.

Therefore, to fix the error, we recommend having your **LONDON** office clear the browser cache.

In the **Firefox** browser, we do this by clicking on the History >> Click on Clear Browser History >> Time range to clear to Everything and uncheck everything else aside from Cookies, Cache and Offline Website Data >> Clear Now

To clear cache in **Google Chrome**, we Click More tools >> Clear browsing data. Then we choose a time range. We check the boxes next to “Cookies and other site data” and “Cached images and files.” Finally, click Clear data.

If running into anymore **ssl_err_bad_cert_domain errors** i'd recommend checking out our [SSL Setup Documentation](https://docs.readme.com/docs/setting-up-custom-domain) or [SSL Problems](https://docs.readme.com/docs/having-problems-generating-ssl) for more advanced configurations.

###Additional Issue

- “Cross-Origin Request Blocked: The Same Origin Policy disallows reading from remote at https://localhost:3000/superfont.ttf”

**What this means?**

- Typically this [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) error is to prevent **UNAUTHORIZED** access to server resource for security purposes.

**How to Fix**

- This can be fixed **two** different ways:
  1.  Moving the resource (superfont.tff) to the same domain to bypass the CORS check.
  2.  Enabling CORS by adding this to the headers of your local instance: `Access-Control-Allow-Origin: * `
- ==Due to the remote being a localhost instance, i'd recommend moving the resource to your Domain.==

-[More Info | Advanced Cors](https://auth0.com/blog/cors-tutorial-a-guide-to-cross-origin-resource-sharing/)

These solutions should resolve the errors your receiving. If you are still having any problems, please don't hesitate to reach back out and we will gladly dive deeper into any remaining issues.

Best,

**Michael**
