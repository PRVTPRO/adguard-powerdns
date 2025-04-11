## 🚀 Build and launch 
1) Cloning repositories 
2) Let's make our own changes .env
``
# Adam-PowerDNS Panel-Administrator
ADMIN_PDNS_API_KEY=api-secret-authoritative
ADMIN_USER_PASSWORD=very secret

# Panel database
ADMIN_DB_PASSWORD=The PDA

# PowerDNS is Reputable
AUTHORITATIVE_API_KEY=api-secret-authoritative
AUTHORITATIVE_WEB SERVER_PASSWORD=web secret-authoritative

# PowerDNS database
AUTHORITATIVE_DB_PASSWORD=IDENTIFICATION data

```
3) We do what is necessary

Build and launch all the services
``
docker-compose -build -d
' `
If the images already exist and do not need to be reassembled:
``
docker layout
```
For the girl, only the administrator:
``
docker is the administrator of the compose build
```
For the authoritative:
``
authoritative docker-compose build

Then you can do the following:

    #change .env_sample to .env and replace variable

    # start powerdns stack
    docker compose up -d
    
    # send DNS queries to Adguard Home 
    dig -p 53 example.com

    # PowerDNS admin interface
    http://localhost:3031
    
    # PowerDNS authoritative stats
    http://localhost:8081


It will be configured to receive DoH from the following points
    - https://dns10.quad9.net/dns-query
    - https://dns.google/dns-query
    - https://cloudflare-dns.com/dns-query
    - https://common.dot.dns.yandex.net/dns-query

Getting local zone records .corp will be directed to the internal PowerDNS authoritative
    - '[/corp/]172.31.118.118:53'


The configuration of the Adguard Home in upstream_mode: parallel mode is shown.
You can clear the adguard home folder and install it via the web panel yourself.


## 📁 Examples of directories

- `/authoritative/` — build scripts for PowerDNS Authoritative.
- `/admin/` — — build scripts for PowedDNSAdmin configuration and working files for AdGuard Home.
- `/adguardhome/` — storage of the AdGuard Home settings after startup.
- `docker-compose.yml` - compilation and launch of services.

## Variables to deploy

### Admin

| Env-Variable         | Description                                              |
| -------------------- | -------------------------------------------------------- |
| ADMIN_DB_HOST        | Postgres host (default: admin-db)                        |
| ADMIN_DB_NAME        | Postgres database (default: pda)                         |
| ADMIN_DB_PASS        | Postgres password (default: pda)                         |
| ADMIN_DB_PORT        | Postgres port (default: 5432)                            |
| ADMIN_DB_USER        | Postgres username (default: pda)                         |
| ADMIN_PDNS_API_KEY   | PowerDNS API key (default: pdns)                         |
| ADMIN_PDNS_API_URL   | PowerDNS API URL (default: http://authoritative:8081/)   |
| ADMIN_PDNS_VERSION   | PowerDNS version number (default: 4.9)                 |
| ADMIN_SIGNUP_ENABLED | Allow users to sign up (default: no)                     |
| ADMIN_USER_EMAIL     | Email address of admin user (default: admin@example.org) |
| ADMIN_USER_FIRSTNAME | First name of admin user (default: Administrator)        |
| ADMIN_USER_LASTNAME  | Last name of admin user (default: User)                  |
| ADMIN_USER_PASSWORD  | Password of admin user (default: admin)                  |


### Authoritative

| Env-Variable                              | Description                                                                                                                             |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| AUTHORITATIVE_ALLOW_AXFR_IPS              | Allow zonetransfers only to these subnets (default: 127.0.0.0/8,::1)                                                                    |
| AUTHORITATIVE_ALLOW_NOTIFY_FROM           | Allow AXFR NOTIFY from these IP ranges (default: 0.0.0.0/0,::/0)                                                                        |
| AUTHORITATIVE_API                         | Enable/disable the REST API (default: no)                                                                                               |
| AUTHORITATIVE_API_KEY                     | Static pre-shared authentication key for access to the REST API (default: pdns)                                                         |
| AUTHORITATIVE_DB_HOST                     | Postgres host (default: authoritative-db)                                                                                               |
| AUTHORITATIVE_DB_NAME                     | Postgres database (default: pdns)                                                                                                       |
| AUTHORITATIVE_DB_PASS                     | Postgres password (default: pdns)                                                                                                       |
| AUTHORITATIVE_DB_PORT                     | Postgres port (default: 5432)                                                                                                           |
| AUTHORITATIVE_DB_USER                     | Postgres username (default: pdns)                                                                                                       |
| AUTHORITATIVE_DEFAULT_KSK_ALGORITHM       | Default KSK algorithm (default: ecdsa256)                                                                                               |
| AUTHORITATIVE_DEFAULT_KSK_SIZE            | Default KSK size (default: 0)                                                                                                           |
| AUTHORITATIVE_DEFAULT_PUBLISH_CDNSKEY     | Default value for PUBLISH-CDNSKEY (default: )                                                                                           |
| AUTHORITATIVE_DEFAULT_PUBLISH_CDS         | Default value for PUBLISH-CDS (default: )                                                                                               |
| AUTHORITATIVE_DEFAULT_ZSK_ALGORITHM       | Default ZSK algorithm (default: )                                                                                                       |
| AUTHORITATIVE_DEFAULT_ZSK_SIZE            | Default ZSK size (default: 0)                                                                                                           |
| AUTHORITATIVE_DIRECT_DNSKEY               | Fetch DNSKEY, CDS and CDNSKEY RRs from backend during DNSKEY or CDS/CDNSKEY synthesis (default: no)                                     |
| AUTHORITATIVE_DISABLE_AXFR                | Disable zonetransfers but do allow TCP queries (default: yes)                                                                           |
| AUTHORITATIVE_DNAME_PROCESSING            | If we should support DNAME records (default: no)                                                                                        |
| AUTHORITATIVE_EXPAND_ALIAS                | Expand ALIAS records (default: no)                                                                                                      |
| AUTHORITATIVE_LOG_DNS_DETAILS             | If PDNS should log DNS non-erroneous details (default: no)                                                                              |
| AUTHORITATIVE_LOG_DNS_QUERIES             | If PDNS should log all incoming DNS queries (default: no)                                                                               |
| AUTHORITATIVE_LOGLEVEL                    | Amount of logging. Higher is more. Do not set below 3 (default: 4)                                                                      |
| AUTHORITATIVE_MASTER                      | Act as a master (default: no)                                                                                                           |
| AUTHORITATIVE_MAX_TCP_CONNECTION_DURATION | Maximum time in seconds that a TCP DNS connection is allowed to stay open (default: 0)                                                  |
| AUTHORITATIVE_MAX_TCP_CONNECTIONS         | Maximum number of TCP connections (default: 20)                                                                                         |
| AUTHORITATIVE_QUERY_LOGGING               | Hint backends that queries should be logged (default: no)                                                                               |
| AUTHORITATIVE_RECEIVER_THREADS            | Default number of receiver threads to start (default: 1)                                                                                |
| AUTHORITATIVE_RESOLVER                    | Use this resolver for ALIAS and the internal stub resolver (default: no)                                                                |
| AUTHORITATIVE_RETRIEVAL_THREADS           | Number of AXFR-retrieval threads for slave operation (default: 2)                                                                       |
| AUTHORITATIVE_REUSEPORT                   | Enable higher performance on compliant kernels by using SO_REUSEPORT allowing each receiver thread to open its own socket (default: no) |
| AUTHORITATIVE_SECURITY_POLL_SUFFIX        | Domain name from which to query security update notifications (default: secpoll.powerdns.com.)                                          |
| AUTHORITATIVE_SLAVE                       | Act as a slave (default: no)                                                                                                            |
| AUTHORITATIVE_SIGNING_THREADS             | Default number of signer threads to start (default: 3)                                                                                  |
| AUTHORITATIVE_TCP_FAST_OPEN               | Enable TCP Fast Open support on the listening sockets (default: 0)                                                                      |
| AUTHORITATIVE_WEBSERVER                   | Start a webserver for monitoring on port 8081 (default: no)                                                                             |
| AUTHORITATIVE_WEBSERVER_PASSWORD          | Password required for accessing the webserver (default: pdns)                                                                           |


A simple example of running Adguard Home and redirecting requests to the local PowerDNS authoritative and to external DoH providers.  This is just an example of a quick start. To get the best results, do the reconstruction yourself.