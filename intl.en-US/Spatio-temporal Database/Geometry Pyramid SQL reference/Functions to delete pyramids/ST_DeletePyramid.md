# ST\_DeletePyramid

This topic describes the ST\_DeletePyramid function, which deletes a vector pyramid.

## Syntax

```
boolean ST_DeletePyramid(cstring  name)
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|name|The name of the pyramid that you want to delete.|

## Examples

```
--Delete a pyramid.
select ST_DeletePyramid('roads');
st_deletepyramid
----------
t
```

