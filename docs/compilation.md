---
layout: default
title: Compilation
permalink: /compilation/
---

# Compilation

## Ubuntu 20.04 LTS

This process is also available as an installation script; which can be found 
[here](https://gist.github.com/obskein/fbfd8d87660297e8be7edf01921ab7a8)

### Update system

It is strongly recommended to update system dependencies before beginning the 
XGT compilation process.

```sh
sudo apt-get clean && sudo apt-get update
```

### Install dependencies

```sh
sudo apt-get install -y \
     autoconf \
     automake \
     cmake \
     g++ \
     git \
     libbz2-dev \
     libsnappy-dev \
     libssl-dev \
     libtool \
     make \
     pkg-config \
     python3 \
     python3-jinja2 \
     scrypt \
     dnsutils \
     ccache \
     libboost-all-dev \
     build-essential \
     curl \
     zlib1g-dev \
     libreadline-dev \
     libyaml-dev \
     libxml2-dev \
     libxslt-dev \
     ninja-build
```

### Setup Ruby & ruby dependencies in a sane way

Some convenience functions are available using the built in `rake` commands.
In order to use these, it is strongly recommended to set up a sane ruby 
environment.

```sh
if [ ! -d $HOME/.rbenv ]; then
  git clone https://github.com/sstephenson/rbenv.git $HOME/.rbenv
  git clone https://github.com/sstephenson/ruby-build.git $HOME/.rbenv/plugins/ruby-build
fi

# $HOME/.rbenv/plugins/ruby-build/install.sh
export PATH="$HOME/.rbenv/bin:$PATH"

# echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh # or /etc/profile

if ! grep -q 'export PATH="$HOME/.rbenv/bin:$PATH"' $HOME/.bashrc; then
  echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> $HOME/.bashrc
  echo 'eval "$(rbenv init -)"' >> $HOME/.bashrc
fi

# source $HOME/.bashrc

export PATH="$HOME/.rbenv/bin:$PATH" # TODO Extraneous?
eval "$(rbenv init -)"

rbenv install 2.7.2 --skip-existing
rbenv global 2.7.2
rbenv rehash

gem update --no-document --system
gem install --no-document bundler rake xgt-ruby
rbenv rehash
```

### Download and compile

Checkout a fresh copy of XGT, in readiness to compile.
```sh
git clone https://github.com/xgt-network/xgt.git $HOME/xgt
cd $HOME/xgt
git checkout master
cd $HOME/xgt

# Clean & compile
rake clean
rake configure
THREAD_COUNT=4 rake make
```

It is possible to pull the latest version of the code, a
```sh
cd $HOME/xgt
git pull
git checkout master
cd $HOME/xgt

# Clean & compile
rake clean
rake configure
THREAD_COUNT=4 rake make
```

### Configure firewall 

The firewall should be configured to open TCP ports 8751 and 2001.
```
sudo ufw allow 8751,2001/tcp
```

### Configure & Execute 
Available configuration options: 

#### Mining options
```sh
# Set ALL of theset to be a recovery private key:
XGT_WIF=
XGT_RECOVERY_PRIVATE_KEY=
XGT_WITNESS_PRIVATE_KEY=
```

#### General options
Connection and synchronization options:
```sh
# Specify a seed host to synchronize against
XGT_SEED_HOST=
# Delete local chain data, forcing a resync against a seed node
FLUSH_TESTNET=TRUE
# Disable mining, thereby creating a seed node
MINING_DISABLED=TRUE
```

Then xgt can be run using `rake run`.

## MacOS
### Setup XCode
```sh
sudo xcodebuild -license accept
```
### Update homebrew
```
brew doctor
brew update
```
### Setup dependencies
```sh
brew install \
    autoconf \
    automake \
    cmake \
    git \
    boost160 \
    libtool \
    openssl \
    snappy \
    zlib \
    bzip2 \
    ruby-dev \
    ccache \
    python3 \
    icu4c \
    ninja
pip3 install --user jinja2
```

### Download and compile

Checkout a fresh copy of XGT, in readiness to compile.
```sh
git clone https://github.com/xgt-network/xgt.git $HOME/xgt
cd $HOME/xgt
git checkout master
cd $HOME/xgt

# Clean & compile
rake clean configure make
```

### Configure & Execute 
Available configuration options: 

#### Mining options
```sh
# Set ALL of theset to be a recovery private key:
XGT_WIF=
XGT_RECOVERY_PRIVATE_KEY=
XGT_WITNESS_PRIVATE_KEY=
```

#### General options
Connection and synchronization options:
```sh
# Specify a seed host to synchronize against
XGT_SEED_HOST=
# Delete local chain data, forcing a resync against a seed node
FLUSH_TESTNET=TRUE
# Disable mining, thereby creating a seed node
MINING_DISABLED=TRUE
```

Then xgt can be run using `rake run`.
