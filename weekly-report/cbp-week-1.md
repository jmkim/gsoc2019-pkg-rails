## Community Bonding Week 1
  * May 6 ~ May 12
  * #rubygsoc weekly meeting: https://bundler.slack.com/archives/C03TNNH59/p1557756129005800

### Learned
  * Extract symbols from shared library using `dpkg-gensymbols`
      + by upgrading libgit2
      + https://wiki.debian.org/UsingSymbolsFiles
  * How to manage C extensions in Ruby gem and Debian Ruby package
      + by upgrading libgit2 and ruby-rugged
  * How the `gem2deb` (and `dh_ruby`) runs the test during Debian package build time
      + https://wiki.debian.org/Teams/Ruby/Packaging/Tests

### Worked
  * (Not yet finished) Estimate all the libraries which Rails depending on
  * Join and work with Debian packaging community:
      + GitLab (`#debian-gitlab:poddery.com` on Matrix)
          - was invited by Utkarsh Gupta, who is a Debian Maintainer.
  * Do the Ruby libraries upgrade transition:
      + libgit2
          - Library written in C, which is dependency of Ruby library `ruby-rugged`.
          - Library transition: upgrade from 0.27.7 to 0.28.1 with exporting symbols.
          - https://salsa.debian.org/debian/libgit2/commits/master
      + ruby-rugged
          - Library transition: upgrade from 0.27.4 to 0.28.1.
          - https://salsa.debian.org/ruby-team/ruby-rugged/commits/master
      + ruby-globalid
          - Patch the test failure. From Rails 6.0.0, `secret_token` will be removed. This patch makes use new `secret_key_base` instead of deprecated `secret_token`.
          - https://salsa.debian.org/ruby-team/ruby-globalid/commits/buster

### Patches
  * ruby-globalid
      + Fix [#925178](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=925178)
      + Patch the test failure. From Rails 6.0.0, `secret_token` will be removed. This patch makes use new `secret_key_base` instead of deprecated `secret_token`.
          - https://salsa.debian.org/ruby-team/ruby-globalid/blob/951ee82dc15cf276fd7587bcd47116707671d586/debian/patches/fix_test_railtie.patch

### Uploaded packages
  * [experimental] libgit2/0.28.1+dfsg.1-0.1
  * [experimental] ruby-rugged/0.28.1+ds-1
  * [unstable] ruby-globalid/0.4.2+REALLY.0.3.6-1 (by Utkarsh Gupta)

