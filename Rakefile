require "bundler/setup"
#require "jekyll/task/i18n"

task default: 'assets:precompile'

# Override assets:precompile script on Heroku deployment
namespace :assets do
  task :precompile do
    Rake::Task['clean'].invoke
    # sh 'npm install'
    sh 'ls -a ./node_modules'
    sh 'JEKYLL_ENV=production bundle exec jekyll build'
  end
end

# cf. How to test a Jekyll site
# http://joenyland.me/blog/how_to_test_a_jekyll_site/
require 'html-proofer'
task test: [:build] do
  sh "bundle exec rake assets:precompile" unless ENV['SKIP_BUILD'] == '1'

  require './test/custom_checks'
  options = {
    allow_hash_href:  true,
    check_opengraph:  true,
    check_favicon:    true,
    check_html:       true,
    disable_external: true,
    file_ignore: [
      /node_modules/,
      "./_site/ja/workshops/raspi/index.html",
      "./_site/en/workshops/raspi/index.html",
      "./_site/ja/workshops/tickle/index.html",
      "./_site/google02f5cc9ed3681f94.html"
    ],
    url_ignore:  %w(coderdojo.com linkedin.com),
    http_status_ignore: [0, 500, 999],
  }

  HTMLProofer.check_directory('./_site', options).run
end

task build: [:clean] do
  system 'bundle exec jekyll build'
end

task :clean do
  system 'bundle exec jekyll clean'
end

#Jekyll::Task::I18n.define do |task|
#  task.locales = ["ja"]
#  task.translator_name  = "Yohei Yasukawa"
#  task.translator_email = "yohei@yasslab.jp"
#  task.files =  Rake::FileList["**/*.md"]
#  task.files -= Rake::FileList["_*/**/*.md"]
#  task.locales.each do |locale|
#    task.files -= Rake::FileList["#{locale}/**/*.md"]
#  end
#end
#
#task default: "jekyll:i18n:translate"
