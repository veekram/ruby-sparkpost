<a href="https://www.sparkpost.com"><img src="https://www.sparkpost.com/sites/default/files/attachments/SparkPost_Logo_2-Color_Gray-Orange_RGB.svg" width="200px"/></a>

[Sign up](https://app.sparkpost.com/join?plan=free-0817?src=Social%20Media&sfdcid=70160000000pqBb&pc=GitHubSignUp&utm_source=github&utm_medium=social-media&utm_campaign=github&utm_content=sign-up) for a SparkPost account and visit our [Developer Hub](https://developers.sparkpost.com) for even more content.

# SparkPost Ruby API Client

[![Travis CI](https://travis-ci.org/SparkPost/ruby-sparkpost.svg?branch=master)](https://travis-ci.org/SparkPost/ruby-sparkpost) [![Coverage Status](https://coveralls.io/repos/SparkPost/ruby-sparkpost/badge.svg?branch=master&service=github)](https://coveralls.io/github/SparkPost/ruby-sparkpost?branch=master) [![Slack Status](http://slack.sparkpost.com/badge.svg)](http://slack.sparkpost.com)

**Due to incredible support and contributions from the community, we will be discontinuing support of the official SparkPost ruby client library as of May 17, 2016. If you’re looking for an alternative, take a look at some of these [repositories](https://github.com/search?l=Ruby&q=sparkpost&type=Repositories&utf8=%E2%9C%93).**

## Installation

Add this line to your application's Gemfile:

    gem 'sparkpost'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install sparkpost

**Important: Implementations may change frequently until we reach v1.0.0**

## Usage

**Send an email**

```ruby
require 'sparkpost'

sp = SparkPost::Client.new() # api key was set in ENV through ENV['SPARKPOST_API_KEY']
response = sp.transmission.send_message('RECIPIENT_EMAIL', 'SENDER_EMAIL', 'test email', '<h1>HTML message</h1>')
puts response

# {"total_rejected_recipients"=>0, "total_accepted_recipients"=>1, "id"=>"123456789123456789"}
```

**Send email with substitution data**

```ruby
require 'sparkpost'

values = { substitution_data: { name: 'Sparky'}}
sp = SparkPost::Client.new() # pass api key or get api key from ENV
response = sp.transmission.send_message('RECIPIENT_EMAIL', 'SENDER_EMAIL', 'testemail', '<h1>HTML message from {{name}}</h1>', values)
puts response

# {"total_rejected_recipients"=>0, "total_accepted_recipients"=>1, "id"=>"123456789123456789"}
```

**Send email with attachment**

*You need to base64 encode of your attachment contents.*

```ruby
require 'sparkpost'

# assuming there is a file named attachment.txt in the same directory
attachment = Base64.encode64(File.open(File.expand_path('../attachment.txt', __FILE__), 'r') { |f| f.read })

# prepare attachment data to pass to send_message method
values = {
    attachments: [{
        name: 'attachment.txt',
        type: 'text/plain',
        data: attachment
    }]
}

sp = SparkPost::Client.new() # pass api key or get api key from ENV
sp.transmission.send_message('RECIPIENT_EMAIL', 'SENDER_EMAIL', 'testemail', '<h1>Email with an attachment</h1>', values)
```

**Search the suppression list**

```ruby
require 'sparkpost'

sp = SparkPost::Client.new() # pass api key or get api key from ENV
sp.suppression_list.search
```


See: [examples](examples)
