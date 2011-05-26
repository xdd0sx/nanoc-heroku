# Nanoc3 Template - HAML, SASS, Compass, CoffeeScript

## Prepare

    git clone git://github.com/meskyanichi/nanoc-template-hsccs.git my_site_name
    cd my_site_name && bundle install

## Start the file server

Move in to the root directory of the new website and run:

    cd /path/to/my_site_name
    nanoc view

## Auto-compiling when you update files

Move in to the root directory of the new website in a new shell window and run:

    cd /path/to/my_site_name
    guard start

Now visit `http://127.0.0.1:3000/` and there you go. This should display your website. Each time you update a file that changes the look of the web page, Guard will run the nanoc compiler to update the end result which you can directly view in the browser.

## Templating and Scripting with

* HAML
* SASS with the Compass framework
* CoffeeScript
* Markdown
* Builder


## Auto-compiling with

* Guard when files are changed


## Also contains Rake tasks for

* RSync (fast / mirroring) deployment
* Optimizing JPG and PNG images (using jpegoptim/optipng OSX/Ubuntu packages)
* Compressing Stylesheet and JavaScript files (using YUI Compressor Gem)


## Credits

Initial work taken from [nanoc-base](https://github.com/johngrimes/nanoc-base) and further improved in various ways.

All gems from the `Gemfile` updated to the latest version and working (as of writing). Rewrote the Rakefile to use YUI-Compressor gem for CSS/JS files, added a nice RSync wrapper for deployment (mirroring), added instructions for installing packages on OSX/Ubuntu for utilizing the JPG and PNG file optimizer rake tasks, moved files and folders around to give it a more Rails-like feel, and more!