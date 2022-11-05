---
layout: page
title: beta.studio.emptycup.in
---

This is a log of maintenance effort for [beta.studio.emptycup.in]().
<br><br>

### October 30: Broken HTTPS

- Broken HTTPS blocked access to [beta.studio.emptycup.in]()
- Luckily had [studio.emptycup3d.com]() linked to the old domain

### November 2: Shortcuts not working

- FC & FCFP for copying and pasting floorplans are not working in the new deployment
- WC for copying woodwork

### November 3: Payments are not working

- Payments are failing because Razorpay is not allowing payments from the new domain.
- Adding domain to our existing Razorpay account involves manual review and has been stuck for 2 days.

The root of the problem is the broken HTTPS. So, I tried to figure out what the issue is.
Netlify's automatic HTTPS renewal from Let's Encrypt is failing because Netlify doesn't
own the DNS for _emptycup.in_ and hence cannot validate certificate request.

So, I have to move all the DNS records to Netlify from Godaddy. Sadly, godaddy's DNS records extended
over 5 pages with a lot stale and junk records. It took a lot of time to identify the necessary records first.
I'm still not sure if I might break the domain validation for some service.

November 5:
- Moved all the DNS records from Godaddy to Netlify
- Moved the TXT used for validation also
- HTTPS got reenabled through automatic cert generation from Let's Encrypt.
- Tested mail addressing by sending a mail from _ab@emptycup.in_ to _admin@emptycup.in_


