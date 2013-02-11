
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

#### Intend: data
Namespace below intend consists of each sensor's unique id.

sensordata.shackspace.20745965.config
	SET
		sensors = {
								"L1.Voltage": {unit: "V", type:"actual" },
								"L1.Current": {unit: "V", type:"actual" },
								"L1.Power": {}
								"L2.Voltage"
								"L2.Current"
								"L2.Power"
								"L3.Voltage"
								"L3.Current"
								"L3.Power"
								"Total": {unit: "W", type:"cummulative"}
								}
	
sensor.shackspace.20745965.data
	SSET
		score = unixtime
		data = 
