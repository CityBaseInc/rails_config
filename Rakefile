begin
  require "bundler"
  Bundler::GemHelper.install_tasks
rescue Exception => e
end

require "rake"
require "rspec"
require "rspec/core/rake_task"
require "bundler/gem_tasks"
require "gemfury/tasks"

RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.pattern = "spec/**/*_spec.rb"
end

RSpec::Core::RakeTask.new('spec:progress') do |spec|
  spec.rspec_opts = %w(--format progress)
  spec.pattern = "spec/**/*_spec.rb"
end

require "rdoc/task"
Rake::RDocTask.new do |rdoc|
  rdoc.rdoc_dir = "rdoc"
  rdoc.title = "Rails Config #{RailsConfig::VERSION}"
  rdoc.rdoc_files.include("README*")
  rdoc.rdoc_files.include("lib/**/*.rb")
end

task :default => :spec

Rake::Task['release'].clear

desc "Tag and release to gemfury under the 'citybase' organization"
task 'release' => 'release:source_control_push'  do
  Rake::Task['fury:release'].invoke('rails_config.gemspec', 'citybase')
end
