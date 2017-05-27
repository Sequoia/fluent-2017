## Redis info
* Docs on datatypes: https://redis.io/topics/data-types

## Docker

* Useful for local, **not** useful for `now`
* Make sure to expose port in docker AND `-p 6379:6379` to expose port externally

## Redis-labs

1. Create account
2. Verify email
3. Create "subscription" (pick standard/30mb/free)
4. Create database
  * Set password! Note this!
5. Wait for it to start
6. Note `hostname` and `port`

## Connecting & Testing

`redis-cli -h <host> -p <port> -a <database password>`

```no-highlight
redis-19435.c12.us-east-1-4.ec2.cloud.redislabs.com:19435> keys *
(empty list or set)
redis-19435.c12.us-east-1-4.ec2.cloud.redislabs.com:19435> set foo bar
OK
redis-19435.c12.us-east-1-4.ec2.cloud.redislabs.com:19435> get foo
"bar"
redis-19435.c12.us-east-1-4.ec2.cloud.redislabs.com:19435> keys *
1) "foo"
```