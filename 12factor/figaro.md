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

When deploying, you can set these keys and values directly with:

  figaro heroku:set -e production

This will grab the production group from your config/application.yml and push those values to the heroku env.