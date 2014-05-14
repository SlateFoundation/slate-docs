## Overview
All the HTML rendered by Slate is generated from template (`.tpl`) files stored within the `html-templates` tree. These templates are
rendered with the [dwoo-1.x templating engine](https://github.com/Seldaek/Dwoo).

## Why Dwoo?
Dwoo provides an extensible templating engine with many advanced features, such as subtemplates, plugins, and template inheritance,
unmatched by most other template engines. Of those that do match it in features, popular options like Twig attempt to create a
restrictive "sandboxed" environment for templates, using unreliable techniques, in an attempt to prevent template authors from running
arbitrary PHP code. Dwoo, on the other hand, aims more to provide syntactical sugar while allowing unrestricted access to core PHP
functions, application classes, and code blocks.

For example, in a Dwoo template for Slate, you can invoke a static method on a model class to retrieve and render some data you want to
present. Under a sandboxed templating engine, you would need to create a new template "glue" plugin just to grab that data, or you could
modify the controller generating the response to include some data unrelated to its core purpose.

(See [&rarr;&nbsp;Include the latest 3 blog posts in your site-wide sidebar](#example-sidebar-blog) below.)

## Response rendering
Whenever you open a URL on a Slate site with your web browser, a PHP script or static file within [`site-root`](site-root) will be
matched to the requested path to fulfill the request. If a PHP script handles the request and uses
`RequestHandler::respond($responseId)` or the lower-level method `Emergence\Dwoo\Engine::respond($responseId)` to render its response,
Emergence will search for a template suitable to render the response by combining the identifier supplied via `$responseId` and the
public-facing route of the script that fired the response, truncating the route from right to left until a template is found.

For example, if you visit <kbd>/sections/ENG101-027/delete</kbd> and the controller for that request fires a response with a
`$responseId` value of `'confirm'`, the `html-templates` tree will be searched in the following order:

1. `html-templates/sections/ENG101-027/delete/confirm.tpl`
2. `html-templates/sections/ENG101-027/confirm.tpl`
3. `html-templates/sections/confirm.tpl`
4. `html-templates/confirm.tpl`

In an unmodified Slate site, path #4 is the first that matches an existing file, so `html-template/confirm.tpl` is used to generate the
response. But you could create a special version of the confirm page for course sections, or even for a specific section, by placing a
template at one of the deeper paths.

## Special template directories
The following directories do not behave in any way differently than any other directories within `html-templates`, but by organizational
convention are used for special purposes:

### The `designs` directory
This directory is intended to contain master templates that other, page-specific templates can extend. `site.tpl` is the standard
master template for built-in pages, but you could add additional design templates here -- they could even themselves extend `site.tpl`.
Templates in this directory *should* include opening and closing `<html>` tags with `{block}`s designated for, at minimum, a `content`
and `title` section.

### The `includes` directory
Templates in this directory contain fragments of markup that are either `{include}`ed on multiple pages, or just broken out so they can
be overridden individually. See [&rarr;&nbsp;Customizing site footer](../customization/footer) for an example use case.

### The `subtemplates` directory
Files in this directory contain one or more named `{template}` blocks, defining a reusable fragment of markup that can be rendered
against a set of parameters. These parameters can have default values. Many such blocks are listed in
`html-templates/designs/site.subtemplates.tpl`,  which defines a set of subtemplates that are universally available for any pages
extending `html-templates/designs/site.tpl`. Other subtemplate files can be included only individual pages though using the
`{load_templates}` method.

## Examples
### Include the latest three blog posts in your site-wide sidebar {#example-sidebar-blog}
Override `html-templates/includes/site.sidebar.tpl` and insert this block:

```language-markup
{load_templates "subtemplates/people.tpl"}
<ul class="sidebar-item latest-blogposts">
{foreach item=BlogPost from=Emergence\CMS\BlogPost::getRecentlyPublished(3)}
    <li>
        <a href="{$BlogPost->getURL()}">{$BlogPost->Title|escape}</a>
        by {personLink $BlogPost->Author}
    </li>
{/foreach}
</ul>
```