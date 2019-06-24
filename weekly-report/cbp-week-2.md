## Community Bonding Week 2
  * May 13 ~ May 19
  * #rubygsoc weekly meeting: https://bundler.slack.com/archives/C03TNNH59/p1558360138078100

### Learned
  * Unit test in Ruby: minitest and RSpec
      + by doing upgrade transition in ruby-gravtastic: from RSpec 2 to RSpec 3
  * `gem2deb` rake hooker for minitest and RSpec
      + https://salsa.debian.org/ruby-team/gem2deb/tree/master/lib/gem2deb/rake
  * How to salvage the package
      + by ITS: libgit2 [#928971](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=928971)
          - was asked by Praveen Arimbrathodiyil
      + https://www.debian.org/doc/manuals/developers-reference/ch05.en.html#package-salvaging
      + https://wiki.debian.org/PackageSalvaging

### Worked
  * Announce my project to Debian Ruby team mailing list
      + https://lists.debian.org/debian-ruby/2019/05/msg00017.html
  * Estimate all the libraries which Rails depending on
      + https://wiki.debian.org/Teams/Ruby/Rails6/DependenciesTransition
  * Create a task tracker on Debian Wiki
      + https://wiki.debian.org/Teams/Ruby/Rails6
  * Join and work with Debian packaging community:
      + Diaspora (`#debian-diaspora` on OFTC)
          - was invited by Praveen Arimbrathodiyil, who is a Debian Developer.
  * Do the Ruby libraries upgrade transition:
      + ruby-httparty
          - Refresh patches for new upstream version.
          - https://salsa.debian.org/ruby-team/ruby-httparty/commits/master
      + ruby-gravtastic
          - Patch the test failure.
          - RSpec 2 and RR upgrade transition.
          - https://salsa.debian.org/Manas-kashyap-guest/ruby-gravtastic/commits/master
      + ruby-zeitwerk
          - New dependency for Rails 6.
          - https://salsa.debian.org/jmkim-guest/ruby-zeitwerk/commits/master

### Reported to upstream
  * [PR:opened] Replace RSpec syntax "should" with "expect"
      + (as the upstream repository was read-only, the patch was published by mail with diff)
      + https://github.com/jmkim/gravtastic/commit/dd431bf2487544183dc64b910edc433ca7c4ed4f

### Patches
  * ruby-gravtastic
      + Patch for fixing the RSpec deprecated syntax
          - https://salsa.debian.org/Manas-kashyap-guest/ruby-gravtastic/commit/ebe6a901a4e357bb3fe49e0cfb3cb587e1692d69
      + Patch for applying upstream latest code
          - https://salsa.debian.org/Manas-kashyap-guest/ruby-gravtastic/commit/bb8bf7a71b9c845177fbf22a1560364a9c8b435d
      + Patch for RR upgrade transition
          - https://salsa.debian.org/Manas-kashyap-guest/ruby-gravtastic/commit/ac871a09229f48bc123eb5ee65d76806669908a7

### Uploaded packages
  * [experimental] ruby-httparty/0.16.4-1
