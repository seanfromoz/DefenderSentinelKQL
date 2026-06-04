## Detect suspicious behavior endpoints being disabled/re-enabled


Show endpoints which have been disabled then re-enabled in short succession.

```kusto
let window = 1h;
SecurityEvent
| where TimeGenerated > ago(30d)
| where EventID in (4722, 4725)
| where TargetUserName endswith "$"
| extend ComputerAccount = trim_end("$", TargetUserName)
| extend Action = iff(EventID == 4725, "Disabled", "Enabled")
| summarize
    Events = make_list(pack("Time", TimeGenerated, "Action", Action), 100)
    by ComputerAccount, TargetDomainName
| mv-expand Events
| extend Time = todatetime(Events.Time), Action = tostring(Events.Action)
| sort by ComputerAccount asc, Time asc
| serialize
| extend NextTime = next(Time), NextAction = next(Action)
| where Action == "Disabled" and NextAction == "Enabled"
| extend TimeDiff = NextTime - Time
| where TimeDiff < window
| project
    ComputerAccount,
    DisabledAt = Time,
    EnabledAt = NextTime,
    TimeDiff
| order by TimeDiff asc
