# Notifiarr

## Regex to filter Indexer/Tracker for Prowlarr etc health notifications

You can add the following Regex in Options > Health check exclusion.
This Regex will filter the notifications, so only the ones for chosen Tracker/Indexer, or if all of them are offline. 

`^(?!((all[ ]indexers)|(indexers[ ]unavailable.*(Indexer1|Indexer2)))).*$`

> I haven't tested this in combo with the Database/Corruption notifications, as i don't use them with PGSql
