source 'https://rubygems.org'

require 'json'
require 'open-uri'
begin
  versions = JSON.parse(open('https://pages.github.com/versions.json').read)
  gem 'github-pages', versions['github-pages']
rescue SocketError
  gem 'github-pages', 28
end
