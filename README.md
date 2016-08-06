# post-massage-rails

post-massage! For Rails!

This gem provides:

  * post-massage

  See [VERSIONS.md](VERSIONS.md) to see which versions of post-massage-rails bundle which versions of post-massage.

## Versions

```
patch version bump = updates to post-massage-rails, and patch-level updates to post-massage
minor version bump = minor-level updates to post-massage
major version bump = major-level updates to post-massage and updates to rails which may be backwards-incompatible
```

## Installation

Gemfile

```ruby
gem "post-massage-rails"
```

And run `bundle install`. The rest of the installation depends on whether the asset pipeline is being used.

### Rails 3.1 or greater (with asset pipeline *enabled*)

The post-massage files will be added to the asset pipeline and available for you to use. add these lines to `app/assets/javascripts/application.js`:

```js
//= require post-massage
```

### Rails 3.0 (or greater with asset pipeline *disabled*)

This gem adds a single generator: `post-massage:install`. Running the generator will copy PostMassage to the `public/javascripts` directory.

This gem will also hook into the Rails configuration process, adding PostMassage to the javascript files included by the `javascript_include_tag(:defaults)` call. While this gem contains the minified and un-minified versions of PostMassage, only the minified versions will be included in the `:defaults` when Rails is run in `production` or `test` mode  (un-minified versions will be included when Rails is run in `development` mode).

To invoke the generator, run:

```sh
rails generate post-massage:install
```

You're done!

## Contributing

Feel free to open an issue ticket if you find something that could be improved. 

## Acknowledgements

This gem's structure and technique for wrapping a JS library into a rails friendly package is based entirely on jquery-rails. Many thanks are due to all of [the jquery-rails contributors](https://github.com/rails/jquery-rails/graphs/contributors).

Copyright Tyler Kasten, released under the MIT License.
