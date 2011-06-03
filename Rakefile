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
desc 'Deploy the website via RSync after re-compiling from scratch for production and optimizing all assets'
task :deploy => ['recompile', 'optimize:all'] do
  puts 'Deploying website..'
  puts %x[rsync -avhz --progress --delete --rsh='ssh -p22' output/ deployer@sample.com:path/to/my/site/]

  puts 'Finished deploying! Re-compiling for development mode..'
  change_base_url_to('http://localhost:3000')
  compile!
end

desc 'Re-compile the website from scratch for deployment'
task :recompile do
  change_base_url_to('http://mydomain.com')
  compile!
end

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

##
# Use this method to change the base url in the configuration file
# so you can automate that instead of manually changing it everytime
# when you want to deploy the website
#
def change_base_url_to(url)
  puts "Changing Base URL to #{url}.."
  config = YAML.load_file('./config.yaml')
  config['base_url'] = url
  File.open('./config.yaml', 'w') do |file|
    file.write(config.to_yaml)
  end
end

##
# Re-compile by removing the output directory and re-compiling
#
def compile!
  puts "Compiling Website.."
  %x[rm -rf output]
  %x[nanoc compile]
end
