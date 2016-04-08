Logging
=======

We're using [fluentd](http://www.fluentd.org/) to log records from all our applications.

Schema
------
To get the most value out of a centralized logging system it's important to use a common schema for records.

```json
{
  "timestamp": "2016-04-08T10:39:42+00:00",
  "message": "<message>",
  "level": "<level>",
  "httpRequest": {
    "uri": "https://www.example.com/checkout?bundle=136",
    "ip": "1.2.3.4",
    "referer": "https://www.example.com/account",
    "useragent": "Mozilla/5.0"
  },
  "computerInfo": {
    "phpInfo": "5.6"
  },
  "<app-name>": {
    "user": "<userId>",
    "client": "<requestClientId>",
    "extra1": "foo",
    "extra2": "bar"
  }
}
```

- **timestamp**: Full ISO 8601, optionally with fractions of a second
- **level**: "debug", "warning", "error" etc. See https://tools.ietf.org/html/rfc5424
- **&lt;app-name&gt;**: Any extra fields specific to the application
