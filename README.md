[![XGT Logo](https://xgt-network.github.io/assets/images/xgt-logo.png)](https://xgt-network.github.io)

# xgt-network.github.io

XGT is a distributed data storage system, with simple API endpoints 
for engineers to develop distributed, decentralized, and robust 
applications on.

Additionally, xgt-network.github.io contains up to date information regarding 
installation, configuration, and tooling surrounding the XGT core 
implementation.

## Running jekyll locally

Dependencies are managed with Bundler. To set up a sane ruby environmentm, it is 
recommended to use rbenv, and to install associated rubygems with bundler.

1. Install ruby.
2. Install the jekyll and bundler gems.
 `gem install jekyll bundler`
3. Change into your new directory.
 `cd docs`
4 Build the site and make it available on a local server.
 `bundle exec jekyll serve`
5. Browse to http://localhost:4000

## Requirements

* Ruby version `2.4.0` or higher, including all development headers (check your Ruby version using `ruby -v`)
* RubyGems (check your Gems version using `gem -v`)
* GCC and Make (check versions using `gcc -v`,`g++ -v`, and `make -v`)

## License

MIT License

Copyright (c) 2021 Robert Day & Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
