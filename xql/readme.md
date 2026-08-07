# Cortex XQL Command Reference

Cortex XQL (Extended Query Language) is a powerful query language used in the Cortex platform for threat hunting, investigation, and analytics across your security data. This reference provides comprehensive documentation for all XQL functions and pipeline stages.

XQL queries are composed of **stages** connected in a pipeline, with **functions** used within those stages to transform, filter, and analyze data. This reference is organized into two main sections:

* [**Functions**](readme/functions) – Built-in functions, indexes, and detailed reference pages.
* [**Stages**](readme/stages) – Pipeline stages, indexes, and detailed reference pages.

## Functions

| Function                                                                                     | Description                                                                                                    |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| [`acos`](readme/functions/acos)                                                              | Calculate the inverse cosine (arccosine) of a numerical expression                                             |
| [`add`](readme/functions/add)                                                                |                                                                                                                |
| [`approx_count`](readme/functions/approx_count)                                              |                                                                                                                |
| [`approx_quantiles`](readme/functions/approx_quantiles)                                      |                                                                                                                |
| [`approx_top`](readme/functions/approx_top)                                                  |                                                                                                                |
| [`asin`](readme/functions/asin)                                                              | Calculate the inverse sine (arcsine) of a numerical expression                                                 |
| [`array_all`](readme/functions/array_all)                                                    |                                                                                                                |
| [`array_any`](readme/functions/array_any)                                                    |                                                                                                                |
| [`array_length`](readme/functions/array_length)                                              |                                                                                                                |
| [`arrayconcat`](readme/functions/arrayconcat)                                                |                                                                                                                |
| [`arraycreate`](readme/functions/arraycreate)                                                |                                                                                                                |
| [`arraydistinct`](readme/functions/arraydistinct)                                            |                                                                                                                |
| [`arrayfilter`](readme/functions/arrayfilter)                                                |                                                                                                                |
| [`arrayindex`](readme/functions/arrayindex)                                                  |                                                                                                                |
| [`arrayindexof`](readme/functions/arrayindexof)                                              |                                                                                                                |
| [`arraymap`](readme/functions/arraymap)                                                      |                                                                                                                |
| [`arraymerge`](readme/functions/arraymerge)                                                  |                                                                                                                |
| [`arrayrange`](readme/functions/arrayrange)                                                  |                                                                                                                |
| [`arraystring`](readme/functions/arraystring)                                                |                                                                                                                |
| [`avg`](readme/functions/avg_with_comp_stage)                                                |                                                                                                                |
| [`avg`](readme/functions/avg_with_windowcomp_stage)                                          |                                                                                                                |
| [`bitwise_and`](readme/functions/bitwise_and)                                                | Perform a bitwise AND operation between two integer values                                                     |
| [`bitwise_or`](readme/functions/bitwise_or)                                                  | Perform a bitwise OR operation between two integer values                                                      |
| [`bitwise_sleft`](readme/functions/bitwise_sleft)                                            | Perform a bitwise left shift operation on an integer value                                                     |
| [`bitwise_sright`](readme/functions/bitwise_sright)                                          | Perform a bitwise right shift operation on an integer value                                                    |
| [`bitwise_xor`](readme/functions/bitwise_xor)                                                | Perform a bitwise exclusive OR (XOR) operation between two integer values                                      |
| [`cbrt`](readme/functions/cbrt)                                                              | Calculate the cube root of a numeric value                                                                     |
| [`ceil`](readme/functions/ceil)                                                              | Round a number up to the nearest integer                                                                       |
| [`coalesce`](readme/functions/coalesce)                                                      |                                                                                                                |
| [`concat`](readme/functions/concat)                                                          |                                                                                                                |
| [`convert_from_base_64`](readme/functions/convert_from_base_64)                              |                                                                                                                |
| [`convert_to_base_64`](readme/functions/convert_to_base_64)                                  |                                                                                                                |
| [`cos`](readme/functions/cos)                                                                | Calculate the cosine of a numeric value specified in radians                                                   |
| [`cosine_distance`](readme/functions/cosine_distance)                                        | Calculate the cosine distance between two numeric vectors                                                      |
| [`cot`](readme/functions/cot)                                                                | Calculate the cotangent of a numeric value specified in radians                                                |
| [`count`](readme/functions/count_with_comp_stage)                                            |                                                                                                                |
| [`count`](readme/functions/count_with_windowcomp_stage)                                      |                                                                                                                |
| [`count_distinct`](readme/functions/count_distinct)                                          |                                                                                                                |
| [`csc`](readme/functions/csc)                                                                | Calculate the cosecant of a numeric value specified in radians                                                 |
| [`current_time`](readme/functions/current_time)                                              |                                                                                                                |
| [`date_floor`](readme/functions/date_floor)                                                  |                                                                                                                |
| [`divide`](readme/functions/divide)                                                          |                                                                                                                |
| [`earliest`](readme/functions/earliest)                                                      |                                                                                                                |
| [`euclidean_distance`](readme/functions/euclidean_distance)                                  | Calculate the Euclidean distance between two numeric vectors                                                   |
| [`exp`](readme/functions/exp)                                                                | Calculate the value of e raised to the power of a numeric value                                                |
| [`extract_time`](readme/functions/extract_time)                                              |                                                                                                                |
| [`extract_url_host`](readme/functions/extract_url_host)                                      |                                                                                                                |
| [`extract_url_pub_suffix`](readme/functions/extract_url_pub_suffix)                          |                                                                                                                |
| [`extract_url_registered_domain`](readme/functions/extract_url_registered_domain)            |                                                                                                                |
| [`first`](readme/functions/first)                                                            |                                                                                                                |
| [`first_value`](readme/functions/first_value)                                                |                                                                                                                |
| [`floor`](readme/functions/floor)                                                            |                                                                                                                |
| [`format_string`](readme/functions/format_string)                                            |                                                                                                                |
| [`format_timestamp`](readme/functions/format_timestamp)                                      |                                                                                                                |
| [`greatest`](readme/functions/greatest)                                                      | Return the largest value from a list of expressions                                                            |
| [`if`](readme/functions/if)                                                                  |                                                                                                                |
| [`incidr`](readme/functions/incidr)                                                          |                                                                                                                |
| [`incidr6`](readme/functions/incidr6)                                                        |                                                                                                                |
| [`incidrlist`](readme/functions/incidrlist)                                                  |                                                                                                                |
| [`int_to_ip`](readme/functions/int_to_ip)                                                    |                                                                                                                |
| [`ip_to_int`](readme/functions/ip_to_int)                                                    |                                                                                                                |
| [`is_ipv4`](readme/functions/is_ipv4)                                                        |                                                                                                                |
| [`is_ipv6`](readme/functions/is_ipv6)                                                        |                                                                                                                |
| [`is_known_private_ipv4`](readme/functions/is_known_private_ipv4)                            |                                                                                                                |
| [`is_known_private_ipv6`](readme/functions/is_known_private_ipv6)                            |                                                                                                                |
| [`json_extract`](readme/functions/json_extract)                                              |                                                                                                                |
| [`json_extract_array`](readme/functions/json_extract_array)                                  |                                                                                                                |
| [`json_extract_scalar`](readme/functions/json_extract_scalar)                                |                                                                                                                |
| [`json_extract_scalar_array`](readme/functions/json_extract_scalar_array)                    |                                                                                                                |
| [`json_path_extract`](readme/functions/json_path_extract)                                    |                                                                                                                |
| [`json_functions_reference`](readme/functions/json_functions_reference)                      | A comprehensive guide to the four JSON extraction functions                                                    |
| [`lag`](readme/functions/lag)                                                                |                                                                                                                |
| [`last`](readme/functions/last)                                                              |                                                                                                                |
| [`last_value`](readme/functions/last_value)                                                  |                                                                                                                |
| [`latest`](readme/functions/latest)                                                          |                                                                                                                |
| [`least`](readme/functions/least)                                                            | Return the smallest value from a list of expressions                                                           |
| [`len`](readme/functions/len)                                                                |                                                                                                                |
| [`list (comp)`](readme/functions/list_with_comp_stage)                                       | Collect all values of a field and return them as an array within the comp stage                                |
| [`ln`](readme/functions/ln)                                                                  | Calculate the natural logarithm (base e) of a numeric value                                                    |
| [`log`](readme/functions/log)                                                                | Calculate the logarithm of a numeric value with a specified base                                               |
| [`log10`](readme/functions/log10)                                                            | Calculate the base-10 logarithm of a numeric value                                                             |
| [`lowercase`](readme/functions/lowercase)                                                    |                                                                                                                |
| [`ltrim`](readme/functions/ltrim)                                                            |                                                                                                                |
| [`max (comp)`](readme/functions/max_with_comp_stage)                                         | Return the maximum value of a field within the comp stage                                                      |
| [`max (windowcomp)`](readme/functions/max_with_windowcomp_stage)                             | Compute the maximum value of a field over a window of rows within the windowcomp stage                         |
| [`md5`](readme/functions/md5)                                                                |                                                                                                                |
| [`median (comp)`](readme/functions/median_with_comp_stage)                                   | Return the median value of a numeric field within the comp stage                                               |
| [`median (windowcomp)`](readme/functions/median_with_windowcomp_stage)                       | Compute the median value of a numeric field over a window of rows within the windowcomp stage                  |
| [`min (comp)`](readme/functions/min_with_comp_stage)                                         | Return the minimum value of a field within the comp stage                                                      |
| [`min (windowcomp)`](readme/functions/min_with_windowcomp_stage)                             | Compute the minimum value of a field over a window of rows within the windowcomp stage                         |
| [`mod`](readme/functions/mod)                                                                | Calculate the remainder (modulus) of the division of two numeric values                                        |
| [`multiply`](readme/functions/multiply)                                                      |                                                                                                                |
| [`object_create`](readme/functions/object_create)                                            |                                                                                                                |
| [`object_merge`](readme/functions/object_merge)                                              |                                                                                                                |
| [`parse_epoch`](readme/functions/parse_epoch)                                                |                                                                                                                |
| [`parse_timestamp`](readme/functions/parse_timestamp)                                        |                                                                                                                |
| [`pow`](readme/functions/pow)                                                                |                                                                                                                |
| [`power`](readme/functions/power)                                                            | Raise a number to the power of another number (alias for pow)                                                  |
| [`rand`](readme/functions/rand)                                                              | Generate a pseudo-random floating-point number between 0 and 1                                                 |
| [`range_bucket`](readme/functions/range_bucket)                                              | Determine which bucket a numeric value falls into given an array of boundaries                                 |
| [`rank (windowcomp)`](readme/functions/rank_with_windowcomp_stage)                           | Assign a rank to each row within a partition in the windowcomp stage                                           |
| [`regexcapture`](readme/functions/regexcapture)                                              |                                                                                                                |
| [`regextract`](readme/functions/regextract)                                                  | Extract a substring from a field value using a regular expression pattern                                      |
| [`replace`](readme/functions/replace)                                                        |                                                                                                                |
| [`replex`](readme/functions/replex)                                                          |                                                                                                                |
| [`round`](readme/functions/round)                                                            |                                                                                                                |
| [`row_number (windowcomp)`](readme/functions/row_number_with_windowcomp_stage)               | Assign a unique sequential integer to each row within a partition in the windowcomp stage                      |
| [`rtrim`](readme/functions/rtrim)                                                            |                                                                                                                |
| [`safe_add`](readme/functions/safe_add)                                                      | Perform addition with overflow protection, returning null on overflow                                          |
| [`safe_divide`](readme/functions/safe_divide)                                                | Perform division with error protection, returning null on division by zero                                     |
| [`safe_multiply`](readme/functions/safe_multiply)                                            | Perform multiplication with overflow protection, returning null on overflow                                    |
| [`safe_negate`](readme/functions/safe_negate)                                                | Negate a numeric value with overflow protection, returning null on overflow                                    |
| [`safe_subtract`](readme/functions/safe_subtract)                                            | Perform subtraction with overflow protection, returning null on overflow                                       |
| [`sec`](readme/functions/sec)                                                                | Calculate the secant of a numeric value specified in radians                                                   |
| [`sha1`](readme/functions/sha1)                                                              |                                                                                                                |
| [`sha256`](readme/functions/sha256)                                                          |                                                                                                                |
| [`sha512`](readme/functions/sha512)                                                          |                                                                                                                |
| [`sign`](readme/functions/sign)                                                              | Determine the sign of a numeric value (-1, 0, or 1)                                                            |
| [`sin`](readme/functions/sin)                                                                | Calculate the sine of a numeric value specified in radians                                                     |
| [`split`](readme/functions/split)                                                            |                                                                                                                |
| [`sqrt`](readme/functions/sqrt)                                                              | Calculate the square root of a numeric value                                                                   |
| [`stddev_population (comp)`](readme/functions/stddev_population_with_comp_stage)             | Compute the population standard deviation of a numeric field within the comp stage                             |
| [`stddev_population (windowcomp)`](readme/functions/stddev_population_with_windowcomp_stage) | Compute the population standard deviation of a numeric field over a window of rows within the windowcomp stage |
| [`stddev_sample (comp)`](readme/functions/stddev_sample_with_comp_stage)                     | Compute the sample standard deviation of a numeric field within the comp stage                                 |
| [`stddev_sample (windowcomp)`](readme/functions/stddev_sample_with_windowcomp_stage)         | Compute the sample standard deviation of a numeric field over a window of rows within the windowcomp stage     |
| [`string_count`](readme/functions/string_count)                                              |                                                                                                                |
| [`subtract`](readme/functions/subtract)                                                      |                                                                                                                |
| [`sum (comp)`](readme/functions/sum_with_comp_stage)                                         | Compute the sum of a numeric field within the comp stage                                                       |
| [`sum (windowcomp)`](readme/functions/sum_with_windowcomp_stage)                             | Compute the sum of a numeric field over a window of rows within the windowcomp stage                           |
| [`tan`](readme/functions/tan)                                                                | Calculate the tangent of a numeric value specified in radians                                                  |
| [`time_frame_end`](readme/functions/time_frame_end)                                          |                                                                                                                |
| [`timestamp_diff`](readme/functions/timestamp_diff)                                          |                                                                                                                |
| [`timestamp_seconds`](readme/functions/timestamp_seconds)                                    |                                                                                                                |
| [`to_boolean`](readme/functions/to_boolean)                                                  |                                                                                                                |
| [`to_epoch`](readme/functions/to_epoch)                                                      |                                                                                                                |
| [`to_float`](readme/functions/to_float)                                                      |                                                                                                                |
| [`to_integer`](readme/functions/to_integer)                                                  |                                                                                                                |
| [`to_json_string`](readme/functions/to_json_string)                                          |                                                                                                                |
| [`to_number`](readme/functions/to_number)                                                    |                                                                                                                |
| [`to_string`](readme/functions/to_string)                                                    |                                                                                                                |
| [`to_timestamp`](readme/functions/to_timestamp)                                              |                                                                                                                |
| [`trim`](readme/functions/trim)                                                              |                                                                                                                |
| [`trunc`](readme/functions/trunc)                                                            | Truncate a numeric value to a specified number of decimal places                                               |
| [`uppercase`](readme/functions/uppercase)                                                    |                                                                                                                |
| [`values`](readme/functions/values)                                                          | Collect all distinct values of a field and return them as an array within the comp stage                       |
| [`var`](readme/functions/var)                                                                | Compute the variance of a numeric field within the comp stage                                                  |
| [`wildcard_match`](readme/functions/wildcard_match)                                          |                                                                                                                |

## Stages

| Stage                                      | Description |
| ------------------------------------------ | ----------- |
| [`alter`](readme/stages/alter)             |             |
| [`arrayexpand`](readme/stages/arrayexpand) |             |
| [`bin`](readme/stages/bin)                 |             |
| [`call`](readme/stages/call)               |             |
| [`comp`](readme/stages/comp)               |             |
| [`config`](readme/stages/config)           |             |
| [`dataset`](readme/stages/dataset)         |             |
| [`dedup`](readme/stages/dedup)             |             |
| [`fields`](readme/stages/fields)           |             |
| [`filter`](readme/stages/filter)           |             |
| [`iploc`](readme/stages/iploc)             |             |
| [`join`](readme/stages/join)               |             |
| [`limit`](readme/stages/limit)             |             |
| [`presets`](readme/stages/presets)         |             |
| [`replacenull`](readme/stages/replacenull) |             |
| [`search`](readme/stages/search)           |             |
| [`sort`](readme/stages/sort)               |             |
| [`tag`](readme/stages/tag)                 |             |
| [`target`](readme/stages/target)           |             |
| [`top`](readme/stages/top)                 |             |
| [`transaction`](readme/stages/transaction) |             |
| [`union`](readme/stages/union)             |             |
| [`view`](readme/stages/view)               |             |
| [`windowcomp`](readme/stages/windowcomp)   |             |
