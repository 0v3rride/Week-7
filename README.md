# Project 7 - WordPress Pentesting

Time spent: 5 hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

### 1. User Enumeration <= 4.7.1 (CVE-2017-5487)
  - [+] Summary: 
    - Vulnerability types: User Enumeration
    - Tested in version: 4.2
    - Fixed in version: 4.7.2
  - [+] GIF Walkthrough: ![User Enumeration]()
  - [+] Steps to recreate: 
    - Create new user(s).
    - Enter a known username such as admin or moderator in my case followed by an invalid password for that account.
    - Detailed error message appears letting a user or attacker know that there is infact an account named admin, moderator, etc.
  - [+] Affected source code:
    - [CVE-2017-5487](https://github.com/WordPress/WordPress/commit/daf358983cc1ce0c77bf6d2de2ebbb43df2add60)
2. Persistent XSS as an authenticated user (variation of CVE-2015-3440)
  - [+] Summary: 
    - Vulnerability types: Persistent XSS
    - Tested in version: 4.2
    - Fixed in version: Unknown
  - [+] GIF Walkthrough: [Persistent XSS as an authenticated user (variation of CVE-2015-3440)]()
  - [+] Steps to recreate: 
    - Created a new account with editor privileges named moderator which was used for the user enumeration walkthrough.
    - Logged into moderator and navigated to the "Example front page" post.
    - Entered the following code into the `<a href=" onmouseover=alert(unescape(/xss/.source)) {enter more data here to make the overall length of the comment 64kb(65536 bytes/characters) long or greater}"`
    - Note that there is no closing bracket for the opening anchor tag nor is there a closing anchor tag.
  - [+] Affected source code:
    - [Klikki's exploit code](https://klikki.fi/adv/wordpress2.html)
      - [Exploit-db 36844](https://www.exploit-db.com/exploits/36844/)
3. Persistent XSS exploit commenting as an unauthenticated user
  - [+] Summary: 
    - Vulnerability types: Persistent XSS
    - Tested in version: 4.0
    - Fixed in version: 4.2.1
  - [+] GIF Walkthrough: [Persistent XSS as an unauthenticated user]()
  - [+] Steps to recreate:
    - An affected wordpress site must allow strangers or unregistered users to comment on posts and pages.
    - Enter the following source code in a comment box as unauthenticated user
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
4. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
5. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

## Assets

List any additional assets, such as scripts or files

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
