---
title: How do redirects work in the static site?
description: Redirect URLs in your WordPress static website generated by WP2Static.
weight: 60
---

> Our sites deal with a lot of 301 redirects to other websites. We currently use a plugin like [SEO Redirection Plugin](https://wordpress.org/plugins/seo-redirection/) I'm not a coder so this question may be dumb, but if I use WP2Static to convert our WP sites to static, would all of the redirects set up with our re-direct plugins remain in place? I'm thinking "no" because they don't edits htaccess but rather handle that redirect through WP if I understand correctly. Any advice? Thank you :)

---

Great question, thanks for asking!

You're spot on - those .htaccess redirects won't be deployed to your static site automatically.

The current solution will depend on your deployment method:

 - for Netlify, using our Add-on, we provide a field for entering your redirects
 - for Netlify manual, you'll need to download and extract the ZIP, add in a Netlify [\_redirects](https://docs.netlify.com/routing/redirects/) file, zip it up again and deploy
 - for deployment *to* servers utilizing an `.htaccess` file, you may be able to copy your existing `.htaccess` file, adjusting the URL patterns as required
 - for Amazon S3/CloudFront, you can [setup redirects within S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/how-to-page-redirect.html#page-redirect-using-console) or if using CloudFront, you can attach a Lambda function that handle redirects to your distribution's behaviour
 - for GitHub Pages, GitLab or BitBucket, you may be able to use a symlink to redirect traffic to a new path, but this may not give you the ability to choose the http status code. A last-resort for all deployment methods is to create an HTML page containing a meta refresh like `<meta http-equiv="refresh" content="0; url=http://example.com/" />` (you may also want to include a canonical link tag just to be sure of no duplicate content indexing).
 - for Cloudflare Workers, you can either define the 301's in your functions's code or within the Page Rules section of the Cloudflare admin

Redirects are an important part of sites for SEO and user experience, so we'll try to come up with a more seamless experience in the future. Some discussions have been had with users about this and we've got some ideas in mind.

Got some other ideas on how to deal with redirects? [Contact us](/contact).