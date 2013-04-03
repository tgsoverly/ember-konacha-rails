# Ember::Konacha::Rails

## Important

Still experimental! Please help improve it :)


## What?

This gem has the stated goal of making it _easy_ to setup a good testing infrastructure for testing your *Ember-Rails* apps.

    $ rails g

```
...

EmberKonacha:
  ember_konacha:controller_spec
  ember_konacha:helper_spec
  ember_konacha:install
  ember_konacha:model_spec
  ember_konacha:view_spec

...  
```

An `install` generator is included for initial infrastructure setup!

Configures your Ember app with *Konacha* using a Javascript driver (poltergeist for PhantomJS by default). Adds the basic Konacha infrastructure so you can start writing tests/specs.

Can generate *Konacha* spec-skeletons for:

* models
* controllers
* views
* helpers

Please help provide more skeleton generators or improve the existing ones!!! :)

## Installation



Add this line to your application's Gemfile:

    gem 'ember-konacha-rails', github: 'kristianmandrup/ember-konacha-rails'

And then execute:

    $ bundle

Or (in the near future) install it yourself (from rubygems) as:

    $ gem install ember-konacha-rails

## Usage

Install basic Konacha infrastructure

    $ bundle exec rails g ember_konacha:install

Files that should be generated

```
vendor/assets/javascripts/sinon.js

spec/javascripts/spec_helper.js.coffee
spec/javascripts/support/sinon_mvc_mocks.js.coffee
spec/javascripts/support/koncha_config.js.coffee

spec/javascripts/app/router_spec.js.coffee
spec/javascripts/app/store_spec.js.coffee
```

Run Koncha!

    $ bundle exec rake konacha:run

Note: make sure that the following is at the end of your `application.js.coffee` file:

```javascript
window.App = Ember.Application.create LOG_TRANSITIONS: true

# Defer App readiness until it should be advanced for either
# testing or production.
App.deferReadiness()
```

(or similar for pure javascript)

The basic test setup/configuration can be found in `support/koncha_config.js.coffee` and `spec_helper.js.coffee` files.

The `spec_helper` initializes the app explicitly using `App.advanceReadiness()` within `Ember.run` in the `beforeEach` closure. To run your app in the browser, while also allowing for testing, you need to explicitly call `App.advanceReadiness()` when your DOM is ready.

To see install options, run:

    $ bundle exec rails g ember_konacha:install --help

Note: To avoid having to `bundle exec` install the gem in your current system gem repository, using `gem install ember_konacha` (when this is an official gem!).

### Generate Controller spec

    $ bundle exec rails g ember_konacha:controller_spec Login

`spec/javascripts/controllers/login_controller_spec.js.coffee`

    $ bundle exec rails g ember_konacha:controller User --type object

`spec/javascripts/controllers/user_controller_spec.js.coffee`

    $ bundle exec rails g ember_konacha:controller_spec Users --type array

`spec/javascripts/controllers/users_controller_spec.js.coffee`

### Generate Model spec

    $ bundle exec rails g ember_konacha:model_spec User

`spec/javascripts/models/user_spec.js.coffee`

### Generate View spec

    $ bundle exec rails g ember_konacha:view_spec NewUser

`spec/javascripts/views/new_user_view_spec.js.coffee`

### Generate Helper spec

    $ bundle exec rails g ember_konacha:model_spec Gravitation

`spec/javascripts/helpers/gravitation_helper_spec.js.coffee`

## Contributing

Please help make it easier for developers tp get started using TDD (or BDD) for Ember with Rails.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
