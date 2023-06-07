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



## Remote

The remote metadata provides details about the remote client's IP address and TCP port.


|  Name                            | Description                                                    |
|----------------------------------|----------------------------------------------------------------|
|  remote_addr                     | Remote (client) IP address                                     |
|  remote_port                     | Remote (client) TCP port                                       |
|  remote_user                     | User informed in the URL. Example: user in http://user@site.com/ |

## Server

|  Name                            | Description                                                    |
|----------------------------------|----------------------------------------------------------------|
|  server_protocol                 | Protocol being used in the request. Example: HTTP/1.1            |
 
## SSL

The SSL-related metadata is available when the request is made over a secure TLS/SSL connection.

|  Name                            | Description                                                    |
|----------------------------------|----------------------------------------------------------------|
|  ssl_cipher                      | TLS/SSL cipher used                                            |
|  ssl_protocol                    | TLS/SSL protocol used                                          |

## Usage

You can access the metadata through `event.request.metadata["remote_addr"]`, such as :

```javascript
    let ip = event.request.metadata["remote_addr"] // Accessing the remote address

```

### Implementation

In the code sample below: 

- The remote address is accessed.
- It's verified if this address is in a network list.
- If it's in the network list, the request is denied.

```javascript
     addEventListener("firewall", (event) => {

      let ip = event.request.metadata["remote_addr"] // Accessing the remote address

      try {
        let found = Azion.networkList.contains(String(networkListId), ip); // Checking if the ip is in the list
        if (found) {
          event.deny(); // If it's in the list, deny the request
        }
      } catch (err) {
        event.console.error(`Error: `, err.stack);
      }
    });
```
