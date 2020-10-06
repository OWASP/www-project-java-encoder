---
title: Templates
displaytext: Template Literals
layout:  null
tab: true
order: 5
tags: java-encoder-tag
---


## Encoding and Template Literals

Several users of the Java Encoder have asked how to properly use the OWASP Java Encoder in combination with template literals.

The best way to encode template literal variables is to first escape the
untrusted data in a JavaScript variable and then place that variable in
the template literal.

	var user = "<%= Encode.forJavaScript(user) %>";
	Hello ${user}, here is your total: ${total}

Another method is to properly escape the variable in-line.

	${"<%= Encode.forJavaScript(user) $>"}, here is your total ${total}

