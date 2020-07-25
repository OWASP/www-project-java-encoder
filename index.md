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

## GitHub

Extensive documentation on how to use this project can be found in our [GitHub repository](https://github.com/OWASP/owasp-java-encoder).

# Use the Java Encoder Project

The general API pattern is to utilize the Java Encoder Project in your
user interface code and wrap all variables added dynamically to HTML
with a proper encoding function. The encoding pattern is
<b>"Encode.forContextName(untrustedData)"</b>, where "ContextName" is
the name of the target context and "untrustedData" is untrusted output.

## Basic HTML Context

	<body>
	<%= <b>Encode.forHtml(UNTRUSTED)</b> %\>
	</body>

## HTML Content Context

	<textarea name="text">
	<%= <b>Encode.forHtmlContent(UNTRUSTED)</b> %\>
	</textarea>

## HTML Attribute context

	<input type="text" name="address" value="<%= Encode.forHtmlAttribute(UNTRUSTED) %>" />

Generally <b>Encode.forHtml(UNTRUSTED)</b> is also safe but slightly
less efficient for the above two contexts (for textarea content and
input value text) since it encodes more characters than necessary but
might be easier for developers to use.

## CSS contexts

	<div style="width:<= Encode.forCssString(UNTRUSTED) %>">

	<div style="background:<= Encode.forCssUrl(UNTRUSTED) %>">

## Javascript Block context

	<script type="text/javascript">
	var msg = "<%= Encode.forJavaScriptBlock(UNTRUSTED) %>";`
	alert(msg);`
	</script>

## Javascript Variable context

	<button
	onclick="alert('<%= Encode.forJavaScriptAttribute(UNTRUSTED) %>');">
	click me</button>

JavaScript Content Notes: <b>Encode.forJavaScript(UNTRUSTED)</b> is safe
for the above two contexts, but encodes more characters and is less
efficient.

## Encode URL parameter values

	<a href="/search?value=<%= Encode.forUriComponent(UNTRUSTED) %>&order=1#top">

## Encode REST URL parameters

	<a href="/page/<%= Encode.forUriComponent(UNTRUSTED) %>">

## Handling a Full Untrusted URL

When handling a full URL with the OWASP Java encoder, first verify the
URL is a legal URL.

	String url = validateURL(untrustedInput);`

Then encode the URL as an HTML attribute when outputting to the page.
Note the linkable text needs to be encoded in a different context.

	<a href="<%= Encode.forHtmlAttribute(untrustedUrl) %>">
	<%= Encode.forHtmlContent(untrustedLinkName) %>
	</a>

## To use in a JSP with EL

	<%@page contentType="text/html" pageEncoding="UTF-8"%>
	<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
	<%@taglib prefix="e" uri="https://www.owasp.org/index.php/OWASP_Java_Encoder_Project" %>

	<html>
	<head>
	<title>
	<b><e:forHtml value="${param.title}" /></b>
	</title>
	</head>
	<body>
	<h1>
	<b>${e:forHtml(param.data)}</b>
	</h1>
	</body>
	</html>

Other contexts can be found in the [org.owasp.Encode class
methods](https://owasp.github.io/owasp-java-encoder/encoder/apidocs/index.html?index-all.html),
including XML contexts and more.

# How To Handle Numbers

Numbers don’t need encoding since they cannot cause XSS. There are no
numbers that will break out of a javascript context. <b>If (and only if)
‘javaNumber’ is a numeric type (primitive or box wrapper), just use:</b>

	var javaScriptNumber = <%= javaNumber %>;

This is true even for the special cases of
java.lang.Double.POSITIVE_INFINITY, NEGATIVE_INFINITY, NaN, and
java.lang.Float equivalents.

On the other hand, if ‘javaNumber’ is some user provided data that is
NOT a numeric type, then you should either (1) convert it to a number on
the java side, or (2) encode it to a string and handle it on the
javascript side. E.g.

	<% // option (1)
	String javaNumber = (untrusted data);
	Double actualNumber = Double.parseDouble(javaNumber); // don’t forget to catch NumberFormatException
	%>

	<script>
	var jsNumber = <%= actualNumber %>;
	</script>

<b>-- OR --</b>

	<% // option (2)
	String javaNumber = (untrusted data);
	%>

	<script>
	var jsNumber = parseInt("<%=Encode.forJavaScript(javaNumber)%>");
	</script>

# Deploy the Java Encoder Project

The OWASP Java Encoder version 1.2.2 is now available in central\!

[OWASP Encoder at Maven
Central](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.owasp.encoder%22).

## Core

Direct Download:
[encoder-1.2.2.jar](http://search.maven.org/remotecontent?filepath=org/owasp/encoder/encoder/1.2.2/encoder-1.2.2.jar)

### Maven

	<dependency>
		<groupId>org.owasp.encoder</groupId>
		<artifactId>encoder</artifactId>
		<version>1.2.2</version>
	</dependency>

## JSP Tag Library

Direct Download:
[encoder-jsp-1.2.2.jar](https://search.maven.org/remotecontent?filepath=org/owasp/encoder/encoder-jsp/1.2.2/encoder-jsp-1.2.2.jar)

### Maven

	<dependency>
		<groupId>org.owasp.encoder</groupId>
		<artifactId>encoder-jsp</artifactId>
		<version>1.2.2</version>
	</dependency>

# Grave Accent Issue

The following describes the Grave Accent XSS issue with unpatched
versions of Internet Explorer. Thank you to <b>Rafay Baloch</b> for
bringing this to our attention and to <b>Jeff Ichnowski</b> for the
workaround.

## Introduction

The grave accent (\`), ASCII 96, hex 60
([wikipedia](http://en.wikipedia.org/wiki/Grave_accent)) is subject to a
critical flaw in unpatched Internet Explorer. There is no possible
encoding of the character that can avoid the issue. For a more in depth
presentation on the issue discussed herein, please see [Mario Heidrech's
presentation](http://www.slideshare.net/x00mario/the-innerhtml-apocalypse).

## Background

In Internet Explorer, the grave accent is usable as an HTML attribute
quotation character, equivalent to single and double quotes.
Specifically, IE treats the following as equivalent:

	<input value="this is the value">
	<input value=`this is the value`>

It is an IE extension, is not in HTML specifications
([HTML4](http://www.w3.org/TR/REC-html40/intro/sgmltut.html#h-3.2.2),
[HTML5](http://www.w3.org/TR/html5/syntax.html#attributes-0)), and is
probably not well supported in other browsers.

## The Issue

The following HTML snippet, demonstrates the cross-site scripting
vulnerability related to grave accents on unpatched Internet Explorer:

	<div id=a>
	<input value="``onmouseover=alert(1)">
	</div>

	<div id=b>
	</div>

	<script>
	b.innerHTML=a.innerHTML
	</script>

When this snippet is run in Internet Explorer the following steps
happen:

1.  Two div elements are created with id's "a" and "b"
2.  The script executes "a.innerHTML" which returns:

	<input value=``onmouseover=alert(1)>

3.  The script sets "b.innerHTML" to the value from (2) and is converted
    to the DOM equivalent of

	<input value="" onmouseover="alert(1)">

The XSS issue arises from IE returning a value from innerHTML that it
does not parse back into the original DOM. Patched version of IE fix
this issue by returning the XSS value as a double-quoted attribute. The
issue is complicated by the fact that no possible encoding of the grave
accent can avoid this issue.

When...

	<input value="``onmouseover=alert(1)">

...is the input, "a.innerHTML" returns the same XSS vector as it does
without the encoding.

## Recommend Solution

Our recommended workaround is to update any JavaScript based innerHTML
read to replace the accent grave with a numeric entity encoded form:
"\`". As an example, the following change to the XSS vulnerable code
above fixes the issue:

	<script>
	a.innerHTML=b.innerHTML.replace(/\`/g, "\`");
	</script>

This can be done in any library code that reads the innerHTML. To follow
how this addresses the issue, the innerHTML from step 2 of the issue is
converted to:

	<input value=&#96;&#96;onmouseover=alert(1)>

Since the browser will no longer see the grave accents as an empty
attribute, it will convert the input back to a copy of its original DOM.

## Other Possible Solutions

As there is no encoding option available, the following options are
available to web application authors:

1.  Do not use innerHTML copies
2.  Filter out the accent grave from any user input
3.  Clean up grave accents when using an innerHTML copy

## OWASP Java Encoder Library Related Changes

The OWASP Java Encoder Library at its core is intended to be a XSS safe
_encoding_ library. The grave accent is a legitimate and frequently
used character, that cannot be encoded to avoid this bug in unpatched
versions of IE. With enough user feedback, we may update the library to
include one of the following options: (1) alternate, drop-in build that
filters grave accents, with unchanged API, (2) new filtering methods.

# Encoding and Template Literals

Several users of the Java Encoder have asked how to properly use the
OWASP Java Encoder in combination with template literals.

The best way to encode template literal variables is to first escape the
untrusted data in a JavaScript variable and then place that variable in
the template literal.

	var user = "<%= Encode.forJavaScript(user) %>";
	Hello ${user}, here is your total: ${total}

Another method is to properly escape the variable in-line.

		${"<%= Encode.forJavaScript(user) $>"}, here is your total ${total}


## News and Events

* [24 July 2020] GitHub migration complete!!!
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