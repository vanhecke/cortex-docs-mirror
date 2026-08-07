# CONST

{% hint style="warning" %}
### Prerequisite

Parsing Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Data Model Rules, and Event Forwarding.
{% endhint %}

A `CONST` section is used to define strings and numbers that can be reused multiple times within Cortex Query Language (XQL) statements in other `INGEST` sections by using `$constName`. This can be helpful to avoid writing the same value in multiple sections, similar to constants in modern programming languages.

```programlisting
[CONST]
DEFAULT_DEVICE_NAME = "firewall3060";       // string
FILE_REGEX = "c:\\users\\[a-zA-Z0-9.]*";    // complex string
my_num = 3;                                 /* int */
```

An example of using a `CONST` inside XQL statements in other `INGEST` sections using `$constName`:

{% hint style="info" %}
### Note

The dollar sign (`$`) must be adjacent to the `[CONST]` name, without any whitespace in between.
{% endhint %}

```programlisting
...
| filter device_name = $DEFAULT_DEVICE_NAME
| alter new_field = JSON_EXTRACT(field, $FILE_REGEX)
| filter age < $MAX_TIMEOUT
| join type=$DEFAULT_JOIN_TYPE conflict_strategy=$DEFAULT_JOIN_CONFLICT_STRATEGY (dataset=my_lookup) as inn url=inn.url
...
```

{% hint style="info" %}
### Important

Only quoted or integer terminal values are considered valid for `CONST` sections.
{% endhint %}

These will not compile:

```programlisting
[CONST]
WORD_CONST = abcde;                             //invalid
func_val = regex_extract(_raw_log, "regex");    // not possible
RECURSIVE_CONST = $WORD_CONST;                  // not terminal - not possible
```

`CONST` sections are meant to replace values. Other types, such as column names, are not supported:

```programlisting
...
| filter $DEVICE_NAME = "my_device"             // illegal
...
```

A few more points to keep in mind when writing `CONST` sections:

* `CONST` names are not case-sensitive. They can be written in any user-desired casing, such as UPPER\_SNAKE, lower\_snake, camelCase, and CamelCase. For example, `MY_CONST=My_Const=my_const`.
* `CONST` names must be unique inside a section, and across all sections of the file. You cannot have the same `CONST` name defined again in the same section, or in any other `CONST` sections in the file.
* Since section order is unimportant, you do not have to declare a `CONST` before using it. You can have the `CONST` section written below other sections that use those `CONST` sections.
* A `CONST` is an add-on to the Parsing Rule syntax and is optional to configure.
* `CONST` syntax is derived from XQL, but a few modifications as explained in the [Parsing Rules file structure and syntax]().
