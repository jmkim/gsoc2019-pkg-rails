# A Rails 6 package transition in Debian

GSoC 2019 First evaluation report by Jongmin Kim

## Project information
  - Project page: [A Rails 6 package transition in Debian](https://summerofcode.withgoogle.com/projects/#6363542624665600)
  - Organisation: [Ruby](https://summerofcode.withgoogle.com/organizations/5542255322988544/)
  - Project proposal (final): [proposal-final.pdf](https://github.com/jmkim/gsoc2019-pkg-rails/blob/gsoc2019/proposal/proposal-final.pdf)

## First evaluation report
**I packaged 22 packages during these weeks, and 11 packages are uploaded into Debian archive.**
I'm going to send 2 more RFS (`image-processing` and `ruby-webpacker`), then 13 packages.

**These weeks, I learned a lot.**
I learned how the Ruby package build process is works, by inspecting the [dh_ruby sources](https://salsa.debian.org/ruby-team/gem2deb).
I learned how the Ruby tests are working, by fixing the tests.
I learned how to convert whole Rakefile from Makefile, by writing with opening two -akefiles side-by-side. :D
Away from Ruby things, I learned the Debian processes ([New Member](https://www.debian.org/devel/join/newmaint), [ITS](https://wiki.debian.org/PackageSalvaging), ...), [how to write manpage](https://manpages.debian.org/unstable/gem2deb/dh_ruby.1.en.html), about [UMEGAYA](https://wiki.debian.org/UpstreamMetadata), and more and more.

**Also, I met a people.**
I joined and worked with some private Ruby packaging team (GitLab and Diaspora) during community bonding period.
In there, I could work with some Ruby team members: Praveen, Utkarsh, and Manas.

Praveen and Utkarsh gave me some work to make me familiar with both Ruby and "package transitioning work".
I did them for two weeks, and thankfully, Praveen asked me and advocated me to become a Debian Maintainer.

With Manas, I tested [GitLab](https://salsa.debian.org/ruby-team/gitlab) and [gitlab-pages](https://salsa.debian.org/Manas-kashyap-guest/gitlab-pages) for inspecting the bugs. I could take a time to understand how the GitLab and Diaspora works in Debian, by installing and debugging them.

**However, my work is 3 weeks behind from the proposed timeline.**
After CBP week 2, I stopped working on those teams, and focused only on my project.

I broke my works into [4 phases](https://wiki.debian.org/Teams/Ruby/Rails6).  
The main part of this project is Phase 3, but not yet started.
I need to estimate the Phase 3 timeline carefully by do transition some packages. :(

From week 1 to week 2, I took too much time for `ruby-redis` failure.
During week 3, I took too much time for investigating `ruby-bootsnap` cache path issue.
Now (week 4), I wrapped up the Phase 1, started Phase 2, and fixing the Rails tests.

With a week debugging, almost of Rails tests are fixed.
The remaining things are all related to Webpacker.
I'm going to wrap up the Phase 2 as soon as possible, this week or next.
And then, I'll start Phase 3, with re-estimate whole the timelines by checking the level of works.

## Quantitative self-assessment
  * Simply calculated from weekly reports
  * Timeline
      + Proposed timeline
          - Phase 1 and 2: May 7 ~ May 25 (19 days)
          - Phase 3: May 26 ~ August 17 (85 days)
      + Actual timeline
          - Phase 1: May 6 ~ June 18 (44 days)
          - Phase 2: June 18 ~
          - Phase 3: Not started
          - Phase 4: Not started
      + 25 days behind from timeline.
  * Learned
      + 15 things learned (1 thing per 3 days)
  * Worked
      + 22 packages modified (1 package per 2 days)
  * Reported to upstream
      + 3 reported (2 issues and 1 PR)
  * Patches
      + 13 patches made (3 patches per 1 day)
  * Uploaded packages
      + 11 packages uploaded to Debian archive (1 package per 4 days)

## Weekly reports
  * [Community Bonding Week 1](./weekly-report/cbp-week-1.md)
  * [Community Bonding Week 2](./weekly-report/cbp-week-2.md)
  * [Community Bonding Week 3](./weekly-report/cbp-week-3.md)
  * [Week 1](./weekly-report/week-1.md)
  * [Week 2](./weekly-report/week-2.md)
  * [Week 3](./weekly-report/week-3.md)
  * [Week 4](./weekly-report/week-4.md)
