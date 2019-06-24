## Week 2
  * June 3 ~ June 9
  * #rubygsoc weekly meeting: https://bundler.slack.com/archives/C03TNNH59/p1560175030001400

### Learned
  * #include vs #prepend in Ruby
      + https://harfangk.github.io/2016/12/11/basics-of-ruby-method-dispatch-system-part1-ko.html
      + #include: append module after super class
      + #prepend: append module before super class
  * Multi binary (and multi language) layout of Debian package
      + https://salsa.debian.org/debian/grpc
      + was suggested by mentor Sruthi
  * Multi binary layout of Debian Ruby package (with dh_ruby)
      + https://manpages.debian.org/unstable/gem2deb/dh_ruby.1.en.html

### Worked
  * Package the Rails 6 dependencies
      + ruby-redis
          - Upgrade from 3.3.5 to 4.1.2
          - https://salsa.debian.org/ruby-team/ruby-redis/commits/master
      + ruby-image-processing
          - New package
          - https://salsa.debian.org/ruby-team/ruby-image-processing
      + ruby-vips
          - New package
          - Dependency of ruby-image-processing
          - https://salsa.debian.org/ruby-team/ruby-vips
      + ruby-minispec-metadata
          - New package
          - Dependency of ruby-image-processing
          - https://salsa.debian.org/ruby-team/ruby-minispec-metadata
      + ruby-mini-magick
          - Upgrade from 4.9.2 to 4.9.3; because of ruby-image-processing error
          - Dependency of ruby-image-processing
          - https://salsa.debian.org/ruby-team/ruby-mini-magick/commits/master

### Patches
  * ruby-redis
      + Use absolute load path in tests
          - https://salsa.debian.org/ruby-team/ruby-redis/commit/1001927ec976f328a33c15b8a45329bc265a02ed
      + Import the missing tests
          - https://salsa.debian.org/ruby-team/ruby-redis/commit/3889424b14d8088e5804649f2fa8603adce41cca
          - https://salsa.debian.org/ruby-team/ruby-redis/commit/a0543dbaf8444be352c14630cda589072bd213f9
      + Fix the d/rules to run redis during build
          - https://salsa.debian.org/ruby-team/ruby-redis/blob/a0543dbaf8444be352c14630cda589072bd213f9/debian/rules
  * ruby-image-processing
      + Exclude phashion from test suite
          - https://salsa.debian.org/ruby-team/ruby-image-processing/blob/2b713e323e407e4ecf2168d6ab14dd504eb653fe/debian/patches/exclude-phashion.patch
          - was discussed with mentor Tessy

### Uploaded packages
  * [unstable] ruby-vips/2.0.13-1
  * [unstable] ruby-minispec-metadata/3.3.0-1
  * [experimental] ruby-mini-magick/4.9.3-1
