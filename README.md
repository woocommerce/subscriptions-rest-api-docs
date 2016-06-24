# WooCommerce Subscriptions REST API Docs #

Repository for the documentation of the WooCommerce Subscriptions REST API.

This project is based on [WooCommerce REST API Docs](http://woothemes.github.io/woocommerce-rest-api-docs/) and [Slate](https://github.com/tripit/slate).

# Testing and deploy changes #

The simplest option to testing changes on this repository would be to fork your own copy and then run the deploy script to get it up on your own GH page (i.e. https://your_github_username.github.io/subscriptions-rest-api-docs)

Assuming you're running the most up-to-date OSX version.

1. Install rvm: https://rvm.io/rvm/install - using the osx defaults ruby version will not work, we need to use a specific version of ruby for deploying to work, hence rvm is used to manage ruby versions and gems
2. Install ruby version 2.2.3: `rvm install ruby-2.2.3` - after many attempts to get this working, 2.2.3 was the only version that has shown success
3. Use that version of ruby: `rvm use ruby-2.2.3`
4. `cd` into your forked repository
5. Install bundle: `gem install bundler`
6. run `bundle install` - shouldn't see any errors when doing this
7. run `./deploy.sh`
8. Check the changes at https://your_github_username.github.io/subscriptions-rest-api-docs
