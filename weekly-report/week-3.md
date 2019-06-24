## Week 3
  * June 10 ~ June 16
  * #rubygsoc weekly meeting: https://bundler.slack.com/archives/C03TNNH59/p1560780043075000

### Learned
  * How to write a Rakefile
      + https://www.stuartellis.name/articles/rake/
      + https://martinfowler.com/articles/rake.html
      + https://medium.com/@sampatbadhe/rake-task-invoke-or-execute-419cd689c3bd
  * Port from Makefile to Rakefile
      + https://salsa.debian.org/ruby-team/ruby-redis/commit/182feeaf1dab69d191f8cf67f157aa0e707924a0
  * Manpage language - mdoc
      + https://manpages.debian.org/unstable/manpages/mdoc.7.en.html

### Worked
  * Fix the ruby-redis test failure
      + Currently redis-server is run by d/rules before test.
      + autopkgtest-pkg-ruby does not use d/rules.
      + So with autopkgtest-pkg-ruby, redis-server will not run before test.
      + https://salsa.debian.org/ruby-team/ruby-redis/commits/master
  * Package the Rails 6 dependencies
      + qunit-selenium
          - New package
          - https://salsa.debian.org/ruby-team/qunit-selenium
  * Write a manpage using mdoc, for qunit-selenium executable
      - https://salsa.debian.org/ruby-team/qunit-selenium/blob/ffaf6937443d2e112d7dba79ccf6eadd12694c77/debian/docs/qunit-selenium.1
  * Try to fix bootsnap issue
      + Ref: https://github.com/Shopify/bootsnap/issues/263
      + Stopped and skipped; bootsnap is not a required dependency
      + Will fix later or when the issue was fixed on upstream

### Reported to upstream
  * ruby-bootsnap
      + [PR:merged] Add helper_test with validating the cache path
          - https://github.com/Shopify/bootsnap/pull/261
      + [issue:opened] Cache path generated randomly when test on Debian packaging environment
          - https://github.com/Shopify/bootsnap/issues/263

### Patches
  * ruby-redis
      + Port from makefile to ruby-tests.rake for run redis during build (to replace d/rules for runtime test)
          - https://salsa.debian.org/ruby-team/ruby-redis/commit/182feeaf1dab69d191f8cf67f157aa0e707924a0
  * qunit-selenium
      + Use Chromium WebDriver instead of Firefox WebDriver (Mozilla geckodriver) which is not in Debian yet
          - https://salsa.debian.org/ruby-team/qunit-selenium/blob/ffaf6937443d2e112d7dba79ccf6eadd12694c77/debian/patches/use-chromium-driver.patch

### Uploaded packages
  * [unstable] ruby-zeitwerk/2.1.6-1
  * [unstable] qunit-selenium/0.0.4-1
  * [experimental] ruby-thor/0.20.3-1
  * [experimental] ruby-redis/4.1.2-1

