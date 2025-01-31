# Analyze Network Layer Communication

## Overview

This repository contains an analysis of network layer communication, focusing on the examination of DNS and ICMP traffic using data from a network protocol analyzer tool. The primary objective is to identify network protocol issues and assess the cybersecurity incident affecting a client.

## Problem Summary

From the tcpdump log analysis, it was observed that multiple users were unable to access the website `www.yummyrecipesforme.com`. The error message "destination port unreachable" was received when attempting to access the website. Further analysis of network traffic using `tcpdump` revealed that UDP packets sent to the DNS server resulted in ICMP responses indicating "udp port 53 unreachable."

## Data Analysis

1. **Initial Request:**

   - The browser sent a DNS request (UDP packet) to resolve the domain name.
   - The request was directed to the DNS server at IP `203.0.113.2`.

2. **ICMP Error Response:**

   - The DNS query resulted in an ICMP error message from the destination IP `203.0.113.2`.
   - The error message stated: "udp port 53 unreachable," indicating that the DNS server was not responding.

3. **Repeated Failures:**

   - The log captured multiple retries of the DNS query, all resulting in the same ICMP error.
   - This confirmed a consistent issue with the DNS resolution process.

## Possible Cause

The issue appears to be caused by an **inaccessible or misconfigured DNS server** at `203.0.113.2`. This could be due to:

- The DNS service being down or misconfigured.
- A firewall or security policy blocking access to port 53.
- Network congestion or infrastructure failure affecting the DNS server’s availability.

## Next Steps

- Verify the DNS server status and configuration.
- Check firewall rules and network policies that may be blocking UDP port 53.
- Perform a traceroute to `203.0.113.2` to identify any routing issues.
- Attempt DNS resolution using an alternative DNS server.

## Usage

To analyze network traffic, use `tcpdump`:

```sh
sudo tcpdump -i eth0 -nn udp port 53
```

This will capture DNS requests and responses for further investigation.

## Conclusion

Analyzing network layer communication is crucial in diagnosing and mitigating network-related cybersecurity incidents. This repository provides insights into troubleshooting DNS-related issues and ensuring uninterrupted service availability.



