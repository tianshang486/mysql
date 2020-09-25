# ST\_Tile

This topic describes the ST\_Tile function, which generates a MVT-formatted standard binary structure based on a tile ID from a pyramid.

## Syntax

```
bytea ST_Tile(cstring name, cstring key);
bytea ST_Tile(cstring name, int x, int y, int z);
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|name|The name of the pyramid.|
|key|The ID of the tile.|
|x|The x value in the tile ID.|
|y|The y value in the tile ID.|
|z|The z value in the tile ID.|

## Description

This function returns a MVT-formatted standard binary structure that is generated based on a tile ID from a pyramid. The tile ID follows the `'z_x_y'` format and the `EPSG:3857` geographic coordinate system.

## Examples

```
select ST_Tile('roads', '3_1_6');
st_tile
----------
0xFFAABB8D8A6678...

select ST_Tile('roads', 1, 6, 3);
st_tile
----------
0xFFAABB8D8A6678...
```

