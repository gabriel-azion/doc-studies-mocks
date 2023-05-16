# Network List interface

The `Azion.networkList.contains()` interface can be used by edge functions on Edge Firewall to match an IP address against a specified network list. If the IP address informed is within the network list, it returns `true` and the desired implementation logic can go on based on that information.

## Syntax

```javascript
    Azion.networkList.contains(networklistID, ip)
```

- `ipAddress (string)`: The IP address to be matched against the network list.
- `networkListId (string)`: The ID of the network list to be used for matching.

## Return Value

`bool`: Returns `true` if the IP address is in the network list and `false` if it's not.

## Usage

Example 1: Basic usage of networklists_match() with a specific IP address and network list ID:

```javascript
    addEventListener("firewall", (event) => {

        let ipsToCheck = [event.request.metadata["remote_addr"]] // Accessing the remote address

        for (const ip of ipsToCheck) {
            try {
                let found = Azion.networkList.contains(String(networkListId), ip); // Checking if the ip is in the list
                if (found) {
                    event.deny(); // If it's in the list, deny the request
                }
            } catch (err) {
                event.console.error(`Error: `, err.stack);
            }
        }
    });
```

## Integration with Edge Firewall and Edge Functions

To integrate the `Azion.networkList.contains()` interface with the Edge Firewall and Edge Functions, you can place the function call within your code passing the IP address and the ID of the network list you wish to use. The return of the function call can be used to make decisions about blocking or allowing requests based on the defined criteria.

## Error Handling

If an error occurs during the execution of `Azion.networkList.contains()`, an exception may be thrown. Make sure to handle potential errors and provide appropriate error messages or fallback actions in your code.

## Best Practices

- Regularly update and maintain the network lists to ensure accurate matching and minimize false positives or false negatives.
- Combine network list matching with other security measures for comprehensive protection.

## Security Considerations

- Ensure the integrity and security of the network lists to prevent unauthorized modifications or access.
- Regularly review and update the network list configurations to address changing security threats and requirements.

## Limitations and Constraints

- The effectiveness of network list matching depends on the quality and coverage of the network lists you define.

tchananaaam