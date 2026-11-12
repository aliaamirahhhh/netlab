##LAB 4
1. Why did the first firewall rule in Step 3 have no effect, and why does blocking h1 → h3 also break h3 → h1?
   - The first firewall rule had no effect since it had the same default priority as the existing forwarding rule (32768). Both rules matched the packet and OpenFlow does not guarantee which overlapping rule it chooses, thus the forwarding rule was chosen first. To overcome this, the firewall's priority was increased for it to take precedence.
   - Blocking h1 -> h3 also breaks h3 -> h1 since pings require both Echo Requestand Echo Reply. While the firewall rule blocks packets from h1 to h3, it also blocks Echo Replies sent by h1 when h3 initiates a ping, thus causing the ping to fail.
  
2. In Step 5, why did one conversation survive the controller failure and another didn't?
   - The conversation between h1 -> h2 survived since there was already a forwarding rule in the switch's flow table. It's stored in cache until its idle timeout of 60 seconds expires. While the h1 -> h3 conversation was never established, thus the switch could not obtain any instructions to forward the packet.
  
3. Secure or standalone: which would you choose for a campus network, and what does the other one cost you?
   - I would choose Secure mode for more security and a more centralised network management, since it does not automatically fallback to Standalone mode, preventing unauthorized and or unexpected behavior. Although the Standalone mode would be helpful to provide network availability when a controller fails, redundant controllers is to be applied in a Secure mode to reduce the risk of network disruption.
