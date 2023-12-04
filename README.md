# aws-query-org

Query CLI for the AWS Config aggregator.

Install jq and AWS CLI, download the query-org script, add it to the PATH, set the default session to the account and region that hosts the aggregator, and then you can run commands like this:

```bash
query-org "
  SELECT
    accountId,
    awsRegion,
    resourceName
  WHERE resourceType = 'AWS::S3::Bucket'
  ;"
```

To get output like this:

```json
[
  {
    "accountId": "111111111111",
    "awsRegion": "eu-central-1",
    "resourceName": "bucket1"
  },
  {
    "accountId": "111111111111",
    "awsRegion": "eu-central-1",
    "resourceName": "bucket2"
  },
  {
    "accountId": "222222222222",
    "awsRegion": "eu-central-1",
    "resourceName": "bucket3"
  },
  ...
]
```

A tip: Don't end the query string with a newline or you'll get a confusing error: `An error occurred (InvalidExpressionException) when calling the SelectAggregateResourceConfig operation: syntax error at line 7, column 1`.

It will take a while to retrieve a result with many thousands of items because the API responds with 100 items per page.
