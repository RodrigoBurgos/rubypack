# Rubypack

This gem provides some utilities to build a package of your application with aims to provide a runnable standalone application that can be shared or deployed in production systems.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'rubypack'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rubypack

## Usage

To build a package of your application, you need to define a new file named `.rubypack` on the root directory of your application.

The content of the .rubypack file:
```ruby
name 'TestApp'
version '3.1'

exclude '*.log'
include 'js/node_modules/**/**'
```

Then run the following command to build your package:

```bash
$ rubypack build

Reading .rubypack file...
 Name: TestApp
 Version: 3.1
  [ OK ]
Downloading gems...
  [ OK ]
Generating list of files...
 Action: exclude, Filter: *.log
 Action: include, Filter: js/node_modules/**/**
 Files count: 33
  [ OK ]
Creating copy of files...
  [ OK ]
Creating package...
 File created:  /repo/my_application/TestApp-3.1.tgz.rpack
  [ OK ]
```

The previous command will generate a file with extension '.tgz.rpack'. It will automatically include all the required gems for all the platforms in the package.

The application can be deployed using the following command:

```bash
$ rubypack deploy --filename TestApp-3.1.tgz.rpack --directory /production/app/
Unpacking file...
 Directory created:  /production/app/
  [ OK ]
Installing gems...
  [ OK ]
```

The previous command will install all the gems required by your application in local mode, without using network or rubygems, and using the `Gemfile.lock` to install the proper gems inside the `vendor` folder.

To view more details about what is happening, you can use the `--verbose` switch. Also with `--help` you can see the different commands available.

### Available commands

```bash
$ rubypack --help
RubyPack 0.1.0 (c) 2017 Jorge del Rio
A ruby package generation and execution manager.

Commands:
  build    Create a new package.
  deploy   Install the application package and all the gems.
  list     List the files to be included in the package.

Options:
  -h, --help    Show this message
```

### Build command

```bash
$ rubypack build --help
build - Builds a package of your application.

Options:
  -c, --config=<s>              The config file to use (default: .rubypack)
  -o, --output-directory=<s>    The directory where the final package is going to be created. (Default: .)
  -m, --compressor=<s>          The compressor utility to use. Possible values: tgz, zip. (Default: tgz)
  -n, --no-overwrite            Do not overwrite the output file if it already exists.
  -v, --verbose                 Verbose output for debugging.
  -q, --quiet                   Do not output anything.
  -h, --help                    Show this message
```

### Deploy command

```bash
$ rubypack deploy --help
deploy - Install the application package and all the gems.

Options:
  -f, --filename=<s>      The file deploy
  -d, --directory=<s>     The directory where the final package is going to be deployed.
  -v, --verbose           Verbose output for debugging.
  -c, --compressor=<s>    The compressor utility to use. Possible values: tgz, zip.
  -h, --help              Show this message
```

### List command

```
$ rubypack list --help
list - List the files to be included in the package.

Options:
  -c, --config=<s>    The config file to use (default: .rubypack)
  -v, --verbose       Verbose output for debugging.
  -h, --help          Show this message
```


## Development

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/newint33h/rubypack.git. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

