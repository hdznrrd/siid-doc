# lighttpd config for siid

- deploy siid in WEBROOT/siid/
- enable cgi support
- allow cgi for .py files in WEBROOT/siid/apps/

<pre>
server.modules += ( "mod_cgi" )
server.breakagelog = "/var/log/lighttpd/breakage.log"
static-file.exclude-extensions += ( ".py" )
$HTTP["url"] =~ "^/siid/apps" {
        cgi.assign = ( ".py" => "/usr/bin/python" )
}</pre>
