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
<pre>redis 127.0.0.1:6379> lrange sensordata.shackspace.20745965.data.L1.Voltage -10 -1
 1) "[1360608494,235.08]"
 2) "[1360608496,235.28]"
 3) "[1360608498,235.09]"
 4) "[1360608500,235.27]"
 5) "[1360608502,235.27]"
 6) "[1360608504,235.44]"
 7) "[1360608506,235.40]"
 8) "[1360608508,235.60]"
 9) "[1360608510,235.66]"
10) "[1360608512,235.62]"</pre>

