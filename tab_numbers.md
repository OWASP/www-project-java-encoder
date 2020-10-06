---
title: Numbers
displaytext: Numbers
layout:  null
tab: true
order: 3
tags: java-encoder-tag
---

## How to Handle Numbers

Numbers don’t need encoding since they cannot cause XSS. There are no numbers that will break out of a javascript context.

<b>If (and only if) ‘javaNumber’ is a numeric type (primitive or box wrapper), just use:</b>
```javascript
	var javaScriptNumber = <%= javaNumber %>;
```
This is true even for the special cases of java.lang.Double.POSITIVE_INFINITY, NEGATIVE_INFINITY, NaN, and java.lang.Float equivalents.

On the other hand, if ‘javaNumber’ is some user provided data that is NOT a numeric type, then you should either (see option 1) convert it to a number on the java side, or (option 2) encode it to a string and handle it on the javascript side. E.g.

### Option 1
```java
<% 
	String javaNumber = (untrusted data);
	Double actualNumber = Double.parseDouble(javaNumber); //remember to catch NumberFormatException
%>
```

```javascript
<script>
	var jsNumber = <%= actualNumber %>;
</script>
```
### Option 2

```java
<% 
	String javaNumber = (untrusted data);
%>
```
```javascript
<script>
	var jsNumber = parseInt("<%=Encode.forJavaScript(javaNumber)%>");
</script>
```