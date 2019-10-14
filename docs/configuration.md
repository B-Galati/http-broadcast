# Configuration

The HTTP Broadcaster follows [the twelve-factor app methodology](https://12factor.net/)
and is configurable using [environment variables](https://en.wikipedia.org/wiki/Environment_variable):

### Configuration

| Variable                      | Required/Default | Description |
|-------------------------------|------------------|-------------|
| `AGENT_ENDPOINT`              | _undefined_      | the address to broadcast requests to (example: `127.0.0.1:6800`). When not defined, the broadcaster will only listen on requests. `SERVER_ADDR` or `AGENT_ENDPOINT` is required. |
| `AGENT_RETRY_DELAY`           | `60s`            | maximum duration for retrying the replay of the request.                                                                                                                         |
| `DEBUG`                       | `0`              | set to `1` to enable the debug mode (prints recovery stack traces).                                                                                                              |
| `HUB_ENDPOINT`                | **required**     | the address of the the mercure hub to push and fetch messages (example: `https://example.com/hub`).                                                                              |
| `HUB_GUARD_TOKEN`             | =`HUB_TOPIC`     | the token used to prevent infinite loop (in case an agent broadcast request to iteself).                                                                                         |
| `HUB_PUBLISH_TOKEN`           | =`HUB_TOKEN`     | valid JWT token to allow publishing.                                                                                                                                             |
| `HUB_SUBSCRIBE_TOKEN`         | =`HUB_TOKEN`     | valid JWT token to allow subscribing.                                                                                                                                            |
| `HUB_TIMEOUT`                 | `5s`             | maximum duration for pushing the message into the HUB, set to `0s` to disable.                                                                                                   |
| `HUB_TOKEN`                   | **required**     | valid JWT token to allow both publishing and subscribing. On could use [this example](https://jwt.io/#debugger-io?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJtZXJjdXJlIjp7InN1YnNjcmliZSI6WyJodHRwLWJyb2FkY2FzdCJdLCJwdWJsaXNoIjpbImh0dHAtYnJvYWRjYXN0Il19fQ._CEt9vXo2zGHSRTmd6LkoOYEtT014m75AVBn9KfA2Go) to generate a new one|
| `HUB_TOPIC`                   | `http-broadcast` | name of the Mercure's topic to exchange messages. This parameter can also be defined with by the queryString of `HUB_ENDPOINT`. example `HUB_ENDPOINT=https://example.com/hub?topic=my_topic`. |
| `LOG_FORMAT`                  | `text`           | the log format, can be `json`, `fluentd` or `text`.                                                                                                                              |
| `LOG_LEVEL`                   | `info`           | the log verbosity, can be `trace`, `debug`, `info`, `warn`, `error`, `fatal`.                                                                                                    |
| `SERVER_ADDR`                 | _undefined_      | the address to listen on (example: `0.0.0.0:6081`). When not defined, the broadcaster will only pusblish requests. `SERVER_ADDR` or `AGENT_ENDPOINT` is required.                |
| `SERVER_CORS_ALLOWED_ORIGINS` | _undefined_      | a comma separated list of allowed CORS origins, can be `*` for all.                                                                                                              |
| `SERVER_INSECURE`             | =`DEBUG`         | trust everyone in [ProxyProtocol](https://www.haproxy.org/download/1.8/doc/proxy-protocol.txt).                                                                                  |
| `SERVER_READ_TIMEOUT`         | `0s`             | maximum duration before timing out writes of the response, set to `0s` to disable, example: `2m`.                                                                                |
| `SERVER_TLS_ACME_ADDR`        | `:http`          | the address use by the acme server to listen on (example:  `0.0.0.0:8080`).                                                                                                      |
| `SERVER_TLS_ACME_CERT_DIR`    | _undefined_      | the directory where to store Let's Encrypt certificates.                                                                                                                         |
| `SERVER_TLS_ACME_HOSTS`       | _undefined_      | a comma separated list of hosts for which Let's Encrypt certificates must be issued.                                                                                             |
| `SERVER_TLS_CERT_FILE`        | _undefined_      | a cert file (to use a custom certificate).                                                                                                                                       |
| `SERVER_TLS_KEY_FILE`         | _undefined_      | a key file (to use a custom certificate).                                                                                                                                        |
| `SERVER_TRUSTED_IPS`          | _undefined_      | list of trusted ips which lead to remote client address replacement in [ProxyProtocol](https://www.haproxy.org/download/1.8/doc/proxy-protocol.txt).                             |
| `SERVER_WRITE_TIMEOUT`        | `0s`             | maximum duration for reading the entire request, including the body, set to `0s` to disable, example: `2m`.                                                                      |

## Next step

[Cookbooks](cookbooks.md)