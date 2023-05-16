# Metadata

The edge functions on Edge Firewall have access to a set of metadata that can be manipulated to:

- Filter and manage access to your application.
- Apply specific logic in different scenarios.

This reference documentation describes the available metadata and their usage.

## GeoIP

The GeoIP information data on the geographical location of the client based on IP data.

|  Name                            | Description                                                    |
|----------------------------------|----------------------------------------------------------------|
|  geoip_asn                       | GeoIP information                                              |
|  geoip_city                      | GeoIP information                                              |
|  geoip_city_continent_code       | GeoIP information                                              |
|  geoip_city_country_code         | GeoIP information                                              |
|  geoip_city_country_name         | GeoIP information                                              |
|  geoip_continent_code            | GeoIP information                                              |
|  geoip_country_code              | GeoIP information                                              |
|  geoip_country_name              | GeoIP information                                              |
|  geoip_region                    | GeoIP information                                              |
|  geoip_region_name               | GeoIP information                                              |

### Usage

```javascript
    async function firewallHandler(event){
        // Access the country code through geoip
        let countryCode = event.request.metadata["geoip_country_code"]

        // Do some logic here
        // In this example, we are blocking access from Brazil
        if (countryCode === "BR"){
            event.deny();
        }

        // Then, if it comes from any other country,
        // the processing continues
        event.continue();
    }

    addEventListener("firewall", (event)=>event.waitUntil(firewallHandler(event)));
```

## Remote

The remote metadata provides details about the remote client's IP address and TCP port.


|  Name                            | Description                                                    |
|----------------------------------|----------------------------------------------------------------|
|  remote_addr                     | Remote (client) IP address                                     |
|  remote_port                     | Remote (client) TCP port                                       |
|  remote_user                     | User informed in the URL. Example: user in http://user@site.com/ |

### Usage

```javascript
    async function firewallHandler(event){
        // Access the country code through geoip
        let countryCode = event.request.metadata["geoip_country_code"]

        // Do some logic here
        // In this example, we are blocking access from Brazil
        if (countryCode === "BR"){
            event.deny();
        }

        // Then, if it comes from any other country,
        // the processing continues
        event.continue();
    }

    addEventListener("firewall", (event)=>event.waitUntil(firewallHandler(event)));
```


## Server

|  Name                            | Description                                                    |
|----------------------------------|----------------------------------------------------------------|
|  server_protocol                 | Protocol being used in the request. Example: HTTP/1.1            |

### Usage

```javascript
    async function firewallHandler(event){
        // Access the country code through geoip
        let countryCode = event.request.metadata["geoip_country_code"]

        // Do some logic here
        // In this example, we are blocking access from Brazil
        if (countryCode === "BR"){
            event.deny();
        }

        // Then, if it comes from any other country,
        // the processing continues
        event.continue();
    }

    addEventListener("firewall", (event)=>event.waitUntil(firewallHandler(event)));
```
 
## SSL

The SSL-related metadata is available when the request is made over a secure TLS/SSL connection.

|  Name                            | Description                                                    |
|----------------------------------|----------------------------------------------------------------|
|  ssl_cipher                      | TLS/SSL cipher used                                            |
|  ssl_protocol                    | TLS/SSL protocol used                                          |

### Usage

```javascript
    async function firewallHandler(event){
        // Access the country code through geoip
        let countryCode = event.request.metadata["geoip_country_code"]

        // Do some logic here
        // In this example, we are blocking access from Brazil
        if (countryCode === "BR"){
            event.deny();
        }

        // Then, if it comes from any other country,
        // the processing continues
        event.continue();
    }

    addEventListener("firewall", (event)=>event.waitUntil(firewallHandler(event)));
```
