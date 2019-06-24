## Week 1
  * May 27 ~ June 2
  * #rubygsoc weekly meeting: https://bundler.slack.com/archives/C03TNNH59/p1559570765004700

### Learned
  * How to manage patches: `quilt` and `dpkg-source --commit`
      + quilt is for manage patch files
      + `dpkg-source --commit` creates a patch with current diff

### Worked
  * Update the Rails 6 dependencies
      + ruby-bootsnap
          - Upgrade from 1.3.0 to 1.4.4
          - https://salsa.debian.org/ruby-team/ruby-bootsnap/commits/master
      + ruby-rubocop
          - Stopped and skipped; is a code formatter for new contributors
          - Reported by Praveen: https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=929814#10
      + ruby-rubocop-performance
          - Dependency of ruby-rubocop
          - Stopped and skipped
      + ruby-whitequark-parser
          - Dependency of ruby-rubocop
          - Stopped and skipped
      + ruby-jaro-winkler
          - Dependency of ruby-rubocop
          - Stopped and skipped

### Patches
  * ruby-bootsnap
      + Import the missing tests
          - https://salsa.debian.org/ruby-team/ruby-bootsnap/commit/54d9b91096ff92d0450ab25e43b6a485a768f7d3
          - https://salsa.debian.org/ruby-team/ruby-bootsnap/commit/4bfcd241101be51c9afc2c61d9e3494d87845010
