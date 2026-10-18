---
title: Deploy
layout:  null
tab: true
order: 6
tags: java-encoder-tag
---

## How to Deploy the Java Encoder

The OWASP Java Encoder version 1.6.0 is available from Maven Central.

[OWASP Encoder at MavenCentral](https://central.sonatype.com/namespace/org.owasp.encoder).

### Core
Direct Download:
[encoder-1.6.0.jar](https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder/1.6.0/encoder-1.6.0.jar)

#### Maven

	<dependency>
		<groupId>org.owasp.encoder</groupId>
		<artifactId>encoder</artifactId>
		<version>1.6.0</version>
	</dependency>

### Jakarta JSP Tag Library

Direct Download:
[encoder-jakarta-jsp-1.6.0.jar](https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jakarta-jsp/1.6.0/encoder-jakarta-jsp-1.6.0.jar)

#### Maven

	<dependency>
		<groupId>org.owasp.encoder</groupId>
		<artifactId>encoder-jakarta-jsp</artifactId>
		<version>1.6.0</version>
	</dependency>

### JSP Tag Library

Direct Download:
[encoder-jsp-1.6.0.jar](https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jsp/1.6.0/encoder-jsp-1.6.0.jar)

#### Maven

	<dependency>
		<groupId>org.owasp.encoder</groupId>
		<artifactId>encoder-jsp</artifactId>
		<version>1.6.0</version>
	</dependency>

Use only one JSP adapter: javax and Jakarta adapters share packages and must not be combined. The ESAPI adapter is retired and is not included in 1.6.0.
