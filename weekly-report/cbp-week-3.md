## Community Bonding Week 3
  * May 20 ~ May 26
  * #rubygsoc weekly meeting: https://bundler.slack.com/archives/C03TNNH59/p1558966645032500

### Learned
  * About Debian New Member Process
      + by applying Debian Maintainer
  * How to import missing tests
      + by importing ruby-thor missing tests

### Worked
  * Apply to become a Debian Maintainer
      + https://nm.debian.org/process/617
      + was asked and thankfully advocated by Praveen Arimbrathodiyil
  * Write a script for importing the tests into debian/ directory
      + https://gist.github.com/jmkim/35a6f05d788806b2f53df414bdf7c618
      + But not used; there was a simple solution: replace gemwatch.d.n to upstream source repo
  * Import Rails 6.0.0.rc1 to Rails Debian package repository
      + https://salsa.debian.org/jmkim-guest/rails/commits/master
  * Package the Rails 6 dependencies
      + ruby-webdrivers
          - New package
          - https://salsa.debian.org/jmkim-guest/ruby-webdrivers
          - Stopped and skipped; this could be replaceable with ruby-chromedriver-helper; which was deprecated
      + ruby-thor
          - Upgrade from 0.19.4 to 0.20.3
          - https://salsa.debian.org/ruby-team/ruby-thor/commits/master
      + ruby-foreman

### Patches
  * ruby-thor
      + Exclude test which uses git
          - https://salsa.debian.org/ruby-team/ruby-thor/commit/6e7d38487e4d3c5419a9ddb390d9a13406e551a1
      + Import the missing tests
          - https://salsa.debian.org/ruby-team/ruby-thor/commit/daab85d994a096767b899c4e7f812ada5a583fa6
          - https://salsa.debian.org/ruby-team/ruby-thor/commit/df3d0c0c580ef68176fb8f9ef66ba92232221d0e
