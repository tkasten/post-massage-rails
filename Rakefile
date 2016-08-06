require 'bundler'
Bundler::GemHelper.install_tasks

# Check if versions are correct between VERSION constants and .js files
#
task :release => [:guard_version]

task :guard_version do
  def check_version(file, pattern, constant)
    body = File.read("vendor/assets/javascripts/#{file}")
    match = body.match(pattern) or abort "Version check failed: no pattern matched in #{file}"
    file_version = body.match(pattern)[1]
    constant_version = PostMassage::Rails.const_get(constant)

    unless constant_version == file_version
      abort "PostMassage::Rails::#{constant} was #{constant_version} but it should be #{file_version}"
    end
  end

  check_version('post-massage.js', /Version: ([\S]+)/, 'POST_MASSAGE_VERSION')
end

task :update_post_massage do
  puts "Downloading post-massage.js"
  puts `curl -o vendor/assets/javascripts/post-massage.js https://raw.githubusercontent.com/tkasten/postMassage/master/src/post-massage.js`

  puts "Updating version.rb"
  version = false
  File.foreach('vendor/assets/javascripts/post-massage.js') do |line|
    version = line.match(/Version: ([\S]+)/)
    version = version && version[1]
    break if version
  end

  version_path = 'lib/post_massage/rails/version.rb'
  lines = IO.readlines(version_path).map do |line|
    line.gsub(/POST_MASSAGE_VERSION = "([\d\.]+)"/, "POST_MASSAGE_VERSION = \"#{version}\"")
  end
  File.open(version_path, 'w') do |file|
    file.puts lines
  end

  puts "\e[32mDone!\e[0m"
end
