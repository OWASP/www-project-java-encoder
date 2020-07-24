---

layout: col-sidebar
title: OWASP Java Encoder
tags: appsec xss encoding escaping defense java
level: 0
type: code

auto-migrated: 1
auto-migrated: 1
auto-migrated: 1

## Welcome

The OWASP Java Encoder is a Java 1.5+ simple-to-use drop-in high-performance encoder class with no dependencies and little baggage. This project will help Java web developers defend against Cross Site Scripting!

Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts (primarily JavaScript) are injected into otherwise trusted web sites. One of the primary defenses to stop Cross Site Scripting is a technique called Contextual Output Encoding. WARNING: Please note that XSS prevention requires other defensive strategies besides encoding! For more information, please read the (Cross Site Scripting prevention cheatsheet)[https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html].

We actively track project issues and seek to remediate any issues that arise. The project owners feel this project is stable and ready for production use and are seeking project status promotion.

Happy Encoding!

## Introduction

Contextual Output Encoding is a computer programming technique necessary to stop Cross Site Scripting. This project is a Java 1.5+ simple-to-use drop-in high-performance encoder class with no dependencies and little baggage. It provides numerous encoding functions to help defend against XSS in a variety of different HTML, JavaScript, XML and CSS contexts.

## Quick Overview

The OWASP Java Encoder library is intended for quick contextual encoding with very little overhead, either in performance or usage. To get started, simply add the encoder-1.2.2.jar, import org.owasp.encoder.Encode and start encoding.

Please look at the javadoc for Encode to see the variety of contexts for which you can encode. Tag libraries and JSP EL functions can be found in the encoder-jsp-1.2.2.jar.

## Licensing
The OWASP Java Encoder is free to use under the New BSD License.

## Downloads 

(encoder-1.2.2.jar)[https://search.maven.org/remotecontent?filepath=org/owasp/encoder/encoder/1.2.2/encoder-1.2.2.jar]
(encoder-jsp-1.2.2.jar)[https://search.maven.org/remotecontent?filepath=org/owasp/encoder/encoder-jsp/1.2.2/encoder-jsp-1.2.2.jar]

## News and Events

* [24 July 2020] GitHub migration complete!
* [14 September 2018] 1.2.2 Released!
* [19 February 2017] 1.2.1 Released!
* [11 June 2016] No reported issues and library use is strong!
* [1 May 2015] Moved to GitHub
* [12 Apr 2015] 1.2 Released!
* [10 Apr 2015] GitHub move
* [1 Feb 2015] Removed ThreadLocal
* [20 Mar 2014] Doc additions
* [5 Feb 2014] New Wiki
* [4 Feb 2014] 1.1.1 Released
---


<!-- Standard Chapter Page Template
This is an example of a Project or Chapter page.
Please change these items to indicate the actual information you wish to present. In addition to this information, the 'front-matter' above the text should be modified to reflect your actual information.  An explanation of each of the front-matter items is below:

{copy for this file (index.md)}
Replace the text above the commented area with your information in the format below:
```
## Welcome
Include some information here about your chapter

## Participation
The Open Web Application Security Project (OWASP) is a nonprofit foundation that works to improve the security of software. All of our projects ,tools, documents, forums, and chapters are free and open to anyone interested in improving application security. 

Chapters are led by local leaders in accordance with the [Chapter Leader Handbook](/www-policy/rules-of-procedure/chapter-handbook). Financial contributions should only be made online using the authorized online donation button. To be a SPEAKER at ANY OWASP Chapter in the world simply review the [speaker agreement](/www-policy/speaker-agreement) and then contact the local chapter leader with details of what OWASP Project, independent research, or related software security topic you would like to present.

Everyone is welcome and encouraged to participate in our [Projects](/projects), [Local Chapters](/chapters), [Events](/events), [Online Groups](https://groups.google.com/a/owasp.com/){:target='_blank'}, and [Community Slack Channel](https://owasp.slack.com/){:target='_blank'}. We especially encourage diversity in all our initiatives. OWASP is a fantastic place to learn about application security, to network, and even to build your reputation as an expert. We also encourage you to be [become a member](/membership) or consider a [donation](/donate) to support our ongoing work.

## Local News
- Meeting Location
- Everyone is welcome to join us at our chapter meetings.

```
{info.md}

This separate file is where you should place links to your Google Group and Meetup page. It will be automatically rendered in the column sidebar.

{leaders.md}

Another separate file that should simply include each leaders name with mailto link as a list. It will also be automatically rendered in the column sidebar.

-->