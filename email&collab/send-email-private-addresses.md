EmailEvents
| where SenderFromDomain in ("stepsgroup.com.au", "stepsstaffingsolutions.com.au")
| where not(RecipientEmailAddress endswith "@stepsgroup.com.au" or RecipientEmailAddress endswith "@stepsstaffingsolutions.com.au")
    and RecipientEmailAddress matches regex "@(gmail|yahoo|outlook|hotmail|icloud|aol|protonmail|zoho|mail).com$"
| project Timestamp, SenderFromAddress, RecipientEmailAddress, Subject
| order by Timestamp desc
