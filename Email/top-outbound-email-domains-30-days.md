## Lists the top outbound domains over 30 days


Show outbound sender domains over 30 days.


```kusto
EmailEvents
| where Timestamp > ago(30d)  // Adjust time range as needed
| extend RecipientDomain = tostring(split(RecipientEmailAddress, "@")[1])
| summarize Count = count() by RecipientDomain
| sort by Count desc
| take 1000
