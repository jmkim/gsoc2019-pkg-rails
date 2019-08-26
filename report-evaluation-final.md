# A Rails 6 package transition in Debian

GSoC 2019 Final evaluation report by Jongmin Kim.


## Project information
  - Project page: [A Rails 6 package transition in Debian](https://summerofcode.withgoogle.com/projects/#6363542624665600)
  - Organisation: [Ruby](https://summerofcode.withgoogle.com/organizations/5542255322988544/)
  - Project proposal (final): [proposal-final.pdf](https://github.com/jmkim/gsoc2019-pkg-rails/blob/gsoc2019/proposal/proposal-final.pdf)


## Final evaluation report

### Overview

I split the upgrading process into 3 phases. As of August 26th, I have completed phase 1 and 2.

**Phase 1: Upgrade the Rails dependencies**
  - [x] [estimate all the dependencies](https://wiki.debian.org/Teams/Ruby/Rails6/DependenciesTransition) *- done (5/11 ~ 5/20)*
  - [x] [introduce the project on ruby-team ML](https://lists.debian.org/debian-ruby/2019/05/msg00017.html) *- done (5/20)*
  - [x] [packaging all the dependencies](https://wiki.debian.org/Teams/Ruby/Rails6/DependenciesTransition) *- done (5/20 ~ 6/22)*

**Phase 2: Upgrade the Rails to 6**
  - [x] [package the rails 6.0.0 rc1](https://salsa.debian.org/jmkim-guest/rails) *- done (5/11 ~ 7/20)*
    - [x] fix all the test failures (using bundler) *- done (6/20 ~ 7/18)*
    - [ ] ~~fix all the test failures (using autopkgtest)~~ *- skip for now*
  - [x] [package the rails 6.0.0 stable](https://salsa.debian.org/ruby-team/rails/tree/transition-to-6) *- done (8/16 ~ 8/24)*
    - [x] rebase from the 5.2.3 branch *- done (8/23 ~ 8/24)*
    - [x] fix all the test failures (using bundler) *- done (8/16 ~ 8/22)*
    - [ ] ~~fix all the test failures (using autopkgtest)~~ *- skip for now*

**Phase 3: Upgrade the Rails reverse-dependencies (Rails apps/libraries)**
  - [x] [check all the reverse-dependencies](https://salsa.debian.org/ruby-team/rails/wikis/Transition-to-Rails-6-for-Debian-Bullseye/) *- (7/21)*
  - [x] [check all the rdepends if build failed or not](https://salsa.debian.org/ruby-team/rails/wikis/Transition-to-Rails-6-for-Debian-Bullseye/) *- done once (7/29 ~ 8/5), required recheck periodically*
  - [x] [check all the rdepends if upstream ready for rails 6 or not](https://salsa.debian.org/ruby-team/rails/wikis/Transition-to-Rails-6-for-Debian-Bullseye/) *- done once (8/5 ~ 8/9), required recheck periodically*
  - [ ] check all the rdepends with rails 6.0.0 stable
  - [ ] import the new version of *29 packages* which supports rails 6
  - [ ] patch the build failures of *55 packages* which not supports rails 6 *- in progress (8/12 ~)*
    - [ ] request to upstream for supporting rails 6 *- in progress (8/12 ~)*
    - [ ] send the patch to upstream as MR/PR


### Works Done

#### Contributed packages

For phase 1, I have worked on these packaging dependencies:

* [ruby-vips-2.0.13-1](https://salsa.debian.org/ruby-team/ruby-vips)
* [ruby-minispec-metadata-3.3.0-2](https://salsa.debian.org/ruby-team/ruby-minispec-metadata)
* [ruby-mini-magick-4.9.3-1](https://salsa.debian.org/ruby-team/ruby-mini-magick)
* [qunit-selenium-0.0.4-1](https://salsa.debian.org/ruby-team/qunit-selenium)
* [ruby-redis-4.1.2-1](https://salsa.debian.org/ruby-team/ruby-redis)
* [ruby-zeitwerk-2.1.6-1](https://salsa.debian.org/ruby-team/ruby-zeitwerk)
* [ruby-thor-0.20.3-1](https://salsa.debian.org/ruby-team/ruby-thor)
* [ruby-image-processing-1.9.0-1](https://salsa.debian.org/ruby-team/ruby-image-processing)
* [ruby-sass-rails-5.0.7-2](https://salsa.debian.org/ruby-team/ruby-sass-rails)
* [ruby-webpacker-4.0.7-1](https://salsa.debian.org/ruby-team/ruby-webpacker)

I have worked on these packages, however, dropped for some reasons:

* [ruby-bootsnap](https://salsa.debian.org/ruby-team/ruby-bootsnap) - exclude bootsnap from Rails package, due to [test failures](https://github.com/Shopify/bootsnap/issues/263)
* [ruby-foreman](https://salsa.debian.org/ruby-team/ruby-foreman) - reverse-dependency of [ruby-thor](https://salsa.debian.org/ruby-team/ruby-thor)
* [ruby-jaro-winkler](https://salsa.debian.org/jmkim-guest/ruby-jaro-winkler) - dependency of rubocop, which was not required
* [ruby-webdrivers](https://salsa.debian.org/jmkim-guest/ruby-webdrivers) - replaceable by [ruby-chromedriver-helper](https://salsa.debian.org/ruby-team/ruby-chromedriver-helper), which was already packaged

For phase 2, I have worked on Rails package:

* [rails-6.0.0~rc1+dfsg-1](https://salsa.debian.org/jmkim-guest/rails) - Rails 6.0.0 RC 1
* [rails-6.0.0+dfsg-1](https://salsa.debian.org/ruby-team/rails/tree/transition-to-6) - Rails 6.0.0 stable


#### Related contributions

I attended an annual Debian Conference, DebConf19 (7/14 ~ 7/24), and presented my project in some sessions.

Those are both live streamed, recorded and uploaded to YouTube:
* GSoC/Outreachy Projects (7/23) [26:00 ~ 31:00] [YouTube](https://youtu.be/tQEf5dbMudA?t=1560) / [DebConf19](https://debconf19.debconf.org/talks/113-gsocoutreachy-projects/) / [Google Slides](https://docs.google.com/presentation/d/1XkraFhVIds0k3ImGpChpwlwqqe132JZnQnvPZhRCTR0/edit?usp=sharing)
* Ruby Team BoF (7/23) [3:10 ~ 7:45] [YouTube](https://youtu.be/hAghpl_HA0g?t=190) / [DebConf19](https://debconf19.debconf.org/talks/44-ruby-team-bof/)


#### Non-related contributions

Not related to my project or Ruby, but a part of the Debian project, I contributed some packages:

* [libgit2-0.28.1+dfsg.1-0.1](https://salsa.debian.org/debian/libgit2)
* [ruby-rugged-0.28.1+ds-1](https://salsa.debian.org/ruby-team/ruby-rugged)
* [golang-gopkg-libgit2-git2go-0.28+git20190813.37e5b53-1](https://salsa.debian.org/go-team/packages/golang-gopkg-libgit2-git2go)
* [ruby-globalid-0.4.2+REALLY.0.3.6-1](https://salsa.debian.org/ruby-team/ruby-globalid/tree/buster)
* [ruby-httparty-0.16.4-1](https://salsa.debian.org/ruby-team/ruby-httparty)
* [ruby-gravtastic-3.2.6-1](https://salsa.debian.org/ruby-team/ruby-gravtastic)
* [ruby-paperclip-6.1.0-2](https://salsa.debian.org/ruby-team/ruby-paperclip)
* [ruby-sassc-2.0.1-1](https://salsa.debian.org/ruby-team/ruby-sassc)
* [ruby-batch-loader-1.4.1+dfsg.1-1](https://salsa.debian.org/ruby-team/ruby-batch-loader)
* [ruby-zip-1.2.0-1.1+deb9u1](https://salsa.debian.org/ruby-team/ruby-zip/tree/debian/stretch)
* [ruby-arbre-1.2.1-1](https://salsa.debian.org/jmkim-guest/ruby-arbre)
* [ruby-ahoy-email-0.5.2-1](https://salsa.debian.org/ruby-team/ruby-ahoy-email)


### Works to be done

I'm going to continue the work for upgrading/patching the reverse-dependencies.

As of August 26th, 84 packages are needed to transition. The full list is below. You could follow two sections: `Supported upstream` and `Upstream does not support rails 6 yet`. The list was refreshed with Rails 6.0.0~rc1.

Transition to Rails 6 for Debian Bullseye (aka. the list): https://salsa.debian.org/ruby-team/rails/wikis/Transition-to-Rails-6-for-Debian-Bullseye/

I could do two jobs for those two sections, which could run parallel:

1. For `Supported upstream` (29 pkgs): import those newer versions into Debian.
2. For `Upstream does not support rails 6 yet` (55 pkgs): request upstream to support Rails 6, or make a patch for them and forward as PR/MR.

Some packages categorised as `Upstream does not support rails 6 yet` are actually not an upstream problem.
The list was estimated with Rails 6.0.0~rc1. I have a lot of build failures which were Rails 6 RC1 problem. They were fixed on 6 stable release. So, refresh the list is needed.

3. Refresh the list with rails-6.0.0.


### Weekly reports

We (Ruby GSoC students) had the weekly meeting during GSoC period. It was happened on Slack (bundler.slack.com), you could read there by signing up at [here](https://slack.bundler.io/).

  * [Community Bonding Week 1](./weekly-report/cbp-week-1.md)
  * [Community Bonding Week 2](./weekly-report/cbp-week-2.md)
  * [Community Bonding Week 3](./weekly-report/cbp-week-3.md)
  * [Week 1](./weekly-report/week-1.md)
  * [Week 2](./weekly-report/week-2.md)
  * [Week 3](./weekly-report/week-3.md)
  * [Week 4](./weekly-report/week-4.md)
  * [Week 5 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1560175030001400)
  * [Week 6 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1560780043075000)
  * [Week 7 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1561384926123800)
  * [Week 8 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1561989820175400)
  * [Week 9 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1562594539005000)
  * [Week 10 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1563198909001700)
  * [Week 11 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1563798952004600)
  * [Week 12 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1564408945018700)
  * [Week 13 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1565013753046500)
  * [Week 14 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1565618538069800)
  * [Week 15 (#rubygsoc on bundler.slack.com)](https://bundler.slack.com/archives/C03TNNH59/p1566223120097100)


### Contact

* [jmkim@pukyong.ac.kr](mailto:jmkim@pukyong.ac.kr)
* `#jmkim` room on [oftc](https://webchat.oftc.net/?channels=%23jmkim)
