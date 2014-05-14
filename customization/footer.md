## Overview
The footer is easy to customize, as its content is set apart in a standalone file with none of the more complex components essential to
Slate's functioning. You can override this file and make whatever changes to it you like, without worrying about breaking anything with
future updates to Slate.

## Default footer
The default footer, which you can open at `_parent/html-templates/includes/site.footer.tpl`, contains a tagline for Slate and a
commented-out template you can use to pleasantly format the school's name, address, and phone number:

```language-markup
<span class="info-line">
    Slate is an open-source web platform for schools.
</span>
<span class="info-line">
    Learn how you can use or build on Slate at
    <a href="http://slate.is">http://slate.is</a>.
</span>

{*
<address>
    <span class="info-line">MyTown High</span>
	<span class="info-line">123 Road St</span>
	<span class="info-line">MyTown, PA 19103</span>
	<span class="info-line">555-555-0155</span>
</address>
*}
```

## Example custom footer
By erasing the first two lines containing the Slate tagline, and the `{*` and `*}` lines that denote the start and end of a commented
out section, you can fill out the footer with your own school's address or other information.

Create the following file at `html-templates/includes/site.footer.tpl`, or open `_parent/html-templates/includes/site.footer.tpl`, make 
your changes, and hit save to automatically create the local override.

```language-markup
<address>
    <span class="info-line">MyTown High</span>
    <span class="info-line">123 Road St<span>
	<span class="info-line">MyTown, PA 19103</span>
	<span class="info-line">555-555-0155</span>
</address>
```