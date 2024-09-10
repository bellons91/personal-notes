# Esempi query KQL

## Sort columns, specifying only the first ones to show

Use `project-reorder`.

## Contains Case sensitive

Use `contains_cs`

## Filter by time range

Use the `between` operator:

```kql
where timestamp between (todatetime("9/28/2023, 9:41:28.577 AM") .. todatetime("9/28/2023, 9:45:28.577 AM"))
```

The date is in the _mese/giorno/anno_ format.

By default, the time is in UTC (2hours behind).

You can use `now()` to define a filter from the current instant:

```kql
where timestamp between (now(-60d) .. now())
```

## Create a new computed field

Use `extend`:

```kql
extend  lastpart_ = split( operation_Name, "/")[-1]
```

## Take the last part of a string

Use the `split` operator to split the string by a certain charachter, then access the parts using `[position]`.

```kql
extend  lastpart_ = split( operation_Name, "/")[-1]
```

You can access the last part using  _-1_.

## Visualize a pie chart

After a `summarize` over a field, use

```kql
render piechart
```

## Parse a text

Use the `parse` operator on a string, and automatically replace parts that match a part of the message

```kql
parse message with '[HTTP TRACE - '_type_' - '_endpoint_']'
```

This way you read the messages, and it auto populates the `_type_` and `_endpoint_` values obtained from the substitution.

## Check if a field belongs to a list of values

Use the `in` operator:

```kql
| where _type_ in ("RESPONSE", "REQUEST")
```

## Group values based on a field

Use `make_list`, specifying what hte list must contains and what is the key used for grouping.

```kql
summarize make_list(_type_) by operation_Id,
```

From the main table, it groups by `operation_Id` and stores in the list all the values for `_type_`.

Note: the result is a `dynamic` type. Data inside the list do not have a static type.

You can give the list a name by assigning it to a field:

```kql
summarize ls_ = make_list(timestamp) by operation_Id
```

## Save the query result in a temporary table

You can save the result in a valiable using the `let` operator, and then reuse it in a following query.

**Note: the first query must end with `;`.**

```kql
let tab_ = traces
| take 10;
tab_
| where message !has "ciao"
```

## Join two tables

Use the `join` operator choosing the type of join and the field used as a key s

```kql
traces
| join kind=inner failedOperationIds_ on operation_Id
```

## Has vs Contains

`has` is more performant than `contains`, but it does not look for substrings (only full words).

If the operation_Name is é "DequeueMessageHandler", using

```kql
traces
| where operation_Name has "Dequeue"
```

I don't get anything, as "Dequeue" is not a single world in the message.

On the contrary, using

```kql
traces
| where operation_Name contains "Dequeue"
```

I get what I'm looking for, because I look at substrings.

## User-defined functions

You can create custom functions to use in the query.

```kql
let HasSms = (arg0: string) { arg0 has "Sending SMS has been successfully sent" };
traces
    | where HasSms(message)
```

## Convert the first value of an array into a single element

Use `toscalar`.

```kql
let startDate = toscalar (traces
| where operation_Id == operationId
| order by timestamp asc
| project timestamp
| take 1);
```

note the `take 1`.
