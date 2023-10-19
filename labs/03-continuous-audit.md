# Continuous Audit and Why

The CSPM market has bloomed in the last 3 years.  CSPM standing for Cloud Security Posture Management.  It simply 
means continuous scanning of your infrastructure.  Hopefully this comes with some kind of alerting or workflow enabled 
to assist engineers in triaging and acting on findings.

As a cloud auditor if a customer is already a user of a CSPM tool you need not run point and shoot scans in order to 
audit the environment.  You can simply ask for access to their respective vendor provided platform.  

We'll examine the native AWS Solution in the lab today as well as a vendor provided solution.


## Step-by-step

### AWS Config

1. Navigate to AWS Config in console of the account you have read only access in.  [Click here](https://us-west-2.console.aws.amazon.com/config/home?region=us-west-2#/home)

2. This has been pre-configured for you but the most interesting interface is perhaps the ["advanced query interface"]('https://us-west-2.console.aws.amazon.com/config/home?region=us-west-2#/queries') If you're looking for all the things you can query you can find
it [here](https://github.com/awslabs/aws-config-resource-schema).

3. Run the following to check for public RDS

```sql
SELECT
    resourceId,
    resourceName,
    resourceType,
    configuration.engine,
    configuration.publiclyAccessible
WHERE
    resourceType = 'AWS::RDS::DBInstance'
    AND configuration.publiclyAccessible = TRUE
```

4. Run the following to check for unencrypted buckets

```sql
SELECT
    resourceId,
    resourceType,
    supplementaryConfiguration.ServerSideEncryptionConfiguration.rules
WHERE
    resourceType = 'AWS::S3::Bucket'
    AND NOT (
        supplementaryConfiguration.ServerSideEncryptionConfiguration.rules.applyServerSideEncryptionByDefault.sseAlgorithm = 'aws:kms'
        OR supplementaryConfiguration.ServerSideEncryptionConfiguration.rules.applyServerSideEncryptionByDefault.sseAlgorithm = 'AES256'
    )
```

5. Check out the conformance pack dashboard -- one has been deployed for PCI compliance.  [PCI Dashboard](https://us-west-2.console.aws.amazon.com/config/home?region=us-west-2#/conformance-packs/details?conformancePackName=PCI) This has been pre-configured for you.  As a consultant setting up dashboarding like this is a potential upsell.

6. Let's check out a single vendor provided solution.  Navigate to https://app.datadoghq.com and sign in with user: andrewkrug+audit_workshop_dd@gmail.com (the password will be provided in the session.)

7. Visit the Datadog CSM Dashboard for compliance https://app.datadoghq.com/security/compliance/home.

8. Check out one of the [findings](https://app.datadoghq.com/security/compliance/home/pci?panels=cprule%7Crule%7CruleId%3Aee4-ngx-bwr%7CresourceId%3A%7Ccontext%3A&timestamp=1697393824949&live=true).

> We'll discuss these dashboards during the session.