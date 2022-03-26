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

`tstats` is like` stats` but can only be used in indexed time fields for a performance improvements (eg. for source, host, sourcetype)

Use Fast or Smart mode instead of Verbose mode
Avoid `NOT`s (e.g. use A AND C AND D AND E)

## Using `spath` to extract fields from inside a stringified JSON

Suppose a field contains stringified JSON. We can use the `spath` command to reach into the JSON object by specifying a path, such as `outer.inner.deeper` and label the field located by path using the `output` argument. That field will now be hoisted up to be treated as a regular field from here on, which means we can include it in our query.

```splunk
spath input=STRINGFIELD path=JSONPATH output=NEWLABEL
```

## Using `TERM()` for increased performance

The `TERM()` directive (all-caps) prevents breaking on minor segmenters --> `/ : = @ . - $ # \\ _`.

Use `TERM()` to match values, which might have minor segmenters exactly instead of using wild chars and partial match.
For example, if you are doing a search for the literal value `x.y.z` as:

```splunk
search key=*.z
```

do instead:
```splunk
search key=TERM(x.y.z)
```

for much better performance.


## Other tips
- Use fields instead of table (latter is a formatting command, not a filtering command)
- Don't use join, limited at 50K rows or by time. Better to use OR for sourcetypes.


## Draft notes
```
|bucket _time span=10m

dedup

stats latest()
```
