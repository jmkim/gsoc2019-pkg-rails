## Week 4
  * June 17 ~ June 23
  * #rubygsoc weekly meeting: (planned on June 24, at https://bundler.slack.com/messages/C03TNNH59 )

### Learned
  * UMEGAYA (DEP 12, aka. d/upstream/metadata)
      + https://wiki.debian.org/UpstreamMetadata
  * dh_ruby test is for build-time test, autopkgtest is for after-build-time test
  * dh_ruby --gem-install follows gemspec
      + https://manpages.debian.org/unstable/gem2deb/dh_ruby.1.en.html

### Worked
  * Package the Rails 6 (rails)
      + Fixing the test failures
      + https://salsa.debian.org/jmkim-guest/rails/commits/master
  * Package the missing Rails 6 dependency
      + ruby-webpacker
          - New package
          - Have a strong dependency relationship with Railties
          - https://salsa.debian.org/ruby-team/ruby-webpacker
  * Fixing the Railties tests related to Webpacker
      + Webpacker rake task hook issue
          - https://github.com/rails/webpacker/issues/2145

### Reported to upstream
  * ruby-webpacker
      + [issue:closed] `RakeTasksTest#test_rake_tasks` failure if webpacker `lib` directory name is changed to another name
          - https://github.com/rails/webpacker/issues/2145

### Patches
  * ruby-webpacker
      + Use system yarnpkg instead of yarn
          - https://salsa.debian.org/ruby-team/ruby-webpacker/blob/master/debian/patches/use-system-yarnpkg.patch
  * rails
      + Fix the test to use ffmpeg 4
          - https://salsa.debian.org/jmkim-guest/rails/blob/e7748254c177eed0b2d32f38ec6c5cc5d0c040a1/debian/patches/fix-test-to-use-ffmpeg-4.patch
