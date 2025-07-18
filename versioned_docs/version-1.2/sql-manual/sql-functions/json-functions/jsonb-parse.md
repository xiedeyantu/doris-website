---
{
    "title": "JSONB_PARSE",
    "language": "en"
}
---

## jsonb_parse
### description
#### Syntax

```sql
JSONB jsonb_parse(VARCHAR json_str)
JSONB jsonb_parse_error_to_null(VARCHAR json_str)
JSONB jsonb_parse_error_to_value(VARCHAR json_str, VARCHAR default_json_str)
```

jsonb_parse functions parse JSON string to binary format. A series of functions are provided to satisfy different demand for exception handling.
- all return NULL if json_str is NULL
- if json_str is not valid
  - jsonb_parse will report error
  - jsonb_parse_error_to_null will return NULL
  - jsonb_parse_error_to_value will return the value specified by default_json_str

### example

1. parse valid JSON string

```
mysql> SELECT jsonb_parse('{"k1":"v31","k2":300}');
+--------------------------------------+
| jsonb_parse('{"k1":"v31","k2":300}') |
+--------------------------------------+
| {"k1":"v31","k2":300}                |
+--------------------------------------+
1 row in set (0.01 sec)
```

2. parse invalid JSON string

```
mysql> SELECT jsonb_parse('invalid json');
ERROR 1105 (HY000): errCode = 2, detailMessage = json parse error: Invalid document: document must be an object or an array for value: invalid json

mysql> SELECT jsonb_parse_error_to_null('invalid json');
+-------------------------------------------+
| jsonb_parse_error_to_null('invalid json') |
+-------------------------------------------+
| NULL                                      |
+-------------------------------------------+
1 row in set (0.01 sec)

mysql> SELECT jsonb_parse_error_to_value('invalid json', '{}');
+--------------------------------------------------+
| jsonb_parse_error_to_value('invalid json', '{}') |
+--------------------------------------------------+
| {}                                               |
+--------------------------------------------------+
1 row in set (0.00 sec)
```

refer to jsonb tutorial for more.

### keywords
JSONB, JSON, jsonb_parse, jsonb_parse_error_to_null, jsonb_parse_error_to_value