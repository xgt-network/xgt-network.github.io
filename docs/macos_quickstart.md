## MacOS Build Instructions

1. `git clone https://github.com/xgt-network/xgt.git`

2. `cd ../xgt`

3. `git checkout master`

4. `sudo xcodebuild -license accept`
	- See note N1 below

5. `brew doctor`

6. `brew update`

7. 
```
brew install
    autoconf \
    automake \
    cmake \
    git \
    boost \
    libtool \
    libmpc \
    openssl \
    snappy \
    zlib \
    bzip2 \
    ruby \
    ccache \
    python3

brew install --cask gcc-arm-embedded
```

8. `echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile`

9. `source ~/.bash_profile`

10. `pip3 install --user jinja2`

11. Set the library paths. If you are using the standard `homebrew` install, then the prefix for all of these library paths will be `/usr/local/Cellar`. If you have a different homebrew install, find your prefix by running `brew —prefix`. At the time of this writing (2021-07-03), run the following commands one at a time to set the library paths:
```

export BOOST_ROOT=/usr/local/Cellar/boost/1.76.0/*

export OPENSSL_ROOT_DIR=/usr/local/Cellar/openssl@1.1/1.1.1k/*

export SNAPPY_ROOT_DIR=/usr/local/Cellar/snappy/1.1.9/*

export ZLIB_ROOT_DIR=/usr/local/Cellar/zlib/1.2.11/*

export BZIP2_ROOT_DIR=/usr/local/Cellar/bzip2/1.0.8/*

 
```

Before moving forward, run `brew list **library**` to check for the version number on your specific machine. If the version number that appears is different than what is listed above, replace the version number with your current version number.

12. `brew install icu4c`

13. export LIBRARY_PATH=${LIBRARY_PATH}:/usr/local/opt/icu4c/lib

14. `cd /usr/local/include`

15. `ln -s ../opt/openssl/include/openssl .`

16. Navigate back to the original `xgt` folder you created in step 1 and run: `rake configure`

17. `rake make`

18. `MINING_DISABLED=FALSE XGT_WALLET=XGT_WALLET_NAME XGT_RECOVERY_PRIVATE_KEY=WALLET_PRIVATE_KEY XGT_WITNESS_PRIVATE_KEY=WALLET_PRIVATE_KEY XGT_SEED_HOST=98.33.76.100:2001,xgt.rag.pub:2001,xgt2.rag.pub:2001,68.129.31.2:2001,116.202.114.157:2001,195.201.167.19:2001,95.216.69.92:2001,95.216.71.199:2001 rake run`


* N1: Apple only allows current install of Xcode 12.5. You can check whether or not your machine supports the most recent release of Xcode [here](https://developer.apple.com/support/xcode/). If your machine does not support Xcode 12.5, you will need to install the Command Line Tools for the most up-to-date version of Xcode that your machine supports. You can search for the Command Line Tools installer [here](https://developer.apple.com/download/all/?q=xcode).
