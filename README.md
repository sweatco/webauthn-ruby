# WebAuthn

Easily implement WebAuthn in your ruby web server

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'webauthn'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install webauthn

## Usage

### Registration

#### Initiation phase

```ruby
credential_creation_options = WebAuthn.credential_creation_options

# Store the newly generated challenge somewhere so you can have it
# for the validation phase.
#
# You can read it from the resulting options:
credential_creation_options[:challenge]

# Send `credential_creation_options` to the browser, so that they can be used
# to call `navigator.credentials.create({ "publicKey": credentialCreationOptions })`
```

#### Validation phase

```ruby
attestation_object = "..." # As came from the browser
client_data_json = "..." # As came from the browser

attestation_response = WebAuthn::AuthenticatorAttestationResponse.new(
  attestation_object: attestation_object,
  client_data_json: client_data_json
)

if attestation_response.valid?(original_challenge)
  # Register the new user
else
  # Handle error
end
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/webauthn.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
