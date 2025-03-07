+++
date = '2025-02-06T13:01:30+08:00'
draft = false
title = 'Snyk Cli Test'
read_more_copy= '閱讀更多...'
+++

安裝 Snyk CLI: https://docs.snyk.io/snyk-cli
![](/images/screenshot_20250206131633.png)

<!--more-->

做一次 scan dependencies:

```shell
linh git:(develop) ✗ snyk test

Testing /Users/fbukevin/Desktop/SanityRover/VNProject/linh...

Tested 93 dependencies for known issues, found 7 issues, 378 vulnerable paths.


Issues to fix by upgrading:

  Upgrade rails@7.2.2 to rails@7.2.2.1 to fix
  ✗ Cross-site Scripting (XSS) [Low Severity][https://security.snyk.io/vuln/SNYK-RUBY-ACTIONPACK-8496389] in actionpack@7.2.2
    introduced by importmap-rails@2.0.3 > actionpack@7.2.2 and 18 other path(s)


Issues with no direct upgrade or patch:
  ✗ Cross-site Scripting (XSS) [Low Severity][https://security.snyk.io/vuln/SNYK-RUBY-NOKOGIRI-8453714] in nokogiri@1.16.7-x86_64-linux
    introduced by capybara@3.40.0 > nokogiri@1.16.7-x86_64-linux and 148 other path(s)
  This issue was fixed in versions: 1.15.7, 1.16.8
  ✗ Cross-site Scripting (XSS) [Low Severity][https://security.snyk.io/vuln/SNYK-RUBY-RAILSHTMLSANITIZER-8447886] in rails-html-sanitizer@1.6.0
    introduced by jbuilder@2.13.0 > actionview@7.2.2 > rails-html-sanitizer@1.6.0 and 41 other path(s)
  This issue was fixed in versions: 1.6.1
  ✗ Cross-site Scripting (XSS) [Low Severity][https://security.snyk.io/vuln/SNYK-RUBY-RAILSHTMLSANITIZER-8448218] in rails-html-sanitizer@1.6.0
    introduced by jbuilder@2.13.0 > actionview@7.2.2 > rails-html-sanitizer@1.6.0 and 41 other path(s)
  This issue was fixed in versions: 1.6.1
  ✗ Cross-site Scripting (XSS) [Low Severity][https://security.snyk.io/vuln/SNYK-RUBY-RAILSHTMLSANITIZER-8448407] in rails-html-sanitizer@1.6.0
    introduced by jbuilder@2.13.0 > actionview@7.2.2 > rails-html-sanitizer@1.6.0 and 41 other path(s)
  This issue was fixed in versions: 1.6.1
  ✗ Cross-site Scripting (XSS) [Low Severity][https://security.snyk.io/vuln/SNYK-RUBY-RAILSHTMLSANITIZER-8448516] in rails-html-sanitizer@1.6.0
    introduced by jbuilder@2.13.0 > actionview@7.2.2 > rails-html-sanitizer@1.6.0 and 41 other path(s)
  This issue was fixed in versions: 1.6.1
  ✗ Cross-site Scripting (XSS) [Low Severity][https://security.snyk.io/vuln/SNYK-RUBY-RAILSHTMLSANITIZER-8454495] in rails-html-sanitizer@1.6.0
    introduced by jbuilder@2.13.0 > actionview@7.2.2 > rails-html-sanitizer@1.6.0 and 41 other path(s)
  This issue was fixed in versions: 1.6.1



Organization:      fbukevin-FPhSMNT7C9DhHAcUYLkoSx
Package manager:   rubygems
Target file:       Gemfile
Project name:      linh
Open source:       no
Project path:      /Users/fbukevin/Desktop/SanityRover/VNProject/linh
Licenses:          enabled

Tip: Detected multiple supported manifests (1), use --all-projects to scan all of them at once.
```

![](/images/screenshot_20250206132040.png)
![](/images/screenshot_20250206132047.png)
![](/images/screenshot_20250206132114.png)
![](/images/screenshot_20250206132144.png)
