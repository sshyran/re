#!/usr/bin/env ruby"

require 'rake/clean'
require 'rake/testtask'
require 'rake/rdoctask'

require 'lib/re'

task :default => :test

Rake::TestTask.new(:test) do |t|
  t.warning = true
  t.verbose = false
  t.test_files = FileList['test/*_test.rb']
end

namespace "release" do
  task :new => [
    :check_non_beta,
    :readme,
    :commit_new_version,
    :gem,
    "publish:rdoc"
  ]
  
  task :commit_new_version do
    sh "git commit -m 'bumped to version #{Re::VERSION}'"
  end
  
  task :check_non_beta do
    fail "Must not be a beta version! Version is #{Re::VERSION}" if Re::Version::BETA
  end
end
task :release => "release:new"
