# Cloud Auditing Workshop

In 2023 cloud environments are becoming increasingly complex resulting in wide variety of misconfigurations. In this workshop you’ll learn how to use point and shoot tools from the open ecosystem for cloud security assessments along with a few pro tips on how to segment and sandbox those. We will also dive into continuous auditing and how to setup long term dashboards for organizations to assess their maturity over time. Attendees will leave with a firm understanding of how to leverage the tools, articulate which method is better based on use case, and assume various roles (safely) in the AWS. 

## Requirements to attend

A laptop that has either a Linux VM or Mac OS. 
The tools for this class are known to work on M1 instances as well as x86_64.

Please ensure that you have the following tools on your *NIX based system:

1. AWS CLIv2 https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
2. AWS Vault https://github.com/99designs/aws-vault
3. Prowler https://docs.prowler.cloud/en/latest/
4. ScoutSuite https://github.com/nccgroup/ScoutSuite/wiki/Setup
5. Trufflehogv3 https://github.com/trufflesecurity/trufflehog
6. oath-toolkit https://www.nongnu.org/oath-toolkit/download.html


## Credits

Much of the infrastructure for this class is deployed using the [Sad Cloud]('https://github.com/nccgroup/sadcloud') project.  Huge thanks to @ramimac
