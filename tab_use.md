---
title: Use
displaytext: How to Use
layout:  null
tab: true
order: 2
tags: java-encoder-tag
---

## How to Use the OWASP Java Encoder

The general API pattern is to utilize the Java Encoder Project in your
user interface code and wrap all variables added dynamically to HTML
with a proper encoding function. The encoding pattern is
<b>"Encode.forContextName(untrustedData)"</b>, where "ContextName" is
the name of the target context and "untrustedData" is untrusted output.

### Basic HTML Context
```java
<body>
	<b><%= Encode.forHtml(UNTRUSTED) %></b>
</body>
```

### HTML Content Context
```java
<textarea name="text">
    <b><%= Encode.forHtmlContent(UNTRUSTED) %></b>
</textarea>
```

### HTML Attribute context
```java
	<input type="text" name="address" value="<%= Encode.forHtmlAttribute(UNTRUSTED) %>" />
```
Generally <b>Encode.forHtml(UNTRUSTED)</b> is also safe but slightly
less efficient for the above two contexts (for textarea content and
input value text) since it encodes more characters than necessary but
might be easier for developers to use.

### Encode URL parameter values
```java
	<a href="/search?value=<%= Encode.forUriComponent(UNTRUSTED) %>&order=1#top">
```

### Encode REST URL parameters
```java
	<a href="/page/<%= Encode.forUriComponent(UNTRUSTED) %>">
```

### Handling a Full Untrusted URL

When handling a full URL with the OWASP Java encoder, first validate to ensure the URL is in the format of a legal URL.
```java
	String url = validateURL(untrustedInput);
```

Then encode the URL as an HTML attribute when outputting to the page.
Note the linkable text needs to be encoded in a different context.
```java
	<a href="<%= Encode.forHtmlAttribute(untrustedUrl) %>">
	    <%= Encode.forHtmlContent(untrustedLinkName) %>
	</a>
```

### Javascript Block context
```javascript
<script type="text/javascript">
	var msg = "<%= Encode.forJavaScriptBlock(UNTRUSTED) %>";
	alert(msg);
</script>
```

### Javascript Variable context
```java
<button onclick="alert('<%= Encode.forJavaScriptAttribute(UNTRUSTED) %>');">
	click me
   </button>
```

JavaScript Content Notes: <b>Encode.forJavaScript(UNTRUSTED)</b> is safe for the above two contexts, but encodes more characters and is less efficient.

### CSS contexts
```java
	<div style="width:<= Encode.forCssString(UNTRUSTED) %>">
	<div style="background:<= Encode.forCssUrl(UNTRUSTED) %>">
```

### To use in a JSP with EL

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
