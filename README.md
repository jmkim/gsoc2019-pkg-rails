# A Rails 6 package transition in Debian

1. **Contact information**
    - Email: jmkim@pukyong.ac.kr
    - OpenPGP key fingerprint: 012E 4A06 79E1 4EFC DAAE 9472 D39D 8D29 BAF3 6DF8
        - Get OpenPGP public key: https://jongmin.dev/pgp
    - Timezone: UTC+9 (KST, Korea Standard Time)
    - Average awake hours:
        - Mon-Fri: 12:00 ~ 23:00
        - Sat-Sun: 12:00 ~ 02:00
    - IRC nickname: jmkim
    - IRC channel: #jmkim/oftc
    - Matrix nickname: @jmkim:matrix.org
    - Phone: +82 10-9978-7433
    - Postal: A12-1309, 45, Yongso-ro, Nam-gu, Busan, 48513, Republic of Korea
    - GitHub: https://github.com/jmkim
    - Salsa: https://salsa.debian.org/jmkim-guest
    - Debian Wiki: https://wiki.debian.org/JongminKim


1. What project do you want to work on? This can be a project that you came up with yourself, a project that you collaborated with a project maintainer or possible GSoC mentor with, or a project that you chose from [the ideas list](https://github.com/rubygsoc/rubygsoc/wiki/Ideas-List).
    - [Rails6 Package Transition in Debian](https://github.com/rubygsoc/rubygsoc/wiki/Rails6-Package-Transition-in-Debian)


1. Why do you like Ruby, and why do you want to work on a Ruby project in GSoC 2019?




1. Describe your **experience** with the following: Ruby, C, other languages. (No experience is okay! We use this to evaluate projects and mentors for a good fit.)
    - Ruby
        - I created some script during writing this proposal, for measuring the reverse-dependencies of Rails:
            - A simple script for parsing Debian d/control file: https://github.com/jmkim/dpkg-control-parser
            - A simple script for download package from Debian Salsa and measure Rails reverse-dependencies: https://gist.github.com/jmkim/d5e3f1b9986d51fdbf9531d1b95909c5
    - C++
        - Universal Stock Crawler: https://github.com/jmkim/stock-crawler
    - Shell scripts
        - Google Domains DDNS Updater: https://github.com/jmkim/google-domains-ddns-updater
        - PDF to JPG converter: https://github.com/jmkim/pdf2jpg-bash
        - Bootup mailer: https://github.com/jmkim/bootmail
    - Web projects
        - [PHP] Simplex - Simple PHP file explorer: https://github.com/jmkim/simplex
        - [JavaScript] Open source software archive mirror service: https://ftp.harukasan.org/
        - [JavaScript, PHP] PAKDD2017 international conference website: http://pakdd2017.snu.ac.kr/
        - [JavaScript, PHP] State public officials relationship graph in Busan, South Korea: http://fun.busan.com/2019busan_public.php
        - [Java] Search engine for getting the educational background statistics in Busan, South Korea: http://db.pknu.ac.kr/dc/prj/bsn201701/
        - [Java] Map for showing the educational background statistics in Busan, South Korea: http://db.pknu.ac.kr/dc/prj/bsn201702/
    - I'm learning Ruby and have confidence in learning Ruby, as a lot of languages I already learnt (C, C++, Java, PHP, JavaScript, Go, Shell, Python).
      I have plans to use Rails for my future projects, so I want to become an expert in Ruby through this project.

1. Describe your **educational background**, including school, degree plan, major, and (if any) past degrees, research area, publications, etc.
    - (2015-current) Bachelor's degree, IT Convergence and Application Engineering, Pukyong National University.

1. Have you sent pull requests to any Ruby open source projects? Code or documentation patches are both useful! Please provide links.
    - During Debian activities, I did patch Ruby package "sup-mail".
        - Overview: https://salsa.debian.org/ruby-team/sup-mail/commits/master
        - Package transitions:
            - https://salsa.debian.org/ruby-team/sup-mail/commit/fd0c7421e8019bafec5a57dc0d3decfa85b57150
            - https://salsa.debian.org/ruby-team/sup-mail/commit/33a28eb758712baa5582df203c908f2ec64c06ef
            - https://salsa.debian.org/ruby-team/sup-mail/commit/9eb0cad6fba3188f0858fc95c2a7dda574ff2cd1
        - Upstream PR:
            - [OPENED] https://github.com/sup-heliotrope/sup/pull/549

1. What **other commitments** do you have this summer aside from GSoC? What obstacles do you foresee this summer as far as contributing the full forty hours per week during the GSoC period? 
    - No other commitments, except the plan for participating DebCamp19 and DebConf19 (below).

1. Are you planning any vacations or trips for fun this summer?
    - From 12 July to 27 July, I have a plan for participating DebCamp19 and DebConf19 (Debian conference). In this period, I'll do packaging sprint in Hacklab, in DebConf venue.

1. How many classes are you taking this summer?
    - One class (Digital signal processing).

1. Do you have any other employment this summer?
    - No.

1. If you've participated in GSoC before, tell us about the project(s) you have done. Please include a way to reach your previous mentor(s).
    - Didn't participated any outreach programmes before.

1. **propose a project**

<hr>

## Proposal: A Rails 6 package transition in Debian

### Project details
1. Update the Rails to 6.0.0 in Debian.
    1. Update the Rails dependencies in Debian [Appendix I](#appendix-i-measured-rails-dependencies-in-debian).
1. Patch the Rails applications and libraries to make compatible with Rails 6.0.0 [Appendix II](#appendix-ii-measured-rails-reverse-dependencies-in-debian).
1. Upload Rails 6, its dependencies, Rails applications and libraries.

### Glossary
1. "Rails frameworks": Libraries and frameworks in Rails (actionpack, activesupport, railties, ...).
1. "Rails applications" or "Rails applications and libraries": Applications and libraries which dependent on Rails.

### Synopsis
Rails is one of the most popular web frameworks in the world.
Rails is distributed in several distributions, and Debian is one of them.

Almost of web applications made with Rails are distributed using RubyGems.
The package manager in Ruby, RubyGems, is designed to distribute the web libraries multiple versions at the same time.
This can make the Rails applications maintain with multiple version of Rails frameworks.
However, the package management system in Debian is designed to deliver one version at a time, which cause mangling the dependency relationship.

Currently, the Rails version in Debian is 5.2.2. And all of Ruby applications and libraries in Debian are dependent on Rails 5.2.2.
This proposal proposes to upgrade Rails to 6.0.0 and change all Debian packages that dependent on Rails to be compatible with Rails 6.0.0.

### Deliverables
- People will be able to use Rails 6 in Debian by typing "apt install rails".
- The upcoming Rails 6 will be released on April 30[1]. With this proposal roadmap, Debian users will be able to use Rails 6 within 4 months after release.
- By patching the Rails applications and libraries and forward to their upstream, make them do fast transition to compatible with Rails 6.

### Success criteria
1. Can install Rails 6 on Debian with "apt install rails".
1. After Rails 6 released in Debian, all the packages should not have FTBFS (Failed To Build From Source).

### Packaging bases

#### Workflow diagram
![Rails 6 package transition workflow diagram](img/figure-01.png)

#### Measured values
1. In Debian, 169 packages dependent on Rails [Appendix II](#appendix-ii-measured-rails-reverse-dependencies-in-debian).
    1. 11 applications dependent on Rails:
        - camping, coquelicot, debci, diaspora, gitaly, gitlab, open-build-service, passenger, redmine, schleuder, sonic-pi
    1. 158 packages are the libraries which dependent on Rails frameworks.
1. In Debian, the count of reverse-dependencies of each Rails packages [Appendix II](#appendix-ii-measured-rails-reverse-dependencies-in-debian) are:
    - ruby-actioncable: none
    - ruby-actionmailbox: none (new module introduced from 6.0.0)
    - ruby-actionmailer: 8
    - ruby-actionpack: 25
    - ruby-actiontext: none (new module introduced from 6.0.0)
    - ruby-actionview: 5
    - ruby-activejob: none
    - ruby-activemodel: 17
    - ruby-activerecord: 37
    - ruby-activestorage: none
    - ruby-activesupport: 69
    - ruby-railties: 40
    - ruby-rails: 32
    - rails: 15
1. In Rails, the count of breaking changes, the version between 5 and 6 [Appendix III](#appendix-iii-breaking-changes-on-rails-6) are:
    - actioncable: 3
    - actionmailbox: none (new module introduced from 6.0.0)
    - actionmailer: 1
    - actionpack: 5
    - actiontext: none (new module introduced from 6.0.0)
    - actionview: 7
    - activejob: 2
    - activemodel: 3
    - activerecord: 21
    - activestorage: 3
    - activesupport: 12
    - railties: 21
1. As almost Rails interfaces as it is, it might be not at all packages need changes. If a patch is needed, make a transition with following [Appendix III](#appendix-iii-breaking-changes-on-rails-6).

### Timeline (based on measured values)
1. 7th May ~ 11th May: Update Rails dependencies to compatible with Rails 6.0.0.
1. 12th May ~ 18th May: Update Rails package to 6.0.0.
1. 19th May ~ 25th May: Update Rails package to 6.0.0 and release it with its dependencies into experimental. This might be done prior to the coding phase.
1. Week 1 (26th May ~ 1st June)
    - Learning the patching, with lesser changes Rails frameworks (actionmailer, activeview, actionpack, actionmodel).
    - ruby-actionmailer
        - ruby-mail-gpg
        - ruby-messagebus-api
        - ruby-exception-notification
    - ruby-activeview
        - ruby-rbpdf
        - ruby-rails-deprecated-sanitizer
    - ruby-actionpack
        - ruby-actionpack-page-caching
        - ruby-diaspora-federation-rails
        - ruby-escape-utils
        - ruby-gon
        - ruby-haml-magic-translations
        - ruby-ice-cube
        - ruby-redis-actionpack
        - ruby-rack-google-analytics
        - ruby-rails-timeago
    - ruby-activemodel
        - ruby-rails-observers
        - ruby-email-validator
        - ruby-openid-connect
        - ruby-rspec-collection-matchers
        - ruby-state-machines-activemodel
        - ruby-validate-url
        - ruby-activeldap
        - ruby-acts-as-api
        - ruby-pundit
        - ruby-sequel
1. Week 2 (2nd June ~ 8th June)
    - activesupport has a lot of breaking changes.
    - ruby-activesupport
        - ruby-awesome-print
        - ruby-babosa
        - ruby-backports
        - ruby-blade
        - ruby-case-transform
        - ruby-climate-control
        - ruby-clockwork
        - ruby-cocaine
        - ruby-delorean
        - ruby-excon
        - ruby-grape
        - ruby-grape-entity
        - ruby-grape-path-helpers
        - ruby-hashie
        - ruby-html-pipeline
1. Week 3 (9th June ~ 15th June)
    - activesupport has a lot of breaking changes.
    - ruby-activesupport
        - ruby-oj
        - ruby-omniauth-crowd
        - ruby-origin
        - ruby-rabl
        - ruby-rack-oauth2
        - ruby-rails-dom-testing
        - ruby-redis-activesupport
        - ruby-shoulda-matchers
        - ruby-spring-watcher-listen
        - ruby-swd
        - ruby-task-list
        - ruby-timecop
        - ruby-treetop
        - ruby-webfinger
        - ruby-wikicloth
1. Week 4 (16th June ~ 22nd June)
    - Both activesupport and activerecord have a lot of breaking changes.
    - activerecord is related to RDBMS connector, so transition might quite complex than others.
    - ruby-activerecord
        - ruby-activemodel-serializers-xml
        - ruby-activerecord-import
        - ruby-activerecord-nulldb-adapter
        - ruby-acts-as-list
        - ruby-acts-as-taggable-on
        - ruby-acts-as-tree
        - ruby-after-commit-queue
        - ruby-attr-encrypted
        - ruby-database-cleaner
        - ruby-default-value-for
        - ruby-delayed-job
        - ruby-delayed-job-active-record
        - ruby-em-synchrony
        - ruby-factory-bot
        - ruby-fast-gettext
1. Week 5 (23rd June ~ 29th June)
    - activerecord is related to RDBMS connector and has a lot of breaking changes, so transition might be complex than others.
    - ruby-activerecord
        - ruby-flipper
        - ruby-kaminari
        - ruby-model-tokenizer
        - ruby-moneta
        - ruby-parallel
        - ruby-paranoia
        - ruby-roxml
        - ruby-seamless-database-pool
        - ruby-seed-fu
        - ruby-sequenced
        - ruby-state-machines-activerecord
        - ruby-stringex
        - ruby-thinking-sphinx
        - ruby-validate-email
1. Week 6 (30th June ~ 6th July)
    - Railties handles the command line interfaces and has a lot of breaking changes, so transition might be complex than others.
    - ruby-railties
        - ruby-actionpack-xml-parser
        - ruby-backbone-on-rails
        - ruby-browser
        - ruby-coffee-rails
        - ruby-doorkeeper
        - ruby-entypo-rails
        - ruby-factory-bot-rails
        - ruby-font-awesome-rails
        - ruby-generator-spec
        - ruby-i18n-inflector-rails
        - ruby-jquery-rails
        - ruby-jquery-scrollto-rails
        - ruby-jquery-ui-rails
        - ruby-js-routes
1. Week 7 (7th July ~ 11th July)
    - Railties handles the command line interfaces and has a lot of breaking changes, so transition might be complex than others.
    - ruby-railties
        - ruby-devise
        - ruby-devise-two-factor
        - ruby-jira
        - ruby-lograge
        - ruby-markerb
        - ruby-momentjs-rails
        - ruby-peek
        - ruby-rabl-rails
        - ruby-rails-i18n
        - ruby-request-store
        - ruby-sass-rails
        - ruby-sidekiq
        - ruby-versionist
        - ruby-web-console
        - ruby-webpack-rails
1. Week 8 (14th July ~ 20th July, in DebCamp19)
    - Package binary packages in DebCamp Hacklab. Rails applications are huge and complex, so work in DebCamp might be helpful for asking a guide from Ruby developers and Debian mentors.
    - Binary packages (Rails applications)
        - camping
        - coquelicot
        - debci
        - diaspora
        - gitlab
1. Week 9 (21st July ~ 26 July, in DebConf19)
    - Package binary packages in DebCamp Hacklab. Rails applications are huge and complex, so work in DebCamp might be helpful for asking a guide from Ruby developers and Debian mentors.
    - Binary packages (Rails applications)
        - gitaly
        - open-build-service
        - passenger
        - redmine
        - schleuder
        - sonic-pi
1. Week 10 (28th July ~ 3rd August)
    - Package complex libraries. ruby-rails contains all of Rails frameworks.
    - Weak ruby-rails (might not contain all the Rails frameworks)
        - ruby-actionpack-action-caching
        - ruby-asset-sync
        - ruby-codemirror-rails
        - ruby-data-migrate
        - ruby-devise-lastseenable
        - ruby-enumerize
        - ruby-hamlit
        - ruby-joiner
        - ruby-leaflet-rails
        - ruby-premailer-rails
        - ruby-rails-tokeninput
        - ruby-sprockets-rails
        - ruby-validates-hostname
        - ruby-active-model-serializers
1. Week 11 (4th August ~ 10th August)
    - Package complex libraries. ruby-rails and rails contains all the Rails frameworks.
    - Strong ruby-rails (contain all the Rails frameworks)
        - ruby-appraiser
        - ruby-flot-rails
        - ruby-gettext-i18n-rails
        - ruby-gettext-i18n-rails-js
        - ruby-rqrcode-rails3
        - ruby-sentry-raven
        - ruby-simple-captcha2
        - ruby-snorlax
        - ruby-yaml-db
        - ruby-api-pagination
        - ruby-carrierwave
        - ruby-combustion
    - rails
        - ruby-dalli
        - ruby-globalid
1. Week 12 (11th August ~ 17th August)
    - Package complex libraries. ruby-rails and rails contains all the Rails frameworks.
    - rails
        - ruby-haml
        - ruby-haml-rails
        - ruby-hashie-forbidden-attributes
        - ruby-health-check
        - ruby-jbuilder
        - ruby-jquery-atwho-rails
        - ruby-js-image-paths
        - ruby-mobile-fu
        - ruby-rails-html-sanitizer
        - ruby-responders
        - ruby-roadie-rails
        - ruby-rspec-rails
        - ruby-spring
        - ruby-voight-kampff
1. Week 13 (18th August ~ 24th August)
    - Ready for submit final work report

### Some notes regarding timeline

1. Week 8~9: Have a plan for participating DebCamp19 and DebConf19 (Debian conference) from 12 July to 27 July. In this period, do sprint in Hacklab, in DebConf venue.

1. A lot of packages should be done transition, so the timeline should be re-estimate occasionally during community bonding phase and coding phase.

### References
[1] https://weblog.rubyonrails.org/2018/12/20/timeline-for-the-release-of-Rails-6-0/
[2] https://github.com/rails/rails

<hr>

## Appendices

1. [Appendix I: Measured Rails dependencies in Debian](#appendix-i-measured-rails-dependencies-in-debian)
1. [Appendix II: Measured Rails reverse-dependencies in Debian](#appendix-ii-measured-rails-reverse-dependencies-in-debian)
1. [Appendix III: Breaking changes on Rails 6](#appendix-iii-breaking-changes-on-rails-6)

### Appendix I: Measured Rails dependencies in Debian
- New package needed:
    - activerecord-jdbc-adapter (52.1-java)
    - activerecord-jdbcmysql-adapter (52.1-java)
    - activerecord-jdbcpostgresql-adapter (52.1-java)
    - activerecord-jdbcsqlite3-adapter (52.1-java)
    - backburner
    - concurrent-ruby (1.1.4)
    - curses (1.0.4)
    - dante (0.2.0)
    - digest-crc (0.4.1)
    - image-processing (1.7.1)
    - jaro_winkler (1.5.2-java)
    - jmespath (1.4.0)
    - kindlerb (1.2.0)
    - mini_portile2 (2.4.0)
    - minitest-bisect (1.4.0)
    - minitest-retry (0.1.9)
    - minitest-server (1.0.5)
    - net_http_ssl_fix (0.0.10)
    - path_expander (1.0.3)
    - puma (3.12.1)
    - que (0.14.3)
    - qunit-selenium (0.0.4)
    - railties (>=4.2)
    - rb-fsevent (0.10.3)
    - rdoc (6.0.4)
    - resque (1.27.4)
    - resque-scheduler (4.3.1)
    - ruby_dep (1.5.0)
    - ruby-vips (>=2.0.13,<3)
    - sass (3.7.2)
    - sass-listen (4.0.0)
    - serverengine (2.0.7)
    - sigdump (0.2.4)
    - sneakers (2.11.0)
    - stackprof (0.2.12)
    - sucker_punch (2.1.1)
    - w3c_validators (1.3.4)
    - wdm (0.1.1)
    - webdrivers (3.7.0)
    - webpacker (4.0.2)
    - zeitwerk (1.4.3)

- Transition needed:
    - https://salsa.debian.org/ruby-team/ruby-ast (2.4.0 needed, 2.3.0 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-benchmark-ips (2.7.2 needed, 1.2.0 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-bunny (2.13.0 needed, 2.9.2 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-daemons (1.2.6 needed, 1.1.9 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-erubi (1.8.0 needed, 1.7.1 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-eventmachine (1.2.7 needed, 1.0.7 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-execjs (2.7.0 needed, 2.6.7 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-ffi (1.10.0 needed, 1.9.10 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-hashdiff (0.2.3 needed, 0.3.7 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-i18n (1.6.0 needed, 1.5.3 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-mime-types-data (3.2018.0812 needed, 3.2015.1120 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-msgpack (1.2.9 needed, 1.1.0 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-multi-json (1.13.1 needed, 1.12.1 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-mustache (1.1.0 needed, 1.0.2 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-os (1.0.0 needed, 0.9.6 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-parallel (1.13.0 needed, 0.12.1 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-rack-cache (1.8.0 needed, 1.2 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-rack-protection (2.0.4 needed, 1.5.3 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-rack-test (1.1.0 needed, 0.7.0 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-rb-inotify (1.10.0 needed, 0.9.10 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-redis (4.0.3 needed, 3.3.5 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-regexp-parser (1.3.0 needed, 1.2.0 in Debian)
    - https://salsa.debian.org/ruby-team/rubocop (0.66.0 needed, 0.52.1 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-progressbar (0.10.0 needed, 0.9.0 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-rufus-scheduler (3.5.2 needed, 3.4.2 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-sdoc (1.0.0 needed, 0.4.1 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-selenium-webdriver (3.141.0 needed, 3.12.0 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-thor (0.20.3 needed, 0.19.4 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-turbolinks (5.2.0 needed, 5.1.1 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-turbolinks-source (5.2.0 needed, 5.1.0 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-tzinfo-data (1.2018.7 needed, 1.2016.6 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-unicode-display-width (1.5.0 needed, 1.1.1 in Debian)
    - https://salsa.debian.org/ruby-team/ruby-websocket-driver (0.7.0 needed, 0.6.3 in Debian)

- No change needed:
    - https://salsa.debian.org/ruby-team/ruby-addressable
    - https://salsa.debian.org/ruby-team/ruby-amq-protocol
    - https://salsa.debian.org/ruby-team/ruby-beaneater
    - https://salsa.debian.org/ruby-team/ruby-blade
    - https://salsa.debian.org/ruby-team/ruby-blade-qunit-adapter
    - https://salsa.debian.org/ruby-team/ruby-blade-sauce-labs-plugin
    - https://salsa.debian.org/ruby-team/ruby-builder
    - https://salsa.debian.org/ruby-team/ruby-byebug
    - https://salsa.debian.org/ruby-team/ruby-capybara
    - https://salsa.debian.org/ruby-team/ruby-childprocess
    - https://salsa.debian.org/ruby-team/ruby-coffee-script
    - https://salsa.debian.org/ruby-team/ruby-connection-pool
    - https://salsa.debian.org/ruby-team/ruby-cookiejar
    - https://salsa.debian.org/ruby-team/ruby-crack
    - https://salsa.debian.org/ruby-team/ruby-crass
    - https://salsa.debian.org/ruby-team/ruby-dalli
    - https://salsa.debian.org/ruby-team/ruby-declarative
    - https://salsa.debian.org/ruby-team/ruby-declarative-option
    - https://salsa.debian.org/ruby-team/ruby-delayed-job
    - https://salsa.debian.org/ruby-team/ruby-delayed-job-active-record
    - https://salsa.debian.org/ruby-team/ruby-em-http-request
    - https://salsa.debian.org/ruby-team/ruby-et-orbi
    - https://salsa.debian.org/ruby-team/ruby-faraday
    - https://salsa.debian.org/ruby-team/ruby-faraday-middleware
    - https://salsa.debian.org/ruby-team/ruby-faye
    - https://salsa.debian.org/ruby-team/ruby-faye-websocket
    - https://salsa.debian.org/ruby-team/ruby-fugit
    - https://salsa.debian.org/ruby-team/ruby-globalid
    - https://salsa.debian.org/ruby-team/ruby-hiredis
    - https://salsa.debian.org/ruby-team/ruby-httpclient
    - https://salsa.debian.org/ruby-team/ruby-http-parser.rb
    - https://salsa.debian.org/ruby-team/ruby-jar-dependencies
    - https://salsa.debian.org/ruby-team/ruby-json
    - https://salsa.debian.org/ruby-team/ruby-jwt
    - https://salsa.debian.org/ruby-team/ruby-libxml
    - https://salsa.debian.org/ruby-team/ruby-listen
    - https://salsa.debian.org/ruby-team/ruby-loofah
    - https://salsa.debian.org/ruby-team/ruby-mail
    - https://salsa.debian.org/ruby-team/ruby-marcel
    - https://salsa.debian.org/ruby-team/ruby-memoist
    - https://salsa.debian.org/ruby-team/ruby-method-source
    - https://salsa.debian.org/ruby-team/ruby-mimemagic
    - https://salsa.debian.org/ruby-team/ruby-mime-types
    - https://salsa.debian.org/ruby-team/ruby-mini-magick
    - https://salsa.debian.org/ruby-team/ruby-mini-mime
    - https://salsa.debian.org/ruby-team/ruby-minitest
    - https://salsa.debian.org/ruby-team/ruby-mono-logger
    - https://salsa.debian.org/ruby-team/ruby-multipart-post
    - https://salsa.debian.org/ruby-team/ruby-mustermann
    - https://salsa.debian.org/ruby-team/ruby-mysql2
    - https://salsa.debian.org/ruby-team/ruby-nio4r
    - https://salsa.debian.org/ruby-team/ruby-nokogiri
    - https://salsa.debian.org/ruby-team/ruby-parser
    - https://salsa.debian.org/ruby-team/ruby-pg
    - https://salsa.debian.org/ruby-team/ruby-psych
    - https://salsa.debian.org/ruby-team/ruby-public-suffix
    - https://salsa.debian.org/ruby-team/ruby-raabro
    - https://salsa.debian.org/ruby-team/racc
    - https://salsa.debian.org/ruby-team/ruby-rack
    - https://salsa.debian.org/ruby-team/ruby-rack-proxy
    - https://salsa.debian.org/ruby-team/ruby-rails-dom-testing
    - https://salsa.debian.org/ruby-team/ruby-rails-html-sanitizer
    - https://salsa.debian.org/ruby-team/ruby-rainbow
    - https://salsa.debian.org/ruby-team/rake
    - https://salsa.debian.org/ruby-team/ruby-redcarpet
    - https://salsa.debian.org/ruby-team/ruby-redis-namespace
    - https://salsa.debian.org/ruby-team/ruby-representable
    - https://salsa.debian.org/ruby-team/ruby-retriable
    - https://salsa.debian.org/ruby-team/ruby-zip
    - https://salsa.debian.org/ruby-team/ruby-safe-yaml
    - https://salsa.debian.org/ruby-team/ruby-sass-rails
    - https://salsa.debian.org/ruby-team/ruby-sequel
    - https://salsa.debian.org/ruby-team/ruby-sidekiq
    - https://salsa.debian.org/ruby-team/ruby-signet
    - https://salsa.debian.org/ruby-team/ruby-sinatra
    - https://salsa.debian.org/ruby-team/ruby-sprockets
    - https://salsa.debian.org/ruby-team/ruby-sprockets-export
    - https://salsa.debian.org/ruby-team/ruby-sprockets-rails
    - https://salsa.debian.org/ruby-team/ruby-sqlite3
    - https://salsa.debian.org/ruby-team/thin
    - https://salsa.debian.org/ruby-team/ruby-thread-safe
    - https://salsa.debian.org/ruby-team/ruby-tilt
    - https://salsa.debian.org/ruby-team/ruby-tzinfo
    - https://salsa.debian.org/ruby-team/ruby-uber
    - https://salsa.debian.org/ruby-team/ruby-uglifier
    - https://salsa.debian.org/ruby-team/ruby-useragent
    - https://salsa.debian.org/ruby-team/ruby-vegas
    - https://salsa.debian.org/ruby-team/ruby-webmock
    - https://salsa.debian.org/ruby-team/ruby-websocket
    - https://salsa.debian.org/ruby-team/ruby-websocket-extensions
    - https://salsa.debian.org/ruby-team/ruby-xpath

### Appendix II: Measured Rails reverse-dependencies in Debian
- https://salsa.debian.org/ruby-team/camping
    - [Recommends] ruby-activerecord
- https://salsa.debian.org/debian/coquelicot
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ci-team/debci
    - [Build-Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/diaspora
    - [Depends] ruby-rails
- https://salsa.debian.org/go-team/packages/gitaly
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/gitlab
    - [Depends] ruby-rails
- https://salsa.debian.org/ruby-team/open-build-service
    - [Build-Depends] rails
    - [Build-Depends] ruby-actionview
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/passenger
    - [Suggests] rails
- https://salsa.debian.org/ruby-team/redmine
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-actionpack-action-caching
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-actionpack-page-caching
    - [Build-Depends, Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-actionpack-xml-parser
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-activeldap
    - [Build-Depends, Depends] ruby-activemodel
    - [Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-active-model-serializers
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-activemodel
    - [Build-Depends] ruby-activerecord
    - [Build-Depends] ruby-rails
    - [Build-Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-activemodel-serializers-xml
    - [Build-Depends] ruby-activerecord
    - [Build-Depends, Depends] ruby-activemodel
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-activerecord-import
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-activerecord-nulldb-adapter
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-acts-as-api
    - [Depends] ruby-activemodel
    - [Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-acts-as-list
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-acts-as-taggable-on
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-acts-as-tree
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-after-commit-queue
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-api-pagination
    - [Build-Depends] rails
- https://salsa.debian.org/ruby-team/ruby-appraiser
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-asset-sync
    - [Build-Depends, Depends] ruby-activemodel
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-attr-encrypted
    - [Build-Depends] ruby-activerecord
    - [Build-Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-awesome-print
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-babosa
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-backbone-on-rails
    - [Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-backports
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-blade
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-browser
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-carrierwave
    - [Build-Depends] rails
    - [Build-Depends, Depends] ruby-activemodel
    - [Build-Depends] ruby-activerecord
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-case-transform
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-climate-control
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-clockwork
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-cocaine
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-codemirror-rails
    - [Depends] ruby-rails
    - [Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-coffee-rails
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-combustion
    - [Build-Depends] rails
    - [Depends] ruby-activesupport
    - [Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-dalli
    - [Build-Depends] rails
- https://salsa.debian.org/ruby-team/ruby-database-cleaner
    - [Build-Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-data-migrate
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-default-value-for
    - [Build-Depends, Depends] ruby-activerecord
    - [Build-Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-delayed-job
    - [Build-Depends] ruby-actionmailer
    - [Build-Depends, Depends] ruby-activerecord
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-delayed-job-active-record
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-delorean
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-devise
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-devise-lastseenable
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-devise-two-factor
    - [Build-Depends] ruby-activemodel
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-diaspora-federation-rails
    - [Build-Depends, Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-doorkeeper
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-email-validator
    - [Build-Depends, Depends] ruby-activemodel
- https://salsa.debian.org/ruby-team/ruby-em-synchrony
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-entypo-rails
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-enumerize
    - [Build-Depends] ruby-rails
    - [Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-escape-utils
    - [Build-Depends, Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-exception-notification
    - [Depends] ruby-actionmailer
    - [Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-excon
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-factory-bot
    - [Build-Depends] ruby-activerecord
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-factory-bot-rails
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-fast-gettext
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-flipper
    - [Build-Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-flot-rails
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-font-awesome-rails
    - [Depends] ruby-activesupport
    - [Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-generator-spec
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-gettext-i18n-rails
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-gettext-i18n-rails-js
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-globalid
    - [Build-Depends] rails
    - [Build-Depends, Depends] ruby-activesupport
    - [Recommends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-gon
    - [Build-Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-grape
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-grape-entity
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-grape-path-helpers
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-haml
    - [Build-Depends, Suggests] rails
- https://salsa.debian.org/ruby-team/ruby-hamlit
    - [Build-Depends] ruby-actionpack
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-haml-magic-translations
    - [Build-Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-haml-rails
    - [Build-Depends] rails
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-hashie
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-hashie-forbidden-attributes
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-health-check
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-html-pipeline
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-http-accept-language
    - [Build-Depends, Depends] ruby-activesupport
    - [Suggests] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-i18n
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-i18n-inflector-rails
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-ice-cube
    - [Build-Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-jbuilder
    - [Build-Depends] rails
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-jira
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-joiner
    - [Build-Depends] ruby-rails
    - [Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-jquery-atwho-rails
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-jquery-datatables-rails
    - [Depends] ruby-actionpack
    - [Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-jquery-rails
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-jquery-scrollto-rails
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-jquery-ui-rails
    - [Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-js-image-paths
    - [Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-json-jwt
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-js-routes
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-kaminari
    - [Build-Depends, Depends] ruby-activesupport
    - [Depends] ruby-actionview
    - [Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-leaflet-rails
    - [Build-Depends] ruby-actionpack
    - [Build-Depends] ruby-activesupport
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-lograge
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-mail-gpg
    - [Build-Depends] ruby-actionmailer
- https://salsa.debian.org/ruby-team/ruby-markerb
    - [Build-Depends] ruby-actionmailer
    - [Build-Depends] ruby-activesupport
    - [Build-Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-messagebus-api
    - [Build-Depends] ruby-actionmailer
- https://salsa.debian.org/ruby-team/ruby-mobile-fu
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-model-tokenizer
    - [Build-Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-momentjs-rails
    - [Build-Depends] ruby-actionmailer
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-moneta
    - [Suggests] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-oj
    - [Suggests] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-omniauth-crowd
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-openid-connect
    - [Build-Depends, Depends] ruby-activemodel
- https://salsa.debian.org/ruby-team/ruby-origin
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-parallel
    - [Build-Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-paranoia
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-peek
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-premailer-rails
    - [Build-Depends, Depends] ruby-actionmailer
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-pundit
    - [Build-Depends] ruby-actionpack
    - [Build-Depends] ruby-activemodel
    - [Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-rabl
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-rabl-rails
    - [Build-Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-rack-google-analytics
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-rack-oauth2
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-rails-deprecated-sanitizer
    - [Build-Depends] ruby-actionview
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-rails-dom-testing
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-rails-html-sanitizer
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-rails-i18n
    - [Build-Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-rails-observers
    - [Build-Depends, Depends] ruby-activemodel
- https://salsa.debian.org/ruby-team/ruby-rails-timeago
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-rails-tokeninput
    - [Depends] ruby-rails
    - [Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-rbpdf
    - [Build-Depends] ruby-actionview
- https://salsa.debian.org/ruby-team/ruby-redis-actionpack
    - [Build-Depends, Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-redis-activesupport
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-request-store
    - [Suggests] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-responders
    - [Build-Depends] rails
    - [Build-Depends, Depends] ruby-railties
    - [Build-Depends] ruby-actionpack
- https://salsa.debian.org/ruby-team/ruby-roadie-rails
    - [Build-Depends] rails
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-roxml
    - [Build-Depends] ruby-activerecord
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-rqrcode-rails3
    - [Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-rspec-collection-matchers
    - [Build-Depends] ruby-activemodel
- https://salsa.debian.org/ruby-team/ruby-rspec-rails
    - [Build-Depends] rails
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-sass-rails
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-seamless-database-pool
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-seed-fu
    - [Build-Depends, Depends] ruby-activerecord
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-sentry-raven
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-sequel
    - [Build-Depends] ruby-activemodel
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-sequenced
    - [Build-Depends, Depends] ruby-activerecord
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-shoulda-matchers
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-sidekiq
    - [Build-Depends] ruby-actionmailer
    - [Build-Depends] ruby-activerecord
    - [Build-Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-simple-captcha2
    - [Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-snorlax
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-spring
    - [Build-Depends] rails
- https://salsa.debian.org/ruby-team/ruby-spring-watcher-listen
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-sprockets-rails
    - [Build-Depends, Depends] ruby-actionpack
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-state-machines-activemodel
    - [Build-Depends, Depends] ruby-activemodel
- https://salsa.debian.org/ruby-team/ruby-state-machines-activerecord
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-stringex
    - [Build-Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-swd
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-task-list
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-thinking-sphinx
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-timecop
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-treetop
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-validate-email
    - [Build-Depends, Depends] ruby-activemodel
    - [Build-Depends] ruby-activerecord
- https://salsa.debian.org/ruby-team/ruby-validates-hostname
    - [Build-Depends, Depends] ruby-activerecord
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends] ruby-rails
- https://salsa.debian.org/ruby-team/ruby-validate-url
    - [Build-Depends, Depends] ruby-activemodel
- https://salsa.debian.org/ruby-team/ruby-versionist
    - [Build-Depends, Depends] ruby-activesupport
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-voight-kampff
    - [Build-Depends] rails
- https://salsa.debian.org/ruby-team/ruby-web-console
    - [Build-Depends, Depends] ruby-activemodel
    - [Build-Depends, Depends] ruby-actionview
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-webfinger
    - [Build-Depends, Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-webpack-rails
    - [Build-Depends, Depends] ruby-railties
- https://salsa.debian.org/ruby-team/ruby-wikicloth
    - [Build-Depends] ruby-activesupport
- https://salsa.debian.org/ruby-team/ruby-yaml-db
    - [Build-Depends, Depends] ruby-rails
- https://salsa.debian.org/ruby-team/schleuder
    - [Build-Depends, Depends] ruby-activerecord
- https://salsa.debian.org/multimedia-team/sonic-pi
    - [Build-Depends, Depends] ruby-activesupport

### Appendix III: Breaking changes on Rails 6
- actioncable
    - https://github.com/rails/rails/blob/master/actioncable/CHANGELOG.md
    - npm package renamed from `actioncable` to `@rails/actioncable`.
    - Configuration of the `WebSocket` adapter and `logger` adapter have been moved from properties of `ActionCable` to properties of `ActionCable.adapters`.
    - The `ActionCable.startDebugging()` and `ActionCable.stopDebugging()` methods have been removed and replaced with the property `ActionCable.logger.enabled`.
- actionmailbox
    - https://github.com/rails/rails/blob/master/actionmailbox/CHANGELOG.md
    - (new module introduced from 6.0.0)
- actionmailer
    - https://github.com/rails/rails/blob/master/actionmailer/CHANGELOG.md
    - Deprecate `ActionMailer::Base.receive` in favor of `actionmailbox`.
- actionpack
    - https://github.com/rails/rails/blob/master/actionpack/CHANGELOG.md
    - Remove deprecated `fragment_cache_key` helper in favor of `combined_fragment_cache_key`.
    - Remove deprecated methods in `ActionDispatch::TestResponse`.
      `#success?`, `missing?` and `error?` were deprecated in Rails 5.2 in favor of `#successful?`, `not_found?` and `server_error?`.
    - Deprecate `ActionDispatch::Http::ParameterFilter` in favor of `ActiveSupport::ParameterFilter`.
    - Encode Content-Disposition filenames on `send_data` and `send_file`.
        - Previously, `send_data 'data', filename: "\u{3042}.txt"` sends `"filename=\"\u{3042}.txt\""`.
        - Now it follows RFC 2231 and RFC 5987 and sends `"filename=\"%3F.txt\"; filename*=UTF-8''%E3%81%82.txt"`.
    - Controller level `force_ssl` has been deprecated in favor of `config.force_ssl`.
- actiontext
    - https://github.com/rails/rails/blob/master/actiontext/CHANGELOG.md
    - (new module introduced from 6.0.0)
- actionview
    - https://github.com/rails/rails/blob/master/actionview/CHANGELOG.md
    - npm package renamed from `rails-ujs` to `@rails/ujs`.
    - Remove deprecated `image_alt` helper.
    - Deprecate calling private model methods from view helpers.
    - Remove `ActionView::Helpers::RecordTagHelper`.
    - Disable `ActionView::Template` finalizers in test environment.
    - Don't enforce UTF-8 by default.
    - Change translation key of `submit_tag` from `module_name_class_name` to `module_name/class_name`.
- activejob
    - https://github.com/rails/rails/blob/master/activejob/CHANGELOG.md
    - Return false instead of the job instance when `enqueue` is aborted.
        - This will be the behavior in Rails 6.1 but it can be controlled now with `config.active_job.return_false_on_aborted_enqueue`.
    - Remove support for Qu gem.
- activemodel
    - https://github.com/rails/rails/blob/master/activemodel/CHANGELOG.md
    - Fix date value when casting a multiparameter date hash to not convert from Gregorian date to Julian date.
    - Fix year value when casting a multiparameter time hash.
    - Fix `ActiveModel::Serializers::JSON#as_json` method for timestamps.
- activerecord
    - https://github.com/rails/rails/blob/master/activerecord/CHANGELOG.md
    - Fix query attribute method on user-defined attribute to be aware of typecasted value.
    - Deprecate mismatched collation comparison for uniqueness validator.
        - Uniqueness validator will no longer enforce case sensitive comparison in Rails 6.1. To continue case sensitive comparison on the case insensitive column, pass case_sensitive: true option explicitly to the uniqueness validator.
    - Don't allow `where` with non numeric string matches to 0 values.
    - Don't allow `where` with invalid value matches to nil values.
    - Deprecate using class level querying methods if the receiver scope regarded as leaked. Use `klass.unscoped` to avoid the leaking scope.
    - Remove deprecated `#set_state` from the transaction object.
    - Remove deprecated `#supports_statement_cache?` from the database adapters.
    - Remove deprecated `#insert_fixtures` from the database adapters.
    - Remove deprecated `ActiveRecord::ConnectionAdapters::SQLite3Adapter#valid_alter_table_type?`.
    - Do not allow passing the column name to `sum` when a block is passed.
    - Do not allow passing the column name to `count` when a block is passed.
    - Deprecate `config.activerecord.sqlite3.represent_boolean_as_integer`.
    - Change `SQLite3Adapter` to always represent boolean values as integers.
    - Remove ability to specify a timestamp name for `#cache_key`.
    - Remove deprecated `ActiveRecord::Migrator.migrations_path=`.
    - Remove deprecated `expand_hash_conditions_for_aggregates`.
    - Deprecate passing `migrations_paths` to `connection.assume_migrated_upto_version`.
    - Raise an error instead of scanning the filesystem root when `fixture_path` is blank.
    - Deprecate `ActiveRecord::Result#to_hash` in favor of `ActiveRecord::Result#to_a`.
    - Deprecate `column_name_length`, `table_name_length`, `columns_per_table`, `indexes_per_table`, `columns_per_multicolumn_index`, `sql_query_length`, and `joins_per_query` methods in `DatabaseLimits`.
    - Deprecate `update_attributes/!` in favor of `update/!`.
- activestorage
    - https://github.com/rails/rails/blob/master/activestorage/CHANGELOG.md
    - npm package renamed from `activestorage` to `@rails/activestorage`.
    - Replace `config.active_storage.queue` to `config.active_storage.queues.analysis` and `config.active_storage.queues.purge`.
    - Active Storage error classes now inherit from `ActiveStorage::Error` instead of `StandardError`.
- activesupport
    - https://github.com/rails/rails/blob/master/activesupport/CHANGELOG.md
    - Fix `Time#advance` to work with dates before 1001-03-07.
    - Remove the `Kernel#` override that suppresses ENOENT and accidentally returns nil on Unix systems.
    - Remove deprecated `Module#reachable?` method.
    - Remove deprecated `#acronym_regex` method from `Inflections`.
    - Deprecate `ActiveSupport::Multibyte::Unicode#pack_graphemes(array)` in favor of `array.flatten.pack("U*")`.
    - Deprecate `ActiveSuppport::Multibyte::Unicode#unpack_graphemes(string)` in favor of `string.scan(/\X/).map(&:codepoints)`.
    - Deprecate `ActiveSupport::Multibyte::Chars.consumes?` in favor of `String#is_utf8?`.
    - Deprecate `ActiveSupport::Multibyte::Unicode#normalize` and `ActiveSuppport::Multibyte::Chars#normalize` in favor of `String#unicode_normalize`.
    - Deprecate `ActiveSupport::Multibyte::Unicode#downcase/upcase/swapcase` in favor of `String#downcase/upcase/swapcase`.
    - Rename `Module#parent`, `Module#parents`, and `Module#parent_name` to `module_parent`, `module_parents`, and `module_parent_name`.
    - Deprecate the use of `LoggerSilence` in favor of `ActiveSupport::LoggerSilence`.
    - Deprecate using negative limits in `String#first` and `String#last`.
- railties
    - https://github.com/rails/rails/blob/master/railties/CHANGELOG.md
    - The `connection` option of `rails dbconsole` command is deprecated in favor of `database` option.
    - Replace `chromedriver-helper` gem with `webdrivers` in default Gemfile.
    - Applications running in `:zeitwerk` mode that use `bootsnap` need to upgrade `bootsnap` to at least 1.4.2.
    - Remove deprecated `after_bundle` helper inside plugins template
    - Remove deprecated support to old `config.ru` that use the application class as argument of `run`.
    - Remove deprecated `environment` argument from the rails commands.
    - Remove deprecated `capify!`.
    - Remove deprecated `config.secret_token`.
    - Remove `app/assets` and `app/javascript` from `eager_load_paths` and `autoload_paths`.
    - Deprecate `rake routes` in favor of `rails routes`.
    - Deprecate `rake initializers` in favor of `rails initializers`.
    - Deprecate `rake dev:cache` in favor of `rails dev:cache`.
    - Deprecate `rails notes` subcommands in favor of passing an `annotations` argument to `rails notes`.
    - `rails notes:custom ANNOTATION=custom` is deprecated in favor of using `rails notes -a custom`.
    - `rails notes:optimize` is deprecated in favor of using `rails notes -a OPTIMIZE`.
    - `rails notes:todo` is deprecated in favor of using `rails notes -a TODO`.
    - `rails notes:fixme` is deprecated in favor of using `rails notes -a FIXME`.
    - Deprecate `SOURCE_ANNOTATION_DIRECTORIES` environment variable used by `rails notes` through `Rails::SourceAnnotationExtractor::Annotation` in favor of using `config.annotations.register_directories`.
    - Deprecate `rake notes` in favor of `rails notes`.
    - Deprecate support for using the `HOST` environment variable to specify the server IP. The `BINDING` environment variable should be used instead.
    - Deprecate passing Rack server name as a regular argument to `rails server`.
