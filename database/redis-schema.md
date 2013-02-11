# shackspace redis schema
## Sensor Data Store
### Namespace Hierarchy
<pre>
Level 0: Logic Group ("sensordata")
Level 1: Location ("shackspace")
Level 2: Unique Sensor ID (eg. "20745965" for the shackspace mains power meter)
Level 3: Intend (eg. "config" for static configuration data or "data" for recorded data)
Level 4+: Different meanings depending on Level 3
</pre>

#### Intend: config
Type: SET

Key: sensors

Value: JSON

<pre>{ "[sensor channel unique id]": { unit: "[SI unit]", type: "[sensor type]" }</pre>

Sensor types may include: "actual", "cummulative", "minimum", "maximum", "average".

##### Example
<pre>redis 127.0.0.1:6379> get sensordata.shackspace.20745965.config.sensors
"{\"L1.Voltage\": {\"unit\": \"V\", \"type\":\"actual\"},
\"L2.Voltage\": {\"unit\": \"V\", \"type\":\"actual\"},
\"L3.Voltage\": {\"unit\": \"V\", \"type\":\"actual\"},
\"L1.Current\": {\"unit\": \"A\", \"type\":\"actual\"},
\"L2.Current\": {\"unit\": \"A\", \"type\":\"actual\"},
\"L3.Current\": {\"unit\": \"A\", \"type\":\"actual\"},
\"L1.Power\": {\"unit\": \"W\", \"type\":\"actual\"},
\"L2.Power\": {\"unit\": \"W\", \"type\":\"actual\"},
\"L3.Power\": {\"unit\": \"W\", \"type\":\"actual\"},
\"Total\": {\"unit\": \"W\", \"type\":\"cummulative\"}}"
</pre>

#### Intend: data
Type: LIST

Namespace below intend consists of each sensor's unique id as defined `sensordata.shackspace.*.config.sensors`.

Data is stored as JSON array with the first element being unixtime and the second the sensor value.

##### Example
<pre>redis 127.0.0.1:6379> lrange sensordata.shackspace.20745965.data.L1.Power -10 -1
 1) "[1360609006,01195]"
 2) "[1360609008,01200]"
 3) "[1360609010,01208]"
 4) "[1360609012,01178]"
 5) "[1360609014,01184]"
 6) "[1360609016,01199]"
 7) "[1360609018,01215]"
 8) "[1360609020,01215]"
 9) "[1360609022,01193]"
10) "[1360609024,01199]"
</pre>

