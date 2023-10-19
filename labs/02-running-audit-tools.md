# Running audit tools

In this lesson we'll run two popular tools on the account and discuss findings. Remember in any audit performed the tool is literally just that "a tool".  You are the value in optimizing the result, interpreting the result, and providing a triaged report that is actionable for the customer.

## Step-by-step

1. These tools open a ton of files on the system.  Do yourself a favor and bump up your ulimit for maximum open files in the operating system.  

```bash
ulimit -n 4096
```

2. Create a directory for this audit to store the results. 
```bash
mkdir -p ~/workspace/audits/example.com
cd !$
```

3. In a shell that has the exported credentials as environment variables run prowler.  

```bash
prowler aws
```

Prowler will create a variety of outputs.

```
Detailed results are in:
 - HTML: output/prowler-output-550477536801-20231015072043.html
 - JSON-OCSF: output/prowler-output-550477536801-20231015072043.ocsf.json
 - CSV: output/prowler-output-550477536801-20231015072043.csv
 - JSON: output/prowler-output-550477536801-20231015072043.json
 ```
 
 > The most useful two outputs for an auditor are CSV and the HTML report.  However you will never hand off a prowler report to a client.  The value is in triage and inclusion of top true-positive actionable findings.  Using the CSV is great for this.

 4. In a shell that has exported credentials as environment variables run scoutsuite.

 ```bash
 scout aws
 ```

 5. The tools both output several different types of files.  

 ```
 scoutsuite-report/scoutsuite-results # Contains JSON of all the findings and configuration information

 output/ #contains prowler's audit data 
 
 ```

 These are rich with additional information that may not surface in the findings.  As a point of principle always run a tool like trufflehog on output from these to see if configuration information contains secrets.  (Believe it or not this happens all the time)

 6. Run trufflehog on the output to check for any credentials

 ```bash
trufflehog filesystem ./scoutsuite-report
trufflehog filesystem ./output
 ```
> If nothing of note is returned there aren't any exposed secrets in things like environment variables.

7. You're ready to write your client report!  Good news.

A sample report template is available here: https://bit.ly/3tw6M8a

> We will discuss how best to leverage this template live.