// Users NOT in a specific security group (match by display name)
let targetGroupName = "security_group";
let users_latest =
    IdentityInfo
    | summarize arg_max(TimeGenerated, *) by AccountObjectId
    | where Type =~ "User" and IsAccountEnabled == true;
let members_of_group =
    users_latest
    | where isnotempty(GroupMembership)
    | mv-expand Group = todynamic(GroupMembership)
    | where tostring(tolower(Group)) == tolower(targetGroupName)
    | summarize by AccountObjectId;
users_latest
| where AccountObjectId !in (members_of_group)
| project AccountUpn, AccountDisplayName, Department, JobTitle
| order by AccountUpn asc
