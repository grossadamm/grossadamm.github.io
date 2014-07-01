---
layout: post
title: Making requirejs, jasmine, and rails all play nice
---

I like tests. It's somewhat unhealthy. I also work on the web and so I enjoy javascript quite a bit. So I set out on making our test suite on our new rails site also test our javascript modules. 

I take absolutely no credit for any of this. If your hard work is listed here, let me know and I will cite you. I tried to cite everything I could remember.

On to the goodness...

## RequireJS General Setup

Follow the instructions at [requirejs-rails] [1]. 

1. Add the gem to your `Gemfile` and dont' forget to `bundle`:
```
gem 'requirejs-rails`
```

2. Cleanout your `application.js` of all `\\=` type requirements.
3. In `layouts/application.html.erb` replace `<%= javascript_include_tag 'application' %>` with `<%= requirejs_include_tag "application" %>` 

## Make RequireJS work with jquery ui and ujs

I had to make some modifications to make jquery ui and jquery ujs start working again. 

Place your jquery-ui.js file into `/vendor/assets/javascripts/jquery-ui.js` 


`/config/requirejs.yml`

```
shim:
  'jquery-ui':
    deps: ['jquery']
    exports: '$'
  'jquery_ujs':
    - 'jquery'

map:
  '*':
    'jquery': 'jquery_with_rails_ujs'
  'jquery_ujs': 
    'jquery': 'jquery' 
  'jquery_with_rails_ujs': 
    'jquery': 'jquery' 
```

## Make sure requirejs is working like it should

First, we create a global module that just sends a message to the console.

`/app/assets/javascripts/global.js`

```
define(['jquery', 'jquery-ui'], function(routes) {
	var init = function() {
		$(function() {
			console.log('hi there!');
		})
	}

	return {
		init: init
	}
})
```

Second in our application.js file we are going to require our module.
`/app/assets/javascripts/application.js`

```
require(['global'], function(global) {
	global.init();
})
```

If you open up your browser you should get a message on your console.

## Setup Jasmine-rails

Follow the instructions at [Jasmine-Rails] [6]. 

>First, add jasmine-rails to your Gemfile, like so
>
>````
>    group :test, :development do
>      gem 'jasmine-rails'
>    end
>````
>Next:
>
>```
>$ bundle install
>```
>
>And finally, run the Rails generator:
>
>```
>$ rails generate jasmine_rails:install
>```
>
>The generator will create the necessary configuration files and mount a test
runner to [/specs](http://localhost:3000/specs) so that you can get started
writing specs!

I also went ahead and modified my `jasmine.yml` as follows:

```
src_dir: "app/assets/javascripts"

css_dir: "app/assets/stylesheets"

css_files:

spec_dir: spec/javascripts

helpers:
  - "helpers/**/*.{js}"

spec_files:
  - "**/*[Ss]pec.{js}"

tmp_dir: "tmp/jasmine"
```

## Make Jasmine-Rails play nice with requirejs

>Create a custom layout in `app/views/layouts/jasmine_rails/spec_runner.html.erb` and reference your helper:
>
>If you wanted to do something like this using [requirejs-rails](https://github.com/jwhitley/requirejs-rails), your helper
might look like this:
>
>```ruby
># in lib/jasmine_rails/spec_helper.rb
>module JasmineRails
>  module SpecHelper
>    # Gives us access to the require_js_include_tag helper
>    include RequirejsHelper
>  end
>end
>```
>
>Remove any reference to `src_files` in `spec/javascripts/support/jasmine.yml`, to ensure files aren't loaded prematurely.
>
>Create your custom layout `app/views/layouts/jasmine_rails/spec_runner.html.erb` like so:
>
>```erb
>
><!DOCTYPE html>
><html>
>  <head>
>    <meta content="text/html;charset=UTF-8" http-equiv="Content-Type"/>
>    <title>Jasmine Specs</title>
>
>    <%= stylesheet_link_tag *jasmine_css_files %>
>    <%= requirejs_include_tag %>
>    <%= javascript_include_tag *jasmine_js_files %>
>  </head>
>  <body>
>    <div id="jasmine_content"></div>
>    <%= yield %>
>  </body>
></html>
>
>```


## jasmine-fixture and jasmin-jquery

Both  [Jasmine-Jquery] [4], and [Jasmine-Fixture] [5] need to be converted to modules to work correctly.

Replace `(function($) {` with `require(['jquery'], function($) {` at the beginning of both files. 

Here are gists of my modified [jasmine-fixture] [7] and my modified [jasmine-jquery] [8] for quick references. 

Place the modified files into `/spec/javascripts/helpers/`.

## Let's actually write a test!

`/spec/javascripts/javascripts/global_spec.js`

```
require(['global', 'jquery'], function(global) {
	describe('Global', function() {

		it("is defined", function() {
			expect(typeof global).toBe('object')
			expect(typeof global.init).toBe('function')
		})
	});
);
```

If you run `rake spec:javascript` or open your browser and point it to `/specs` you should see a passing test!

## Include those javascript tests in rspec!

Create `/spec/features/javascript_spec.rb`, this method does require capybara and a way to run js on capybara (capybara-webkit is what I'm using)

```
require 'spec_helper'
 
feature 'Jasmine suite', :js do
  def run_jasmine_tests
    visit '/specs'
  end
 
  scenario "running all the javascript tests" do
    run_jasmine_tests

    expect(page).to have_css('.passed')

    if page.has_css?(".failed")
      messages = []
      all('.spec-detail.failed .description').each_with_index do |spec, index|
        messages << "#{index + 1}. #{spec.text}"
      end
      messages.unshift("Jasmine suite failed with #{messages.size} failures")

      fail messages.join("\n")
    end
  end
end
```


[1]:https://github.com/jwhitley/requirejs-rails
[3]:http://jasmine.github.io/2.0/introduction.html
[4]:https://github.com/velesin/jasmine-jquery
[5]:https://github.com/searls/jasmine-fixture
[6]:https://github.com/searls/jasmine-rails
[7]:https://gist.github.com/grossadamm/11add4b4681df3a23804
[8]:https://gist.github.com/grossadamm/a4f6997a369d30eb5110
