require "bundler/gem_tasks"

require 'rspec/core/rake_task'

RSpec::Core::RakeTask.new do |t|
  t.rspec_opts = ["-c", "-f progress", "-r ./spec/spec_helper.rb"]
  t.pattern = 'spec/**/*_spec.rb'
end

task :default => :spec

namespace :doc do
  project_root = File.dirname(__FILE__)
  doc_destination = File.join(project_root, 'rdoc')

  begin
    require 'rdoc'
    require 'yard'
    require 'yard/rake/yardoc_task'

    YARD::Rake::YardocTask.new(:generate) do |yt|
    yt.files   = Dir.glob(File.join(project_root, 'lib', '**', '*.rb'))
    yt.options = ['--output-dir', doc_destination, '--readme', 'README.md']
  end
  rescue LoadError
    desc "Generate YARD Documentation"
    task :generate do
      abort "Please install the YARD gem to generate rdoc."
    end
  end

  desc "Remove generated documenation"
  task :clean do
    rm_r doc_dir if File.exists?(doc_destination)
  end

end
