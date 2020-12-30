# Splunk

SPL = Splunk Processing Language (140 commands)

SPL: search and filter | munge | report | cleanup

Distributable Commands: eval, regex, where, rename, fields, rename, replace 
Centralized Commands: head, streamstats          // Only works on the search head
Transforming Commands: transactionstats, top, timechart

index=xyz
source=www
earliest=-24h   (or -24h@h to snap to the hour)
latest=now

tstats is like stats but can only be used in indexed time fields for a performance improvements (eg. for source, host, sourcetype)

Use Fast or Smart mode instead of Verbose mode
Avoid NOTS (e.g. use A AND C AND D AND E)

spath input=field


TERM directive (all-caps)
prevents breaking on minor segmenters --> `/ : = @ . - $ # \\ _`


Use fields instead of table (latter is a formatting command, not a filtering command)


|bucket _time span=10m

Don't use join, limited at 50K rows or by time. Better to use OR for sourcetypes.

dedup

stats latest()

