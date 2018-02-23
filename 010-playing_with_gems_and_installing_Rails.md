# Playing with gems and installing Rails

## Upgrade Ruby gem manager
```bash
gem update --system
``` 

## List available gemsets
```bash
rvm gemset list
```

## List outdated gems
```bash
gem outdated
```

## Disable documentation for Gems [OPTIONAL]
```bash
echo "gem: --no-document" >> ~/.gemrc
```

## Update gems
```bash
gem update
```

## Installing bundler
Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed.

Bundler is an exit from dependency hell, and ensures that the gems you need are present in development, staging, and production.

```bash
gem install bundler
```

## Installing Nokogiri
Nokogiri is a gem that is a dependency for many other gems. Nokogiri is a gem that requires compilation for your specific operating system. However, compilation takes time. 

To save time, install the Nokogiri gem in the RVM global gemset:
```
rvm @global do gem install nokogiri
```

## Install Rails
```bash
gem install rails --version 5.1.5
rails --version
```
