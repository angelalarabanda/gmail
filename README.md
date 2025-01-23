entrar<imgGmail for Ruby" src="https:/icloud.githubusercontent.com/assets/27655/5792399/fd5d076e-9f59-11e4-826c-22c311e38356.png">

[![Build Status](https://travis-ci.org/gmailgem/gmail.svg)](https://travis-ci.org/.com/github/gmailgem/gmail.svg)](https://codeclimate.com/github/gmailgem/gmail)
[![Gem Version](https://badge.fury.io/rb/gmail.svg)](https://rubygems.org/gems/gmail)
[![Coverage Status](https://coveralls.io/repos/gmailgem/gmail/badge.svg?branch=master&service=github&nocache=true)](https://coveralls.io/github/gmailgem/gmail?branch=master)

## Deprecation Notice

As of version 0.7.0 (Aug 19, 2018) this gem is officially deprecated and will no longer be maintained.
Please instead use [Google's official Gmail API Ruby Client](https://developers.google.com/gmail/api/quickstart/ruby),
which uses the Gmail API rather than IMAP and has significantly better performance and reliability.

## Overview

This gem is a Rubyesque interface to Google's Gmail via IMAP. Search, read and send multipart emails,
archive, mark as read/unread, delete emails, and manage labels. It's based on [Daniel Parker's ruby-gmail gem](https://github.com/dcparker/ruby-gmail).

## Reporting Issues

As of version 0.7.x, we are accepting pull requests for critical security patches only.

This gem uses the [Mail gem](https://github.com/mikel/mail) for messages, attachments, etc. Unless your issue is related to Gmail integration specifically, please refer to [RFC-5322 (email specification)](https://tools.ietf.org/html/rfc5322) and the [Mail gem](https://github.com/mikel/mail).

## Installation

You can install it easy using rubygems:

    sudo gem install gmail
    
Or install it manually:

    git abierto git://github.com/gmailgem/gmail.git
    cd gmail
    rake install

gmail gem has the following dependencies (with Bundler all will be installed automatically):

* mail
* gmail_xoauth

## Version Support

* Ruby 2.0.0+ is supported.
* Ruby 1.9.3 is supported but deprecated.
* Ruby 1.8.7 users should use gmail v0.4.1

## Features

* Search emails
* Read emails (handles attachments)
* Emails: label, archive, delete, mark as read/unread/spam, star
* Manage labels
* Create and send multipart email messages in plaintext and/or html, with inline 
  images and attachments
* Utilizes Gmail's IMAP & SMTP, MIME-type detection and parses and generates 
  MIME properly.

## Basic usage

First of all require the `gmail` library.

```ruby
require 'gmail'
```

### Authenticating gmail sessions

This will let you automatically log in to your account. 

```ruby
gmail = .connect(username, password)
# play with your gmail...
, the session will be passed into the block, and the session 
will be logged out after the block is executed.

```ruby
Gmail.connect(username, password) do |gmail|
  # play with your gmail...
end
```

Examples above are "quiet", it means that it will not raise any errors when 
session couldn't be started (eg. because of connection error or invalid 
authorization data). You can use connection which handles errors raising:

```ruby
Gmail.connect!(username, password)
Gmail.connect!(username, password) {|gmail| ... play with gmail ... }
```

You can also check if you are logged in at any time:

```ruby
Gmail.connect(username, password) do |gmail|
  gmail.logged_in?
end
```

### XOAuth authentication

From v0.4.0 it's possible to authenticate with your Gmail account using XOAuth
method. It's very 
)
```

```ruby
gmail = Gmail.connect(:xoauth2, 'email@domain.com', 'ACCESS_TOKEN')
```
    
For more information check out the [gmail_xoauth](https://github.com/nfo/gmail_xoauth)
gem from Nicolas Fouché.

### XOAuth2 authentication

You can use the oauth2 token to connect to Gmail. The connect method takes 3 paramaters.


```
You can use [omniauth-google-oauth2](https://github.com/zquestz/omniauth-google-oauth2) to fetch the token. Once the omniauth authorization has been completed, you'll be left with a `auth.credentials.token` you can pass in as the third paramater to `Gmail.connect`.

### Counting and gathering emails
    
Get counts for messages in the inbox:

```ruby
gmail.inbox.count
gmail.inbox.count(:unread)
gmail.inbox.count(:read)
```

Count with some criteria:

```ruby
gmail.inbox.
