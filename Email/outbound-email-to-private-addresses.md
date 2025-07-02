## Outbound Email from Company Domain to Popular Free Email Accounts


Show emails sent from company domain addresses to popular private email accounts.


```kusto
EmailEvents
| where SenderFromDomain in ("mydomain.com", "mydomain2.com")
| where RecipientEmailAddress !endswith "@mydomain.com"
    and RecipientEmailAddress !endswith "@mydomain2.com"
    and (
        RecipientEmailAddress endswith "@gmail.com"
        or RecipientEmailAddress endswith "@yahoo.com"
        or RecipientEmailAddress endswith "@outlook.com"
        or RecipientEmailAddress endswith "@hotmail.com"
        or RecipientEmailAddress endswith "@icloud.com"
        or RecipientEmailAddress endswith "@aol.com"
        or RecipientEmailAddress endswith "@protonmail.com"
        or RecipientEmailAddress endswith "@zoho.com"
        or RecipientEmailAddress endswith "@mail.com"
        or RecipientEmailAddress endswith "@bigpond.com"
        or RecipientEmailAddress endswith "@storyconsulting.com.au"
        or RecipientEmailAddress endswith "@live.com.au"
        or RecipientEmailAddress endswith "@yahoo.com.au"
        or RecipientEmailAddress endswith "@iinet.net.au"
        or RecipientEmailAddress endswith "@live.com"
        or RecipientEmailAddress endswith "@tutanota.com"
        or RecipientEmailAddress endswith "@optusnet.net.au"
        or RecipientEmailAddress endswith "@exemail.com.au"
        or RecipientEmailAddress endswith "@westnet.com.au"
        or RecipientEmailAddress endswith "@bigpond.net.au"
        or RecipientEmailAddress endswith "@rocketmail.com"
        or RecipientEmailAddress endswith "@yahoo.com.ph"
        or RecipientEmailAddress endswith "@hotmail.fr"
        or RecipientEmailAddress endswith "@hotmail.com.au"
        or RecipientEmailAddress endswith "@proton.me"
    )
| project Timestamp, SenderFromAddress, RecipientEmailAddress, Subject
| order by Timestamp desc
