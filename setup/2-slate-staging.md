## Overview
You will want to start out with Slate by first creating a "staging" site. This instance of Slate will serve as your workspace
for customizing and testing out features of Slate. Later you will set up a "live" site for your actual users. The live site will
mirror your staging site, but have its own database and only be synchronized with your changes to the staging site on your command.

This setup enables you to experiment with changes and take some time implementing and testing them without interfering with your
users' experience. Once your new changes are perfected on the staging site, you can roll them out to the live site all at once.

## Prerequisite steps
- [Setting up an Emergence server](1-emergence)

## Create a staging site
1. Log in to your Emergence server's control panel (http://example.com:9083) as you left off at the end of [the previous step](1-emergence).

2. Click **Create Site**.

3. In the **Site Label** field, enter something like <kbd>My School Name (staging)</kbd>.

4. Tab to **Handle** and a handle will be suggested for your site. The handle will serve as a sort-of "username"
   for the site within other systems, so it needs to be simple, short, and unique. For your staging site, we recommend a handle
   ending in <kbd>-staging</kbd>.
   
   *Due to restrictions in other tools, handles must be 16 characters or less. If the system highlights your handle as an error, it
   may be too long.*

5. Tab to the **Primary Hostname** field and enter a
   [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) that will resolve to your Emergence server
   and be used to access your staging site.
   
   If your domain name is example.com, you might enter <kbd>slate-staging.example.com</kbd> here. Then create an "A record" in your
   domain control panel for example.com, pointing <kbd>slate-staging.example.com</kbd> to the IP address of your Emergence machine.

6. Tab to the **Alt. Hostnames** field. You can leave this field blank, or enter any number of additional hostnames that you want to
   use to access this staging site.

7. Tab to the **Parent Site** field and enter <kbd>v1.slate.is</kbd>.

8. Tab to the **Parent Access Key** field and enter <kbd>o9B11mbIXY1proH7</kbd> (this is the public inheritence key for v1.slate.is).

9. Under the **First User** section, fill in details for your initial account. This should be personal to you, and will give you access
   to log in and make changes to your Slate site and its code. You can create additional accounts for other developers, administrators,
   and users later on, from within Slate.

10. Finally, click **Save Site** and Emergence will set up the site instance for you. The new site will show up at the bottom of your
    sites list with a red marker to indicate that it's saving. Once the red marker disappears, your site is ready and you can open it
    through the primary hostname you assigned.

## Screencast
<iframe width="640" height="480" src="//www.youtube.com/embed/ZzFKJqgtRP4?rel=0" frameborder="0" allowfullscreen></iframe>

## Next steps
- [Creating a live site](3-slate-live)
- [Making changes to your staging site](4-making-changes)