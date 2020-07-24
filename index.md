---

layout: col-sidebar
title: OWASP Java Encoder
tags: appsec xss encoding escaping defense java
level: 0
type: code

---

## Welcome

The OWASP Java Encoder is a Java 1.5+ simple-to-use drop-in high-performance encoder class with no dependencies and little baggage. This project will help Java web developers defend against Cross Site Scripting!

Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts (primarily JavaScript) are injected into otherwise trusted web sites. One of the primary defenses to stop Cross Site Scripting is a technique called Contextual Output Encoding. WARNING: Please note that XSS prevention requires other defensive strategies besides encoding! For more information, please read the [Cross Site Scripting prevention cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html).

We actively track project issues and seek to remediate any issues that arise. The project owners feel this project is stable and ready for production use and are seeking project status promotion.

Happy Encoding!

## Getting Started

The OWASP Java Encoder library is intended for quick contextual encoding with very little overhead, either in performance or usage. To get started, simply add the encoder-1.2.2.jar, import org.owasp.encoder.Encode and start encoding.

Please look at the javadoc for Encode to see the variety of contexts for which you can encode. Tag libraries and JSP EL functions can be found in the encoder-jsp-1.2.2.jar.

## Licensing
The OWASP Java Encoder is free to use under the New BSD License.

## Downloads 

* [encoder-1.2.2.jar](https://search.maven.org/remotecontent?filepath=org/owasp/encoder/encoder/1.2.2/encoder-1.2.2.jar)
* [encoder-jsp-1.2.2.jar](https://search.maven.org/remotecontent?filepath=org/owasp/encoder/encoder-jsp/1.2.2/encoder-jsp-1.2.2.jar)

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


<!--

```
{info.md}

This separate file is where you should place links to your Google Group and Meetup page. It will be automatically rendered in the column sidebar.

{leaders.md}

Another separate file that should simply include each leaders name with mailto link as a list. It will also be automatically rendered in the column sidebar.

-->