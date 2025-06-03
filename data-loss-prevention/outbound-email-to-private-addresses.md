## Outbound Email from Company Domain to Popular Free Email Accounts

One of the first basic KQL scripts for showing emails sent from company domain addresses to popular private email accounts.


```kusto
EmailEvents
| where SenderFromDomain in ("insertcompanydomin.com", "insertcompanydomain.com")
| where not(RecipientEmailAddress endswith "@insertcompanydomain.com" or RecipientEmailAddress endswith "@insertcompanydomain.com")
    and RecipientEmailAddress matches regex "@(gmail|yahoo|outlook|hotmail|icloud|aol|protonmail|zoho|mail).com$"
| project Timestamp, SenderFromAddress, RecipientEmailAddress, Subject
| order by Timestamp desc'```
