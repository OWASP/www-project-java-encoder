---

layout: col-sidebar
title: OWASP Java Encoder
tags: java-encoder-tag
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

