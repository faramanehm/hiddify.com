<div dir="ltr" markdown="1">

# Guide for domain fronting
Domain Frontig is one of the CDN services that can be used to bypass the filtering system. For example, what the GFW system sees is discord.com, but by using the host field, we set the main destination of the internet packets to our own server, and in this way, the filtering system is bypassed.

This feature has been disabled in Cloudflare CDN because malware used to exploit it, but other CDNs can be used for this purpose.

## Domain registration on CDN

- First, you need to register on the CDN site of your choice and register a domain in it. [Tutorial for domain registration](/manager/wiki/Domain-types-and-how-to-register-them)

- After that, register a DNS record and turn on its proxy tick.

## Domain fronting settings on Hiddify panel

To do this, go to the `Settings` and `Domains` section in the Hiddify panel and then click on `Create`.

<div align=center markdown=1>
![Screenshot_20230621_174231](https://github.com/hiddify/hiddify-config/assets/125398461/8a354ba2-a8c6-471b-8ab1-efbd1d189335)

</div>

- Set the domain mode to CDN.
- Enter your registered subdomain in the previous step, whose proxy is turned on.
- If you want, in the `Alias` field, put a desired name to be displayed in the configurations.
- In the `Enable TLS Domain Fronting`, you can enter the addresses of sites that use the CDN you want but are not filtered. Use [DNS Lookup tool](https://dns-lookup.com/) to find them. Find the right site here and put it in the domain fronting field.
- Finally, if needed, you can put the clean IPs for the desired CDN in the the field `Force Config to Use Following IPs` .

- The work is done. The desired CDN configs are set for domain fronting mode and you can use them.

## Add config to the subscription link

As you know, it is always recommended to keep subscription links separate from configs. Therefore, if you have already created a subscription link, just add the new CDN domain in its settings so that the new domain fronting configurations are also connected to the subscription link. [How to create subscription link on Hiddify](/manager/wiki/How-to-create-subscription-link-on-Hiddify)