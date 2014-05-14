## Overview
Your live Slate site will be a mirror of your staging site, where you can apply a minimal number of configuration changes on top of
staging to tune your instance for production. It also serves to hold back changes you make on staging from your users until you are
ready to publish them.

## Prerequisite steps
- [Creating a staging site](2-slate-staging)

## Create a live site
1. Log in to your Emergence server's control panel (http://example.com:9083).

2. Right click on the row for the staging site you created in [the previous step](2-slate-staging).

3. Select **Create inheriting site**.

4. In the **Site Label** field, enter something like <kbd>My School Name</kbd>.

4. Tab to **Handle** and a handle will be suggested for your site. The handle will serve as a sort-of "username"
   for the site within other systems, so it needs to be simple, short, and unique. For your live site, we recommend a handle
   matching your staging site's handle, but without the <kbd>-staging</kbd> suffix.
   
   *Due to restrictions in other tools, handles must be 16 characters or less. If the system highlights your handle as an error, it
   may be too long.*

5. Tab to the **Primary Hostname** field and enter a
   [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) that will resolve to your Emergence server
   and be used to access your live site.
   
   If your domain name is example.com, you might enter <kbd>slate.example.com</kbd> here. Then create an "A record" in your domain
   control panel for example.com, pointing <kbd>slate.example.com</kbd> to the IP address of your Emergence machine.

6. Tab to the **Alt. Hostnames** field. You can leave this field blank, or enter any number of additional hostnames that you want to
   use to access this staging site.

7. Under the **First User** section, fill in details for your initial account. This should be personal to you, and will give you access
   to log in and make changes to your Slate site and its code. You can create additional accounts for other developers, administrators,
   and users later on, from within Slate.

8. Finally, click **Save Site** and Emergence will set up the site instance for you. The new site will show up at the bottom of your
   sites list with a red marker to indicate that it's saving. Once the red marker disappears, your site is ready and you can open it
   through the primary hostname you assigned.

## Screencast
<iframe width="640" height="480" src="//www.youtube.com/embed/Xj7VAqJky1Q?rel=0" frameborder="0" allowfullscreen></iframe>

## Next steps
- [Making changes to your staging site](4-making-changes)
- [Publishing changes to your live site](5-publish-changes)