ruby_pkg
========

[![Build Status](https://travis-ci.org/reaktor/chef-ruby_pkg.png?branch=master)](https://travis-ci.org/reaktor/chef-ruby_pkg)

Description
-----------

A Chef cookbook and [Vagrant](http://www.vagrantup.com/) setup for building and packaging a specified Ruby version.

Requirements
------------

Requires [ruby_build](http://community.opscode.com/cookbooks/ruby_build) and [fpm-tng](http://community.opscode.com/cookbooks/fpm-tng) community cookbooks.

Should work on all Debian based Linux distributions. Support for some other platforms (that ruby_build and [fpm](https://github.com/jordansissel/fpm) support) is planned. Please open an [issue](https://github.com/reaktor/chef-ruby_pkg/issues) or pull request if interested.

Usage
-----

This cookbook is intended to be used with the included Vagrant setup (although you *can* use the cookbook directly by adding it to run_list or by including it in your own cookbooks).

To use Vagrant you need to clone the repository from Github:

        $ git clone https://github.com/reaktor/chef-ruby_pkg.git
        $ cd chef-ruby_pkg

### Install Vagrant environment

1. Install [Vagrant](http://downloads.vagrantup.com/) v1.2 or later
2. Install needed Vagrant plugins:

        $ vagrant plugin install vagrant-berkshelf
        $ vagrant plugin install vagrant-omnibus

3. Add your favorite Vagrant box, for example:

        $ vagrant box add "ubuntu-12.04" "http://files.vagrantup.com/precise64.box"

### Building with Vagrant

Spin up the box to build and package a specified Ruby version:

    $ VERSION="1.9.3-p429" BOX="ubuntu-12.04" vagrant up

The package will be created to _pkg_ directory.

### Environment variables for Vagrant

  * `$BOX` - The Vagrant box name. Defaults to "squeeze-6.0".
  * `$DEBUG` - If set, enable debug logging of the Chef run.
  * `$VERSION` - The Ruby version to package. Passed to ruby_build. Defaults
    to "1.9.3-p429"
  * `$ITERATION` - The package iteration version number. Passed to fpm.
    Defaults to 1.
  * `$MAINTAINER` - The (optional) package maintainer. Passed to fpm.

License and Author
------------------

Author:: Teemu Matilainen <<teemu.matilainen@reaktor.fi>>

Copyright © 2013, [Reaktor Innovations Oy](http://reaktor.fi/en)

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE).
