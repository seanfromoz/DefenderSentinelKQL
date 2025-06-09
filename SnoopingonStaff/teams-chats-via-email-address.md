## Search for Teams Chats via Email Address


List teams chats searching via email address.

```kusto
let convoIds =
    MessageEvents
    | where SenderEmailAddress == "email@address.com"
    | distinct MessageId;
MessageEvents
| where MessageId in (convoIds)
| extend RecipientDisplayNames = extract_all(@"RecipientDisplayName"":\s*""([^""]+)""", tostring(RecipientDetails))
| sort by MessageId, Timestamp asc
| project MessageId, Timestamp, SenderEmailAddress, RecipientDisplayNames, TeamsMessageId
