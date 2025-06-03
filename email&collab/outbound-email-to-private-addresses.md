




```kusto
EmailEvents
| where SenderFromDomain in ("insertcompanydomin.com", "insertcompanydomain.com")
| where not(RecipientEmailAddress endswith "@insertcompanydomain.com" or RecipientEmailAddress endswith "@insertcompanydomain.com")
    and RecipientEmailAddress matches regex "@(gmail|yahoo|outlook|hotmail|icloud|aol|protonmail|zoho|mail).com$"
| project Timestamp, SenderFromAddress, RecipientEmailAddress, Subject
| order by Timestamp desc'```
