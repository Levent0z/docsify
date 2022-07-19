# Splunk

`SPL` = Splunk Processing Language (140 commands)

SPL takes the form:

```
search and filter | munge | report | cleanup
```

## Command Types

- **Distributable**: eval, regex, where, rename, fields, rename, replace
- **Centralized**: head, streamstats // Only works on the search head
- **Transforming**: transactionstats, top, timechart

## Basic search

Example:

```splunk-spl
index=SOMEINDEX source=SOMESOURCE earliest=-24h (or -24h@h to snap to the hour) latest=now
```

## Built-in fields

- `_raw`
- `_time`
- `host`
- `source`
- `sourcetype`
- `splunk_server`
- `splunk_server_group`

## Functions

- `true()`
- `false()`
- `if(EXPRESSION, VALUE_IF_TRUE, VALUE_IF_FALSE)`
- `like(FIELD, "%VALUE%")`
- `min(FIELD)`
- `max(FIELD)`
- `sum(FIELD)`
- `avg(FIELD)`
- `dc(FIELD)`: Distinct count
- `round(VALUE, DECIMALPOINTS)`
- `perc95(FIELD)`: 95th percentile
- `len(TEXT)`
- `lower(TEXT)`
- `strftime(FIELD, FORMATSTRING)`
  - Example: `eval dayofweek=lower(strftime(_time,"%A"))`: Sets day of week, e.g. "saturday"

## Commands

- `head N`: limits the result set to the top $n$ entries.
- `top limit=10 FIELD`: Shows top 10 values for the specified field
- `dedup FIELD1, FIELD2, ...`: Removes duplicates from the results list
- `where if(EXPRESSION, true(), false())`: creates
- `rex field=FIELD "SOMEREGEX"`: Allows results whose field FIELD satisfies the specified regex. Group names become fields.
- `sort FIELD`: sort
- `sort -FIELD`: Reverse sort
- `stats FUNC1(FIELD1) as LABEL1, FUNC2(FIELD2) by FIELD3`: Applies the functions to the fields, groups by field #2.
- `stats min(FIELD1) as LABEL1, max(FIELD2) as LABEL2, sum(FIELD3) as LABEL3, avg(FIR`
- `chart values(FIELD1) as LABEL1, values(FIELD2) as LABEL2 by FIELD3, FIELD4, ...`
- `bucket FIELD span=10m`: Buckets the field values in 10 minute increments.
- `timechart FIELD1 as LABEL by FIELD2 span=1d`: Creates a time chart, grouping data from field #1 in day-long buckets and have different charts based on values of field #2.

## Using spath, mvcount, mvexpand and mvjoin with stringified JSONs

### Use `spath` to reach into the json

Suppose a field contains stringified JSON. We can use the `spath` command to reach into the JSON object by specifying a path, such as `outer.inner.deeper` and label the field located by path using the `output` argument. That field will now be hoisted up to be treated as a regular field from here on, which means we can include it in our query.

```splunk-spl
| makeresults
| eval newField="{\"string\":\"text\"}"
| spath input=newField path=string
| table string
```

### Use `mvcount` to get count of array items.

Use `{}` suffix to indicate an array

```splunk-spl
| makeresults
| eval newField="{\"string\":\"text\",\"array\":[1,2,3,4]}"
| spath input=newField path="array{}" output=arrayObj
| eval itemCount=mvCount(arrayObj)
| table itemCount
```

Spath can also be written in function form. The above is equivalent to:

```splunk-spl
| makeresults
| eval newField="{\"string\":\"text\",\"array\":[1,2,3,4]}"
| eval arrayObj = spath (newField, "array{}")
| eval itemCount=mvcount(arrayObj)
| table itemCount
```

### Use `mvjoin` to join array items

Use mvjoin to string join items of an array

```splunk-spl
| makeresults
| eval newField="{\"string\":\"text\",\"array\":[1,2,3,4]}"
| eval arrayObj = spath (newField, "array{}")
| eval joined=mvjoin(arrayObj, ";")
| table joined
```

### Use `mvexpand` to promote array items to top-level.

Use `{}` suffix to indicate an array.

```splunk-spl
| makeresults
| eval newField="{\"string\":\"text\",\"array\":[1,2,3,4],\"collection\":[{\"name\":\"one\",\"value\":1},{\"name\":\"two\",\"value\":2}]"
| spath input=newField path="collection{}" output=collectionObj
| mvexpand collectionObj
| table collectionObj
```

```splunk-spl
| makeresults
| eval newField="{\"string\":\"text\",\"array\":[1,2,3,4],\"collection\":[{\"name\":\"one\",\"value\":1},{\"name\":\"two\",\"value\":2}]"
| spath input=newField path="collection{}" output=collectionObj
| mvexpand collectionObj
| spath input=collectionObj path=name output=name
| table name
```

## Function Tips

### Find count of occurrences where keyword appears

**Example**: Find names where the letter 'w' appears

```splunk-spl
| makeresults
| eval newField="{\"collection\":[{\"name\":\"one\",\"value\":1},{\"name\":\"two\",\"value\":2}]"
| spath input=newField path="collection{}.name" output="name"
| eval hasValue=if(like(name, "%w%"), 1, 0)
| stats sum(hasValue)
```

### Assign keywords to matches

```splunk-spl
| ...
| eval LABEL = case(
    match(FIELD, ".*KEYWORD1.*"), "LABEL1",
    match(FIELD, ".*KEYWORD2.*"), "LABEL2",
    1=1, "OTHER")
```

## Performance Tips

- Use Fast or Smart mode instead of Verbose mode
- Avoid `NOT`s (e.g. use A AND C AND D AND E)
- `tstats` is like `stats` but can only be used in indexed time fields for a performance improvements (eg. for source, host, sourcetype)
- Use `TERM()` (all-caps) to match values which might have minor segmenters (`/ : = @ . - $ # \\ _`).
  - Prefer instead of wild chars and partial match. For example, if you are doing a search for the literal value `x.y.z` as:

```splunk-spl
search key=*.z
```

do instead:

```splunk-spl
search key=TERM(x.y.z)
```

## Other tips

- Use `fields` instead of `table` (latter is a formatting command, not a filtering command)
- Don't use join, limited at 50K rows or by time. Better to use `OR` for `sourcetype`s.


## Find Indexes

```splunk-spl
index=* earliest=-2m | stats count as countIndex by index | sort -countIndex | head 10
```
