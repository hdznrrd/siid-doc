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
