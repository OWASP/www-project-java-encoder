---
title: Accent
displaytext: Grave Accent
layout:  null
tab: true
order: 4
tags: java-encoder-tag
---

## Grave Accent Issue

The following describes the Grave Accent XSS issue with unpatched versions of Internet Explorer. Thank you to <b>Rafay Baloch</b> for bringing this to our attention and to <b>Jeff Ichnowski</b> for the workaround.

### Introduction
The grave accent (\`), ASCII 96, hex 60 ([wikipedia](http://en.wikipedia.org/wiki/Grave_accent)) is subject to a  critical flaw in unpatched Internet Explorer. There is no possible encoding of the character that can avoid the issue. For a more in depth presentation on the issue discussed herein, please see [Mario Heidrech's presentation](http://www.slideshare.net/x00mario/the-innerhtml-apocalypse).

### Background

In Internet Explorer, the grave accent is usable as an HTML attribute quotation character, equivalent to single and double quotes. 
Specifically, IE treats the following as equivalent:

	<input value="this is the value">
	<input value=`this is the value`>

It is an IE extension, is not in HTML specifications
([HTML4](http://www.w3.org/TR/REC-html40/intro/sgmltut.html#h-3.2.2),
[HTML5](http://www.w3.org/TR/html5/syntax.html#attributes-0)), and is probably not well supported in other browsers.

### The Issue

The following HTML snippet, demonstrates the cross-site scripting vulnerability related to grave accents on unpatched Internet Explorer:

	<div id=a>
	<input value="``onmouseover=alert(1)">
	</div>

	<div id=b>
	</div>

	<script>
	b.innerHTML=a.innerHTML
	</script>

When this snippet is run in Internet Explorer the following steps happen:

1.  Two div elements are created with id's "a" and "b"
2.  The script executes "a.innerHTML" which returns:

	<input value=``onmouseover=alert(1)>

3.  The script sets "b.innerHTML" to the value from (2) and is converted to the DOM equivalent of

	<input value="" onmouseover="alert(1)">

The XSS issue arises from IE returning a value from innerHTML that it does not parse back into the original DOM. Patched version of IE fix this issue by returning the XSS value as a double-quoted attribute. The issue is complicated by the fact that no possible encoding of the grave accent can avoid this issue.

When...

	<input value="``onmouseover=alert(1)">

...is the input, "a.innerHTML" returns the same XSS vector as it does without the encoding.

### Recommend Solution

Our recommended workaround is to update any JavaScript based innerHTML read to replace the accent grave with a numeric entity encoded form: "\`". 
As an example, the following change to the XSS vulnerable code above fixes the issue:

	<script>
	a.innerHTML=b.innerHTML.replace(/\`/g, "\`");
	</script>

This can be done in any library code that reads the innerHTML. To follow how this addresses the issue, the innerHTML from step 2 of the issue is converted to:

	<input value=&#96;&#96;onmouseover=alert(1)>

Since the browser will no longer see the grave accents as an empty attribute, it will convert the input back to a copy of its original DOM.

### Other Possible Solutions

As there is no encoding option available, the following options are available to web application authors:

1.  Do not use innerHTML copies
2.  Filter out the accent grave from any user input
3.  Clean up grave accents when using an innerHTML copy

### OWASP Java Encoder Library Related Changes

The OWASP Java Encoder Library at its core is intended to be a XSS safe
_encoding_ library. The grave accent is a legitimate and frequently
used character, that cannot be encoded to avoid this bug in unpatched
versions of IE. With enough user feedback, we may update the library to
include one of the following options: (1) alternate, drop-in build that
filters grave accents, with unchanged API, (2) new filtering methods.