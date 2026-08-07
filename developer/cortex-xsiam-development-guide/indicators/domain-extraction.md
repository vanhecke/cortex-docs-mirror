---
description: >-
  Extract a domain indicator from text that is recognized from a regular
  expression and then formatted with a formatting script.
---

# Domain extraction

The Cortex XSIAM domain indicator type is built using regular expression and a formatting script. The following describes the domain extraction components and what output you should expect when extracting indicators of type domain.

#### Domain extraction components

There are two components when extracting domain indicators:

* Regular expression
* Formatting script

#### Regular expression

When text is given, a domain regular expression will try to catch a valid domain based on the following characteristics:

* A domain with ASCII and non-ASCII characters
* Escaped and unescaped domains

The regular expression can extract domains from one of the following:

* Explicit domain
* URL
* Email address

#### Formatting script

After extracting the domain using a regular expression, an `ExtractDomainAndFQDNFromUrlAndEmail` formatting script iterates on each given domain and does the following:

1.  Replaces "\[.]" with ".".

    For example:

    `www[.]example.com --&gt; www.example.com`
2.  Validate the Top-Level-Domain to avoid file extension false positives.

    Excludes ‘.zip’ Top-Level-Domain by default.
3. Returns the formatted domain.

#### Common domain structures

* `example.com`
* `www.example.com`
* `xn--t1e2s3t4.com`
* `www.xn--t1e2s3t4.com`
* `www.example.co.uk`
* `example.co.uk`
* `subtest.example.com`
* `www.example.example.com`
* `öexample.com`
* `exampleö.com`
* `www.exampleö.com`
* `www.examöle.com`

For more information, see [Indicator extraction]().
