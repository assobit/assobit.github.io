# This is to ensure that when you perform `bundle install` you have the correct versions
#  of the github-pages gem as explained in http://jekyllrb.com/docs/github-pages/
source 'https://rubygems.org'

require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'github-pages', versions['github-pages']
