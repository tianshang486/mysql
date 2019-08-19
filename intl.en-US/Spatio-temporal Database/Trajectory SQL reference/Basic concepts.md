# Basic concepts {#concept_tx2_52c_5gb .concept}

|Concept|Description|
|-------|-----------|
|trajectory point|The spatio-temporal object that consists of the spatial location and attributes of a moving object at a time point. The spatial location can be represented by 2D or 3D coordinates. The attributes support multiple fields of different types.|
|trajectory object|The high-dimensional object that consists of a series of trajectory points and events, including time, space, attributes, and events.|
|trajectory timeline|The time value sequence of a trajectory object.|
|trajectory spatial|The spatial geometry object of a trajectory object, which is of the linestring type.|
|trajectory leaf|The spatial location of a moving object \(which is a trajectory point\) at a time point.|
|trajectory attributes|The attributes of a moving object at different trajectory points, such as the velocity and direction.|
|trajectory attribute field|The attribute field of a trajectory object, such as the velocity field. The number of values of an attribute field is the same as the number of trajectory points.|
|trajectory field value|The value of a trajectory attribute field at a time point.|
|trajectory events|The events that occur in a trajectory, such as refueling, breakdown, and car lock events in the trajectory of a car. A trajectory event consists of the event type ID and event time.|

The following figure shows a trajectory object.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/124633/156620876438819_en-US.png)

