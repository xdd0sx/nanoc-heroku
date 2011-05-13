##
# Load Nanoc3 tasks for additional validators
#
# require 'nanoc3/tasks'

##
# RSync-based deployment
#
# Performant/Fast mirroring with RSync:
#  Will compress data during transfer to lower bandwidth and improve transfer speed.
#  Will output human readable data.
#  Will mirror the local output directory with the remote server,
#  remote files that don't exist locally will be deleted.
#
# Modify the "puts %x[rsync ...]" line
#
desc 'Deploy the static site via RSync'
task :deploy do
  puts 'RSyncing website..'
  puts %x[rsync -avhz --progress --delete output/ deployer@sample.com:path/to/my/site/]
end

##
# Same as :deploy, except that it first optimizes all
# JPG, PNG, Stylesheet and JavaScript files before deploying
#
desc 'Deploy the static site via RSync after optimization'
task :deploy_optimized => ['optimize:all', :deploy]

##
# A couple of rake tasks that'll optimize JPG, PNG, JavaScripts and Stylesheet files
#
namespace :optimize do

  ##
  # Gem Requirement:
  #  YUI-Compressor - Bundled in Gemfile
  #
  desc 'Compress all stylesheet files'
  task :stylesheets do
    require 'yui/compressor'
    compressor = YUI::CssCompressor.new

    Dir['output/**/*.css'].each do |stylesheet|
      puts "Compressing Stylesheet: #{stylesheet}"
      css = File.read(stylesheet)
      File.open(stylesheet, 'w') do |file|
        file.write(compressor.compress(css))
      end
    end
  end

  ##
  # Gem Requirement:
  #  YUI-Compressor - Bundled in Gemfile
  #
  desc 'Compress all javascript files'
  task :javascripts do
    require 'yui/compressor'
    compressor = YUI::JavaScriptCompressor.new(:munge => true)

    Dir['output/**/*.js'].each do |javascript|
      puts "Compressing JavaScript: #{javascript}"
      js = File.read(javascript)
      File.open(javascript, 'w') do |file|
        file.write(compressor.compress(js))
      end
    end
  end

  ##
  # Package Requirement:
  #  jpegoptim
  # Install OSX:
  #  brew install jpegoptim
  # Install Ubuntu:
  #  [apt-get | aptitude] install jpegoptim
  #
  desc 'Optimize JPG images in output/images directory using jpegoptim'
  task :jpg do
    puts `find output/images -name '*.jpg' -exec jpegoptim {} \\;`
  end

  ##
  # Package Requirement:
  #  optipng
  # Install OSX:
  #  brew install optipng
  # Install Ubuntu:
  #  [apt-get | aptitude] install optipng
  #
  desc 'Optimize PNG images in output/images directory using optipng'
  task :png do
    puts `find output/images -name '*.png' -exec optipng {} \\;`
  end

  ##
  # Convenient task for performing all optimization techniques at once
  #
  desc 'Optimize all JPG, PNG, Stylesheet and JavaScript files in the output directory'
  task :all => [:jpg, :png, :javascripts, :stylesheets]
end
