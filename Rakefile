require 'bundler/gem_tasks'

desc "Invokes the test suite in multiple RVM environments"
task :'test!' do
  %w[1.3 1.4 master].each do |version|
    env = "env sinatra=#{version}"
    system("rm -f Gemfile.lock; #{env} bundle && #{env} bundle exec rake test") or abort
  end
end

desc "Runs tests"
task :test do
  Dir['test/*_test.rb'].each { |f| load f }
end

task :default => :test

repo = ENV['GITHUB_REPO'] || 'rstacruz/sinatra-backbone'
namespace :doc do
  desc "Builds documentation"
  task :build do
    # github.com/rstacruz/reacco
    analytics = "--analytics #{ENV['ANALYTICS_ID']}"  if ENV['ANALYTICS_ID']
    system "reacco --literate --toc --api lib --github #{repo} #{analytics}"
  end

  desc "Uploads documentation"
  task :deploy => :build do
    # github.com/rstacruz/git-update-ghpages
    system "git update-ghpages -i doc #{repo}"
  end
end

task :doc => :'doc:build'
