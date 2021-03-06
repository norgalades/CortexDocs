# Configuration

The Cortex back-end looks for its configuration in the same file (`/etc/cortex/application.conf` by default).

In order to start Cortex, the only required parameter is the key of the server
(`play.http.secret.key`). This key is used to authenticate the cookies that
contain data, and not only a session ID. If Cortex runs in cluster mode, all
instances must share the same key.

You should generate a random key using the following command line:

```
sudo mkdir /etc/cortex
(cat << _EOF_
# Secret key
# ~~~~~
# The secret key is used to secure cryptographics functions.
# If you deploy your application to several instances be sure to use the same key!
play.http.secret.key="$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 64 | head -n 1)"
_EOF_
) | sudo tee -a /etc/cortex/application.conf

```

Please, note that this secret key is mandatory to start the Cortex application. With this configuration, you will only be
able to run analyzers that do not require any configuration parameter, an API key for instance. To configure other
analyzers, refer to their [guide](../installation/analyzers.md).

**Warning**: By default, Cortex runs an HTTP service on port `9001/tcp`. You can
change the port by adding `http.port=8080` in the configuration file or add the
`-Dhttp.port=8080` parameter to the command line below. If you run Cortex using
a non-privileged user, you can't bind a port under 1024. If you run TheHive on
the same system, make sure that you are using two different TCP ports.

# Cortex application

## Initial configuration

### Elasticsearch configuration

## HTTPS

# First access

See [](userManagement#first_access_configure_cortex_administrator)

# Important Note

With introduction of users management, a key API is henceforth mandatory to request Cortex from TheHive or any other solution.  
