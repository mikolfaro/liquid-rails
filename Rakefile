# frozen_string_literal: true

require 'bundler/gem_tasks'
require 'rspec/core'
require 'rspec/core/rake_task'

RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.pattern = FileList['spec/**/*_spec.rb']
end

task default: 'spec:all'

namespace :spec do
  rails_versions = %w[rails_60 rails_61 rails_70 rails_80]
  rails_versions.each do |gemfile|
    desc "Run Tests against #{gemfile}"
    task gemfile => :environment do
      sh "BUNDLE_GEMFILE='gemfiles/#{gemfile}.gemfile' bundle --quiet"
      sh "BUNDLE_GEMFILE='gemfiles/#{gemfile}.gemfile' bundle exec rake spec"
    end
  end

  desc 'Run Tests against rails versions'
  task all: :environment do
    rails_versions.each do |gemfile|
      sh "BUNDLE_GEMFILE='gemfiles/#{gemfile}.gemfile' bundle --quiet"
      sh "BUNDLE_GEMFILE='gemfiles/#{gemfile}.gemfile' bundle exec rake spec"
    end
  end
end
