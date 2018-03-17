# Project 7 - WordPress Pentesting

Time spent: 5 hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

## 1. User Enumeration <= 4.7.1 (CVE-2017-5487)
 - Summary: 
    - Vulnerability types: User Enumeration
    - Tested in version: 4.2
    - Fixed in version: 4.7.2
  - GIF Walkthrough: ![User Enumeration]()
  - Steps to recreate: 
    - Create new user(s).
    - Enter a known username such as admin or moderator in my case followed by an invalid password for that account.
    - Detailed error message appears letting a user or attacker know that there is infact an account named admin, moderator, etc.
  - Affected source code:
    - [WordPress Github](https://github.com/WordPress/WordPress/commit/daf358983cc1ce0c77bf6d2de2ebbb43df2add60)
## 2. Persistent XSS as an authenticated user (variation of CVE-2015-3440)
  - Summary: 
    - Vulnerability types: Persistent XSS
    - Tested in version: 4.2
    - Fixed in version: Unknown
  - GIF Walkthrough: [Authenticated Persistent XSS]()
  - Steps to recreate: 
    - Created a new account with editor privileges named moderator which was used for the user enumeration walkthrough.
    - Logged into moderator and navigated to the "Example front page" post.
    - Generated 65563 random bytes by issuing the following command in the terminal of Kali Linux: `/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 65536`
    - Entered the following code into the `<a href=" onmouseover=alert(unescape(/xss/.source)) {enter more data here to make the overall length of the comment 64kb(65536 bytes/characters) long or greater}"`
    - Note that there is no closing bracket for the opening anchor tag nor is there a closing anchor tag.
  -  Affected source code:
    - [Klikki's exploit code](https://klikki.fi/adv/wordpress2.html)
      - [Exploit-db 36844](https://www.exploit-db.com/exploits/36844/)
## 3. Persistent XSS exploit commenting as an unauthenticated user (CVE-2015-3440)
  - Summary: 
    - Vulnerability types: Persistent XSS
    - Tested in version: 4.0
    - Fixed in version: 4.2.1
  - GIF Walkthrough: [Unauthenticated Persistent XSS]()
  - Steps to recreate:
    - An affected wordpress site must allow strangers or unregistered users to comment on posts and pages.
    - Generated 65563 random bytes by issuing the following command in the terminal of Kali Linux: `/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 65536 -s A`
    - Enter the following source code in a comment box as an unauthenticated user `<a title='x onmouseover=alert(unescape(/xss/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64kb or 65563 bytes/characters]..AAA'></a>`
  - Affected source code:
    - [Klikki's exploit code](https://klikki.fi/adv/wordpress2.html)
      - [Exploit-db 36844](https://www.exploit-db.com/exploits/36844/)
## 4. 
  - Summary: Cross-Site Scripting (XSS)
    - Vulnerability types: Cross-Site Scripting (XSS)
    - Tested in version: 4.0
    - Fixed in version: 4.6
  - GIF Walkthrough: [Cross-Site Scripting]()
  - Steps to recreate:
    - Comment on a post (authenticated or unauthenticated).
    - Enter the following JS code: `<script>alert(document.cookie)</script>`
  - Affected source code:
    - [WordPress GitHub](https://github.com/WordPress/WordPress/commit/c9e60dab176635d4bfaaf431c0ea891e4726d6e0)
## 5. Large file upload error XSS
  - Summary: 
    - Vulnerability types: XSS (non-persistent) (CVE-2017-9061)
    - Tested in version: 4.7
    - Fixed in version: 4.7.5
  - GIF Walkthrough: [Large file upload error XSS]()
  - Steps to recreate:
    - This must be done in Linux and you must be authenticated.
    - Create a .png file that is 20MB in size using the command `fallocate -l 20M bad_file.png` one can also use
the dd command `dd if=/dev/<zero|urandom> of=~/Desktop/bad_file.txt bs=2048 count=10` or another command that fulfills this requirement.
    - Rename the file to `Some random name<img src=x onerror=alert(1)>.png`.
    - Upload the file via the add new media option and dragging the file you made into the drop the area as the admin.
  - Affected source code:
    - [Hackerone](https://hackerone.com/reports/203515)
    - [CVE Details](https://www.cvedetails.com/cve/CVE-2017-9061/) 
    - [NIST NVD](https://nvd.nist.gov/vuln/detail/CVE-2017-9061) 
    - [WordPress Github](https://github.com/WordPress/WordPress/commit/8c7ea71edbbffca5d9766b7bea7c7f3722ffafa6)
## Assets

Exploit 2 & 3:
```
<a title='x onmouseover=alert(unescape(/xss/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64kb or 65563 bytes/characters]..AAA'></a>
```
http://klikki.fi/adv/wordpress2.html

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Using vagrant to setup wpdistillery was fairly easy to do once I got acquainted with the process. I couldn't really find anything pertaining to what I specifically did for exploit 2 (Persistent XSS as an authenticated user (variation of CVE-2015-3440)). I discovered it by playing around with it and trying different permuations of the exploit code by Klikki which eventually led to the XSS exploit. I also came across an interesting exploit (WordPress < 4.7.4 - Unauthorized Password Reset - https://www.exploit-db.com/exploits/41963/). However, from my understanding this would require me to setup my own temporary domain along with a publicly routable email server which I don't have enough insight for, but nevertheless the PoC was interesting to read about. 

## License

    Copyright [2018] [Override]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
