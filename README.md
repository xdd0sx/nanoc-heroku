# Nanoc3 Template - HAML, SASS, Compass, CoffeeScript

## Prepare

    git clone git://github.com/meskyanichi/nanoc-template-hsccs.git my_site_name
    cd my_site_name && bundle install
    nanoc autocompile

Now visit `http://127.0.0.1:3000/` and there you go.

## Ready to roll with

* HAML
* SASS and the Compass framework
* CoffeeScript

## Also contains Rake tasks for

* RSync (fast / mirroring) deployment
* Optimizing JPG and PNG images (using jpegoptim/optipng OSX/Ubuntu packages)
* Compressing Stylesheet and JavaScript files (using YUI Compressor Gem)

### Credits

Initial work taken from [nanoc-base](https://github.com/johngrimes/nanoc-base) and modified to look more like the typical Rails layout.

All gems from the `Gemfile` updated to the latest version and working (as of writing). Rewrote the Rakefile to use YUI-Compressor gem for CSS/JS files, added a nice RSync wrapper for deployment (mirroring), added instructions for installing packages on OSX/Ubuntu for utilizing the JPG and PNG file optimizer rake tasks, moved files and folders around to give it a more Rails-like feel, and more!