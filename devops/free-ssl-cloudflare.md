# Free SSL from Cloudflare

<img width="998" alt="image" src="https://user-images.githubusercontent.com/24983797/178022718-40d97560-1c49-4ad0-95b5-40bcae128cc1.png">

> SSL, or Secure Sockets Layer, is an encryption-based Internet security protocol. It was first developed by Netscape in 1995 for the purpose of ensuring privacy, authentication, and data integrity in Internet communications. SSL is the predecessor to the modern TLS encryption used today.  
> A website that implements SSL/TLS has `https` in its URL instead of `http`.  
> (Source: [Cloudflare Learning](https://www.cloudflare.com/learning/ssl/what-is-ssl/))

[tl:dr; 👉 Click to read why I recommend Cloudflare](#👍-the-best-ux-for-a-free-ssl)

## Background

SSL certificates are becoming more important for even relatively small projects. Browsers have started displaying scary warnings when visiting sites without SSL and there are SEO implications as well. Many people think you need to **pay** for the added security an SSL provides. I knew a company that paid good taxpayer money for an SSL, then had issues when it expired after the person that set it up left the company. For their use case, [Cloudflare's](#the-best-ux-for-a-free-ssl) free SSL would have provided more than enough security, saved taxpayer money, and avoided headaches with expiration and renewal. Don't be like that company!

Worse still, even in 2022 I still see some company websites without an SSL certificate. Does this inspire confidence?

<img width="515" alt="image" src="https://user-images.githubusercontent.com/24983797/178032378-4cad421a-32e8-42e5-83fb-aed8645cc733.png">

Don't be like this company either!

## Do I need an SSL?

Yes. See this brief [intro](https://www.cloudflare.com/learning/ssl/what-is-an-ssl-certificate/) and a more detailed [explanation](https://www.cloudflare.com/ssl/) from Cloudflare, and another one from Google about [SSL and SEO](https://developers.google.com/search/blog/2014/08/https-as-ranking-signal).

## The 2nd best option (in my opinion)

One popular free SSL option is Let's Encrypt. They certainly have great SEO and marketing. They provide a great service at a price that can't be beat but unfortunately, (as far as I know at the time of writing) their certificates expire every 90 days and can only be auto-renewed in certain majority of cases. Also, setup requires some technical knowledge. While growing one's technical knowledge is certainly a benefit, there is a bit of a learning curve and it's possible to make mistakes as a beginner. That's why, I don't think Let's Encrypt is the best option.

## 👍 The best UX for a free SSL

[Cloudflare](https://www.cloudflare.com/ssl/) is my favorite free SSL provider (of the 2 I've tried 😅). I was shocked how quick and easy the setup was. Let's Encrypt doesn't have a **difficult** setup, but it's definitely more technically involved (last time I did it). Cloudflare's certificates can also auto-renew in more cases. Their free plan also includes some DDOS protection and CDN benefits. They made the UX (or maybe DX?) so simple! Hope it helps!
