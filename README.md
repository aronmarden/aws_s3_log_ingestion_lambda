[![Community Plus header](https://github.com/newrelic/opensource-website/raw/master/src/images/categories/Community_Plus.png)](https://opensource.newrelic.com/oss-category/#community-plus)

# AWS Lambda for sending logs from S3 to New Relic

`s3-log-ingestion-lambda` is an AWS Serverless application that sends log data from an S3 bucket of your choice to New Relic.

## Requirements

To forward data to New Relic you need access to a [New Relic License Key](https://docs.newrelic.com/docs/accounts/install-new-relic/account-setup/license-key).

## Configuration

### Log Sampling

This Lambda function supports log sampling to reduce the volume of logs sent to New Relic. This can be useful for high-volume log sources where you want to analyze a representative sample rather than all logs.

#### Environment Variables

- **`LOG_SAMPLING_PERCENTAGE`** (optional): Specifies the percentage of logs to sample and send to New Relic. 
  - **Range**: 1 to 100 (integer or decimal values)
  - **Default**: 100 (no sampling - all logs are sent)
  - **Examples**: 
    - `100` - Send all logs (default behavior)
    - `50` - Send 50% of logs randomly sampled
    - `10` - Send 10% of logs randomly sampled  
    - `1` - Send 1% of logs randomly sampled

#### How Sampling Works

- Sampling is applied at the individual log line level
- Each log line is randomly selected based on the sampling percentage
- The sampling is deterministic per invocation but random across different log files
- Sampling statistics (total logs processed vs. sampled logs sent) are logged for monitoring

#### Example Configurations

**Serverless Framework (serverless.yml):**
```yaml
environment:
  LOG_SAMPLING_PERCENTAGE: "25"  # Send 25% of logs
```

**CloudFormation Template:**
```yaml
Environment:
  Variables:
    LOG_SAMPLING_PERCENTAGE: "10"  # Send 10% of logs
```

**AWS Lambda Console:**
Set the environment variable `LOG_SAMPLING_PERCENTAGE` to your desired percentage value.

## Install

To install and configure the New Relic S3 log shipper Lambda, [see our documentation](https://docs.newrelic.com/docs/logs/enable-new-relic-logs/1-enable-logs/aws-lambda-sending-logs-s3).

## Support

New Relic hosts and moderates an online forum where customers can interact with New Relic employees as well as other customers to get help and share best practices. Like all official New Relic open source projects, there's a [related Community topic in the New Relic Explorers Hub](https://discuss.newrelic.com/t/aws-s3-log-ingestion-lambda/104986).

## Contributing

Contributions to improve s3-log-ingestion-lambda are encouraged! Keep in mind when you submit your pull request, you'll need to sign the CLA via the click-through using CLA-Assistant. You only have to sign the CLA one time per project.

To execute our corporate CLA, which is required if your contribution is on behalf of a company, or if you have any questions, please drop us an email at opensource@newrelic.com.

## Developers

For more information about how to contribute from the developer point of view,
we recommend you to take a look to the [DEVELOPER.md](./DEVELOPER.md) that 
contains most of the info you'll need.

## License
`s3-log-ingestion-lambda` is licensed under the [Apache 2.0](http://apache.org/licenses/LICENSE-2.0.txt) License. The s3-log-ingestion-lambda also uses source code from third party libraries. Full details on which libraries are used and the terms under which they are licensed can be found in the third party notices document