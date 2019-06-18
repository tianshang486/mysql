# Basic concepts {#concept_x5z_4rd_5gb .concept}

|Concept|Description|
|-------|-----------|
|raster object|The regular grid that represents a space. Each cell in a raster object is assigned an attribute value. A raster object can be a satellite image, a digital elevation model \(DEM\), or a picture.|
|raster cell|The cell in a raster object, which is also called a pixel.|
|band|The layer of cell value matrix in a raster object. A raster object can have multiple bands.|
|chunk|The portion of a raster object. The size of a chunk can be customized, such as 256 × 256 × 3.|
|pyramid|The downsampled version of a raster object. A pyramid can contain multiple downsample layers. Consecutive pyramid layers are downsampled at a scale of 2:1.|
|pyramid level|The level in a pyramid.|
|mosaic|The operation to integrate multiple raster objects into an existing raster object.|
|interleaving|The arrangement of pixels in a raster object. The interleaving types include band sequential \(BSQ\), band interleaved by pixel \(BIP\), and band interleaved by line \(BIL\).|
|world space|The world coordinates \(geographic coordinates\) of a raster object.|
|raster space|The pixel coordinates of a raster object.|

