source 'http://rubygems.org'

# Replace 'git' with 'https' protocol
git_source(:github) do |repo_name|
  repo_name = "#{repo_name}/#{repo_name}" unless repo_name.include?("/")
  "https://github.com/#{repo_name}.git"
end

ruby '2.7.1'

gem "jekyll", "~> 4.0"
#gem "jekyll", github: "jekyll/jekyll"

#gem 'rack-jekyll', "~> 0.5"
gem 'rack-jekyll', github: "adaoraul/rack-jekyll"
gem 'rake'           # for running scripts
gem 'nokogiri'       # for qiita.rb
gem 'redcarpet'      # for rendering markdown files

# Gems to enable SSL
gem 'acme_challenge' # for authentication w/ LetsEncrypt
gem 'rack-rewrite'   # for redirection like http->https
gem 'rack-contrib'   # for managing CSP (cf. /config.ru)

# To enhance building time with Jekyll 4.0.0+
# https://github.com/yasslab/yasslab.jp/pull/123
gem "liquid-c"

# To run tasks triggered by GitHub Actions
group :actions, optional: true do
  gem 'idobata'           # All: Notify
  gem 'sanitize'          # RSS: Remove HTML tags
  gem 'activesupport'     # RSS: Time Calculation
  gem 'yaml'              # note: Upsert articles
  gem 'mechanize'         # note: Upsert articles
  gem 'google-api-client' # GCal: Access to Calendar
  gem 'multi_json'        # GCal: Access to Calendar
  gem 'gmail'             # Share inquiry from form
end

group :jekyll_plugins do
  gem "jekyll-include-cache"
  gem 'jekyll-sitemap'
end

group :development, :test do
  gem 'html-proofer'  # Static check for HTML tags
  gem 'rspec'

  # Gems for debugging
  gem 'pry'
  gem 'pry-byebug'
end

group :production do
  gem 'puma'
end
