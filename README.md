# alb-log-parser

[![npm](https://img.shields.io/npm/v/alb-log-parser.svg)](https://www.npmjs.com/package/alb-log-parser)
[![Donate to this project using Patreon](https://img.shields.io/badge/patreon-donate-yellow.svg)](https://www.patreon.com/igtm)
[![alb-log-parser Dev Token](https://badge.devtoken.rocks/alb-log-parser)](https://devtoken.rocks/package/alb-log-parser)

A basic parser for ALB access logs, forked from elb log parser git@github.com:toshihirock/node-elb-log-parser.git
i cannot find alb log parser instead of elb-log-parser. so i modify a bit of the code. Thank you toshihirock!

## When I use this npm

- ALB Access Log(S3)->Lambda->ElasticSearch. Example [awslabs/amazon-elasticsearch-lambda-samples](https://github.com/awslabs/amazon-elasticsearch-lambda-samples/blob/master/src/s3_lambda_es.js)
- Analyze ELB Access Log

## Install

```
npm install -g alb-log-parser
```

## Supported fields

See <https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-access-logs.html#access-log-entry-format> for definitions

- `type`
- `timestamp`
- `elb`
- `client`
- `client_port`
- `target`
- `target_port`
- `request_processing_time`
- `target_processing_time`
- `response_processing_time`
- `elb_status_code`
- `target_status_code`
- `received_bytes`
- `sent_bytes`
- `request_method`
- `request_uri`
- `request_http_version`
- `request_uri_scheme`
- `request_uri_host`
- `request_uri_port`
- `request_uri_path`
- `request_uri_query`
- `request`
- `user_agent`
- `ssl_cipher`
- `ssl_protocol`
- `target_group_arn`
- `trace_id`
- `domain_name`
- `chosen_cert_arn`
- `matched_rule_priority`
- `request_creation_time`
- `actions_executed`
- `redirect_url`
- `error_reason`
- `target:port_list`
- `target_status_code_list`
- `classification`
- `classification_reason`

## Example API usage

```
node-alb-log-parser$node
> var parse = require('./index');
undefined
> parse('http 2020-08-27T16:35:00.166351Z app/my-loadbalancer/50dc6c495c0c9188 192.168.131.39:2817 192.168.201.251:80 0.000 0.440 0.000 200 200 1107 11912 "GET http://example.com:80/path?foo=bar&baz=bak HTTP/1.1" "Fake/1.0.0 (Linux)" - - arn:aws:elasticloadbalancing:us-east-1:123456789012:targetgroup/my-tg/ffffffffffffffff "Self=1-00000000-111111111111111111111111;Root=1-00000000-222222222222222222222222" "-" "-" 0 2020-08-27T16:34:59.725000Z "forward" "-" "-" "192.168.201.251:80" "200" "-" "-"')
{
  type: 'http',
  timestamp: '2020-08-27T16:35:00.166351Z',
  elb: 'app/my-loadbalancer/50dc6c495c0c9188',
  client: '192.168.131.39',
  client_port: 2817,
  target: '192.168.201.251',
  target_port: 80,
  request_processing_time: 0,
  target_processing_time: 0.44,
  response_processing_time: 0,
  elb_status_code: 200,
  target_status_code: 200,
  received_bytes: 1107,
  sent_bytes: 11912,
  request_method: 'GET',
  request_uri: 'http://example.com:80/path?foo=bar&baz=bak',
  request_http_version: 'HTTP/1.1',
  request_uri_scheme: 'http:',
  request_uri_host: 'example.com',
  request_uri_port: 80,
  request_uri_path: '/path',
  request_uri_query: 'foo=bar&baz=bak',
  request: 'GET http://example.com:80/path?foo=bar&baz=bak HTTP/1.1',
  user_agent: 'Fake/1.0.0 (Linux)',
  ssl_cipher: '-',
  ssl_protocol: '-',
  target_group_arn: 'arn:aws:elasticloadbalancing:us-east-1:123456789012:targetgroup/my-tg/ffffffffffffffff',
  trace_id: 'Self=1-00000000-111111111111111111111111;Root=1-00000000-222222222222222222222222',
  domain_name: '-',
  chosen_cert_arn: '-',
  matched_rule_priority: 0,
  request_creation_time: '2020-08-27T16:34:59.725000Z',
  actions_executed: 'forward',
  redirect_url: '-',
  error_reason: '-',
  'target:port_list': '192.168.201.251:80',
  target_status_code_list: 200,
  classification: '-',
  classification_reason: '-'
}
>
```

You get the idea.

## Tests

```

\$npm test

```

## License

WTFPL
```
