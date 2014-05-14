Developing inside Slate entails creating new files and overriding inherited files within your site. Like with any site built with
Emergence, each Slate site is a layer of files applied on top of an inherited layer of files from the parent site. Layers are kept
separate from the perspective of the developer, but as far as the application code that runs the site is concerned there is only
one flat filesystem for it to load code and assets from.

The various components of Slate are laid out in a directory+file structure that should make it as easy as possible replace or
enhance any piece of it without impacting unrelated components, and the layer-based filesystem keeps track of what you've changed and
what you can continue to inherit from upstream.

Your goal while extending Slate should be to override as few files as possible. Each time you override a file, you become responsible
for keeping an eye on and integrating into your code any enhancements that get published to that file upstream. The less you override,
the easier you gain the benefit of improvements made upstream. In most cases, outside overriding Slate's core PHP classes, it should
be safe to ignore new versions of files you override and just miss out on enhancements that won't have an impact outside whatever
feature that particular file is responsible for.

Slate's core PHP classes are designed to enable you to configure and extend them as much as possible, either by extending existing PHP
classes, modifying config files, or even overriding classes altogether. Generally you should only override a Slate PHP class if you are
adding some new capability or flexibility that you will request be merged into Slate's upstream code.

## Next Steps

The remaining chapters in this section go into detail about each of the major root directories in Slate:

- [`site-root/...` -- Creating new pages and hosting files](site-root)
- [`php-config/...` -- Configuring server components with PHP](php-config)
- [`html-templates/...` -- Customizing HTML templates](html-templates)
- [`php-classes/...` -- Creating new server components with PHP](php-classes)