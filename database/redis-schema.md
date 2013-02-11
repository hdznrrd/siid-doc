
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
<pre>{ "<sensor channel unique id>": { unit: "<SI unit>", type: "<sensor type>" }</pre>

Sensor types may include: "actual", "cummulative", "minimum", "maximum", "average".

##### Example
<pre>
sensordata.shackspace.20745965.config
		sensors = {
								"L1.Voltage": {unit: "V", type:"actual" },
								"L1.Current": {unit: "A", type:"actual" },
								"L1.Power": {unit: "W", type:"actual" },
								"L2.Voltage": {unit: "V", type:"actual" },
								"L2.Current": {unit: "A", type:"actual" },
								"L2.Power": {unit: "W", type:"actual" },
								"L3.Voltage": {unit: "V", type:"actual" },
								"L3.Current": {unit: "A", type:"actual" },
								"L3.Power": {unit: "W", type:"actual" },
								"Total": {unit: "W", type:"cummulative"}
								}
</pre>

#### Intend: data
Namespace below intend consists of each sensor's unique id.
The data store is implemented as `sorted set` with the unix time as score value and sensor value being the actual value.

##### Example
<pre>redis 127.0.0.1:6379> .shackspace.20745965.data.L1.Voltage 0 -1 withscores
  1) "233.35"
  2) "1360603257"
  3) "233.75"
  4) "1360603259"
  5) "234.47"
  6) "1360603587"</pre>

