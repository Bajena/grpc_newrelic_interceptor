# GrpcNewrelicInterceptor
An interceptor for using New Relic with gRPC.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'grpc_newrelic_interceptor'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install grpc_newrelic_interceptor

## Usage

### Server

```ruby
require 'grpc'
require 'grpc_newrelic_interceptor'

NewRelic::Agent.manual_start  # start newrelic agent

server = GRPC::RpcServer.new(
  interceptors: [
    GrpcNewrelicInterceptor::ServerInterceptor.new,
  ]
)
server.handle(MyHandler.new)
server.run_till_terminated_or_interrupted(['SIGINT'])
```

### Client

```ruby
require 'grpc'
require 'grpc_newrelic_interceptor'

url = "dns:test-service:80"
stub = TestService::Stub.new(url, :this_channel_is_insecure, interceptors: [
  GrpcNewrelicInterceptor::ClientInterceptor.new,
])
stub.hello_rpc
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `bundle exec rspec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/wantedly/grpc_newrelic_interceptor.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
