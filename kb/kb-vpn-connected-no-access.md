# KB VPN connected but no access DNS and routing

## Summary
When VPN connects but internal resources do not work, isolate whether the issue is DNS resolution or routing.

## Applies to
Windows 10 and Windows 11 endpoints using a VPN client

## Steps
1: Test internal hostname and internal IP
If the internal IP works but hostname fails, it is usually DNS.
If both fail, it is usually routing or policy.

2: Verify DNS servers and DNS suffix
Run ipconfig all and confirm VPN adapter DNS points to internal DNS servers.
Run nslookup and confirm internal names resolve.

3: Verify routes to internal subnets
Run route print and confirm routes exist for private subnets through the VPN interface.

4: Validate service ports
Use Test NetConnection to verify port reachability for the required service.

## Notes
Split tunneling can cause some subnets to bypass VPN.
Local firewall rules can block internal traffic after VPN connects.

## Verification
Internal hostname resolves via internal DNS.
Internal services are reachable on required ports.
User confirms access to required resources.
