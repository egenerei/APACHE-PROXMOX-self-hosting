# Grafana's configuration

## Edit grafana.ini to fit your server
```yaml
#################################### Server ####################################
[server]
# Protocol (http, https, h2, socket)
;protocol = http

# Minimum TLS version allowed. By default, this value is empty. Accepted values are: TLS1.2, TLS1.3. If nothing is set TLS1.2 would be taken
;min_tls_version = ""

# The ip address to bind to, empty will bind to all interfaces
http_addr = 127.0.0.1

# The http port to use
http_port = 3000

# The public facing domain name used to access grafana from a browser
domain = grafana.egenerei.es

# Redirect to correct domain if host header does not match domain
# Prevents DNS rebinding attacks
;enforce_domain = false

# The full public facing url you use in browser, used for redirects and emails
# If you use reverse proxy and sub path specify full url (with sub path)
root_url = %(protocol)s://%(domain)s:%(http_port)s/
```
