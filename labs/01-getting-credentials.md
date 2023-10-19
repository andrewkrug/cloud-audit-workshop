# Getting credentials and verifying access

In this lesson you'll learn how to obtain credentials for your cloud audit.  Increasingly companies are moving away from long-lived access keypairs.  You wouldn't want your access as an auditor to be a compliance violation, right?

## Step-by-step

1. In any web browser visit the "start url" [https://d-90679c1e00.awsapps.com/start]('https://d-90679c1e00.awsapps.com/start')
2. Sign in with the username _cloudaudit_.  The password and TOTP seed for MFA have been shared with you in the room.  
3. When prompted for your second factor credential use oath-toolkit to get your 2FA.  

```bash
export SEED=fill_this_in
oathtool --base32 --totp $SEED
```

4. Click on the "AWS Account Tile" 

5. Click on the only account in the list and then click "Command line or programmatic access. This will present you a set of credentials you'll use for your audit.   

!['credential-screen'](/_static/img/1.png)

6. In a shell set the default profile and region using export commands.  
- `export AWS_DEFAULT_REGION=us-west-2` 
- `export AWS_PROFILE=550477536801_SecurityAudit`

7. Test the credential by running `aws sts get-caller-identity`

A successful test of the credentials will return the following output:

```json
{
    "UserId": "AROAYAKYETYQ2F27BC4IY:cloudaudit",
    "Account": "550477536801",
    "Arn": "arn:aws:sts::550477536801:assumed-role/AWSReservedSSO_SecurityAudit_96f966a980e0d3d9/cloudaudit"
}
```

8. Congratulations! You now have a valid set of credentials for use during your audit.  These are temporary credentials that in this case last 2 hours each time they are generated.  These credentials can be configured to last up to 12 hours per session which is especially useful for auditing accounts with lots of resources.

