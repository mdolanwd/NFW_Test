
### AWS Network Firewall Configuration

The [firewall.tf](firewall.tf) template file contains the definitions of the FW rule-groups that these templates come with by default. 

The [default action](https://docs.aws.amazon.com/network-firewall/latest/developerguide/stateless-default-actions.html) taken by the stateless engine is `Forward to stateful rule groups`.

[Alert logs](https://docs.aws.amazon.com/network-firewall/latest/developerguide/logging-cw-logs.html) are persisted in a dedicated Cloudwatch Log Group (`/aws/network-firewall/alert`).

[Flow logs](https://docs.aws.amazon.com/network-firewall/latest/developerguide/logging-cw-logs.html) are persisted in a dedicated S3 Bucket (`network-firewall-flow-bucket-*`).

The rule-groups configured in the policy are the following:
- `drop-icmp`: this is a stateless rule group that drops all ICMP traffic
- `drop-non-http-between-vpcs`: this stateful rules drops anything but HTTP traffic between spoke VPCs.
- `block-domains`: this stateful rule prevents any HTTP traffic to occur to two FQDNs specified in the rule itself.

The template deploys two instances in `spoke-vpc-a` and `spoke-vpc-b` in the `protected` subnets that you can use to test east-west connectivity (and north-south).



### Cleanup
Remember to clean up after your work is complete. You can do that by doing `terraform destroy`.

Note that this command will delete all the resources previously created by Terraform.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the [LICENSE](LICENSE) file.

