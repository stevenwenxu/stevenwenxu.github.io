source "https://rubygems.org"

gem "jekyll", "~> 4.4"

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-redirect-from"
  gem "jekyll-remote-theme"
  gem "jekyll-seo-tag"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :windows, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1", :platforms => [:windows]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
# do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
