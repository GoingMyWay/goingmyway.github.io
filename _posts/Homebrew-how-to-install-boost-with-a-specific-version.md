---
title: 'Homebrew: how to install boost with a specific version'
date: 2018-02-06 09:41:52
tags: Homebrew
categories: Homebrew
---

Since boost 1.58 and boost-python 1.58 are not available in the newest homebrew, one way to install them using homebrew is to downgrade the formula--editing the formula file so that you can install boost 1.58 and boost-python via homebrew.  See this page: https://stackoverflow.com/questions/3939651/how-to-modify-a-homebrew-formula

The newest boost formula file is here: https://github.com/Homebrew/homebrew-core/blob/master/Formula/boost.rb, and you can also find boost-python formula file.

So, how can we edit the formula of boost and boost-python? Just use `edit` option in brew command,

**Note that** all the sha256 values and the corresponding URLs should be right. And if you tried to install boost from source, you should remove boost first, see this page: https://askubuntu.com/questions/325504/ubuntu-12-04-uninstall-boost-installed-from-source

**Edit boost formula**

```shell
brew edit boost       
Editing /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Formula/boost.rb
Warning: Using vim because no editor was set in the environment.
This may change in the future, so we recommend setting EDITOR,
or HOMEBREW_EDITOR to your preferred text editor.
```
change the code

```
class Boost < Formula
  desc "Collection of portable C++ source libraries"
  homepage "https://www.boost.org/"
  #url "https://dl.bintray.com/boostorg/release/1.65.1/source/boost_1_65_1.tar.bz2"
  #sha256 "9807a5d16566c57fd74fb522764e0b134a8bbe6b6e8967b83afefd30dcd3be81"
  url "https://downloads.sourceforge.net/project/boost/boost/1.58.0/boost_1_58_0.tar.bz2"
  sha256 "fdfc204fc33ec79c99b9a74944c3e54bd78be4f7f15e260c0e2700a36dc7d3e5"
  head "https://github.com/boostorg/boost.git"
```

**also, edit boost-python formula**

```shell
brew edit boost-python
```

```
class BoostPython < Formula
  desc "C++ library for C++/Python interoperability"
  homepage "https://www.boost.org/"
  #url "https://dl.bintray.com/boostorg/release/1.65.1/source/boost_1_65_1.tar.bz2"
  #sha256 "9807a5d16566c57fd74fb522764e0b134a8bbe6b6e8967b83afefd30dcd3be81"
  url "https://downloads.sourceforge.net/project/boost/boost/1.58.0/boost_1_58_0.tar.bz2"
  sha256 "fdfc204fc33ec79c99b9a74944c3e54bd78be4f7f15e260c0e2700a36dc7d3e5"
  head "https://github.com/boostorg/boost.git"
```



And then install boost and boost-python without specifying version

```shell
brew install boost 
brew install boost-python # python2
# or python 3
brew install boost-python3 # python 3
```

Just wait for about 30 minutes to install these libraries.

