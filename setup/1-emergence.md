## Overview
Slate requires an [Emergence](http://emr.ge)-managed Linux virtual machine for development and deployment.

You can follow [Emergence's setup docs](http://emr.ge/docs/setup) to prepare a fresh [Ubuntu 14.04](http://emr.ge/docs/setup/ubuntu/14.04), [Ubuntu 13.10](http://emr.ge/docs/setup/ubuntu/13.10),
[Ubuntu 13.04](http://emr.ge/docs/setup/ubuntu/13.04), or [Gentoo](http://emr.ge/docs/setup/gentoo) Linux machine to host Slate. **Ubuntu 14.04 is the recommended choice** because it has LTS (long-term support) status.

## Prerequisite steps
- Obtain a fresh Linux system -- typically a virtual machine from a provider like [Digital Ocean](https://www.digitalocean.com/?refcode=889859901aab) *(full
disclosure: this link has a referral code that will get us some credit if you sign up from it)*

## Screencast
<iframe width="640" height="480" src="//www.youtube.com/embed/md7_J_ol5TY?rel=0" frameborder="0" allowfullscreen></iframe>

## Optional tools

### wkhtmltopdf
To generate PDF reports, you'll need to install the latest stable wkhtmltopdf, it's best to use [a binary distributed by the project](http://wkhtmltopdf.org/downloads.html):
```
wget https://bitbucket.org/wkhtmltopdf/wkhtmltopdf/downloads/wkhtmltox-0.13.0-alpha-7b36694_linux-trusty-amd64.deb
sudo dpkg -i wkhtmltox-0.13.0-alpha-7b36694_linux-trusty-amd64.deb
```

## Next steps
- [Creating a staging site](2-slate-staging)
