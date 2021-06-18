source "https://rubygems.org"

require "json"
require "open-uri"
versions = JSON.parse(URI.open("https://pages.github.com/versions.json").read)

ruby versions["ruby"]

gem "github-pages", versions["github-pages"]
gem "json"

group :test do
  gem "html-proofer"
end
