# shackspace interactive information display
## Source
You can find the source code for this project at http://github.com/hdznrrd/siid

## Data Path
### Capture and Storage
All sensor data is captured and stored into a central [redis](http://redis.io/) database running on glados.shack.
The database schema is documented in more detail in [database/redis-schema.md](database/redis-schema.md).

### Processing and Preparation
Processing to make data suitable for plotting on the presentation frontend is done using various [apps](https://github.com/hdznrrd/siid/tree/master/apps).
Apps are triggered from the presentation layer.

### Presentation
Plotting is done using the [g.raphaeljs](http://g.raphaeljs.com/) library.
[twitter Bootstrap](twitter.github.com/bootstrap) is used for quick and easy prototyping of the GUI.

## Setting up siid
The following two are required but not handled by siid

- A redis instance to hold captured data
- A means to capture data and push it to redis


### Installation

<pre>apt-get install lighttpd python python-pip
pip install redis
cd /var/www/
git clone git://github.com/hdznrrd/siid.git</pre>

Now [configure your lighttpd](lighttpd/README.md).
