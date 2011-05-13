# Nanoc Template - HAML, SASS, Compass, CoffeeScript

### Prepare

    git clone git://github.com/meskyanichi/nanoc-template-hsccs.git my_site_name
    cd my_site_name && bundle install
    nanoc autocompile

Now visit `http://127.0.0.1:3000/` and there you go.

### Ready to roll with

* HAML
* SASS and the Compass framework
* CoffeeScript

### Also contains Rake tasks for

* Optimising JPEG and PNG images (using jpegoptim and optipng)
* Compressing CSS files (using YUI Compressor)
* Compressing JavaScript files (using YUI Compressor)
* Compressing HTML and XML files (using htmlcompressor)

### Credits

Template taken from [nanoc-base](https://github.com/johngrimes/nanoc-base) and modified to look more like the typical Rails layout. All gems from the `Gemfile` updated to the latest version and working.