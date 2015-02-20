# Figaro
The Figaro gem lets us declare environment variables, both locally and on heroku. To use it, first add the gem.

    gem “figaro”

Then, set it up with

    figaro install

This creates config/application.yml, a simple yaml file, as well as adds that file to your gitignore. Figaro sets these values to your ENV hash (or the proxy Figaro.env).You can use it in your app like this:

    client = Twitter::REST::Client.new do |config|
      config.consumer_key        = Figaro.env.tw_c_key
      config.consumer_secret     = Figaro.env.tw_c_secret
    end

You can set different keys for development, test, and production. Here’s an example config/application.yml:

    development:
      stripe_api_key: ‘12345654321_dev_key’

    test:
      stripe_api_key: ‘fake_key’

    production:
      stripe_api_key: ‘the_real_key’

Use [application.yml](/protocol/rails/application.yml) as the base for your application.yml.

Don't push keys to staging or production. We (hugo + ken) will be responsible for those keys. But for development and test, you should create your own keys.

## Getting API Keys
For Facebook, go to the [Facebook Dev Center](https://developers.facebook.com/apps) and click '+ Add a New App'.

For Twitter, go to the [twitter app management page](https://apps.twitter.com/) and click 'Create New App'.