---
description: >-
  Learn more about how Cortex XSIAM treats JSON functions in the Cortex Query
  Language.
---

# JSON functions

The Cortex Query Language (XQL) includes a number of JSON functions. Before using any of these functions, it's important to understand how Cortex XSIAM treats a JSON so you can accurately formulate your queries using the correct syntax.

{% hint style="info" %}
### Important

JSON field names are case sensitive, so the key to field pairing must be identical in an XQL query for results to be found. For example, if a field value is `"TIMESTAMP"` and your query is defined to look for "timestamp", no results will be found.
{% endhint %}

<details>

<summary>&#x3C;json_path></summary>

Each JSON function includes defining a `<json_path>` in both the regular syntax and when using the syntatic sugar format. The `<json_path>` argument identifies the data of the JSON object you want to extract using dot-notation. When using the regular syntax, the beginning of the object is represented by a `$`. This `$` is not required when using the syntatic sugar format.

Example

If you have the following object:

```programlisting
{
  "a_field" : "This is a_field value",
  "b_field" : {
                 "c_field" : "This is c_field value"
              }
}
```

Then the path using the regular syntax:

```programlisting
$.a_field
```

Returns `"This is a_field value"`, while the path using the regular syntax:

```programlisting
$.b_field.c_field
```

Returns `"This is c_field value"`.

</details>

<details>

<summary>Field in &#x3C;json_path> contains characters</summary>

#### In the regular syntax

When using the regular syntax to write your XQL queries and a field in the `<json_path>` contains characters, such as a dot (.) or colon (:), the syntax needs to be tweaked slightly to account for the `<json_field>`.

For example, when using the `json_extract` function, the previous regular syntax would need to be changed to an updated syntax to account for the field in the `<json_path>` containing characters.

Previous regular syntax for the `json_extract` function:

```programlisting
json_extract(<json_object_formatted_string>, <json_path>)
```

Updated regular syntax for the `json_extract` function, where the `<json_field>` now includes single quotation marks as `'<json_field>'`:

```programlisting
json_extract(<json_object_formatted_string>, "['<json_field>']")
```

For each JSON function, the regular syntax can change slightly, but the `"['<json_field>']"` format is the same. The `"['<json_field>']"` identifies the data you want to extract using dot-notation, where the data extracted is dependent on your syntax.

Example

If you have the following JSON object defined:

```programlisting
{"a.b": 
    {"inn": 
        {"one":1}
    }
}
```

To extract the data `{"one":1}`, the `"['<json_field>']"` would need to be defined as `"$['a.b'].inn"` for all JSON functions. For example, when using the `json_extract` function, the regular syntax is:

```programlisting
json_extract(field_json_1, "$['a.b'].inn")
```

To extract the data `{"inn": {"one":1}}`, the `"['<json_field>']"` would need to be defined as `"$['a.b']"` for all JSON functions. For example, when using the `json_extract` function, the regular syntax is:

```programlisting
json_extract(field_json_1, "$['a.b']")
```

Example

If you have the following JSON object defined:

```programlisting
{"a.b": 
    {"inn.inn": 
        {"one":1}
    }
}
```

To extract the data `{"one":1}`, the `"['<json_field>']"` would need to be defined as `"$['a.b']['inn.inn']"` for all JSON functions. For example, when using the `json_extract` function, the regular syntax is:

```programlisting
json_extract(json_field, "$['a.b']['inn.inn']")
```

#### In the syntatic sugar format

To make it easier for you to write your XQL queries, each JSON function includes an optional syntatic sugar format as opposed to using the regular syntax. When defining the syntatic sugar format and a field in the `<json_path>` contains characters, such as a dot (.) or colon (:), the syntax needs to be tweaked slightly to account for the `<json_field>`.

For example, when using the `json_extract` function, the previous syntatic sugar format would need to be changed to an updated syntax to account for the field in the `<json_path>` containing characters.

Previous syntatic sugar format for the `json_extract` function:

```programlisting
<json_object_formatted_string> -> <json_path>{}
```

Updated syntatic sugar format for the `json_extract` function, where the `<json_field>` now includes quotations as `"<json_field>"`:

```programlisting
<json_object_formatted_string> -> ["<json_field>"]{}
```

For each JSON function, the syntax of the syntatic sugar format can change slightly, but the `["<json_field>"]` format is the same. The `["<json_field>"]` identifies the data you want to extract using dot-notation, where the data extracted is dependent on your syntax.

Example

If you have the following JSON object defined:

```programlisting
{"a.b": 
    {"inn": 
        {"one":1}
    }
}
```

To extract the data `{"one":1}`, the `["<json_field>"]` would need to be defined as `["a.b"].inn` for all JSON functions. For example, when using the `json_extract` function, the syntatic sugar format is:

```programlisting
json_field -> ["a.b"].inn{}
```

To extract the data `{"inn": {"one":1}}`, the `["<json_field>"]` would need to be defined as `["a.b"]` for all JSON functions. For example, when using the `json_extract` function, the syntatic sugar format is:

```programlisting
json_field -> ["a.b"]{}
```

Example

If you have the following `json_object` defined:

```programlisting
{"a.b": 
    {"inn.inn": 
        {"one":1}
    }
}
```

To extract the data `{"one":1}`, the `["<json_field>"]` would need to be defined as `["a.b"]["inn.inn"]` for all JSON functions. For example, when using the `json_extract` function, the syntatic sugar format is:

```programlisting
json_field -> ["a.b"]["inn.inn"]{}
```

</details>
