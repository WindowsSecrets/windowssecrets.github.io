---
layout: default
permalink: /increaseNetworkSpeed/
title: Increase Network Speed
---
[Go Back to Main](https://windowssecrets.github.io)
# Increase Network Speed

## IRPStackSize

IRPStackSize (I/O Request Packet Stack Size) basically represents how many 36-byte receive buffers your computer can use simultaneously. It allows your computer to receive more data at the same time. If you have a large Internet connection (more than 10 Mbps), you’ll benefit from this. For those of you with smaller Internet connections, you might not notice even the slightest difference, so skip this.
Your system usually allocates 15 IRPs in its network stack. More often than not, you’d benefit much more with 32, although you can configure up to 50. Try 32 first.
Here’s the location of the key in your registry: 

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters
```

Add “IRPStackSize” as a DWORD value on the right hand side of the regedit window and modify the value to 32.

## SizReqBuf

SizReqBuf represents the size of the raw receive buffers within a server environment. This means that it will affect your ability to host something in a high-latency environment. Let’s say you host a game server and tons of people complain about lag. Modifying this value will help reduce the impact of lag. You’d also benefit if you’re hosting a website or any other service, including sending files through instant messenger or Neo Modus Direct Connect.

Your system usually places this buffer at 16384 bytes. For most servers, this is efficient enough, but sometimes you have a small amount of memory and cannot keep up with the high request volume.

Here’s the location of the key in your registry: 

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters
```

Add “SizReqBuf” as a DWORD value on the right hand side of the regedit window. If you have a server with over 512 MB of physical memory, modify the value to 17424. If you have less than 512 MB of memory, you should consider getting a new computer, but you can modify this value in the meantime to 4356.

## DefaultTTL

Time to Live (TTL) tells routers how long a packet should stay in the air while attempting delivery before giving up and discarding the packet. When the value is often high, your computer spends more time waiting for a failed packet to deliver, effectively decreasing the amount of productivity in your network.

Without a value set, Windows waits 128 seconds for the transaction to finish. This makes your computer lag terribly if you’re in the middle of something and your connection with a server unexpectedly goes south.

Here’s the location of the key in your registry: 

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
```

Add “DefaultTTL” as a DWORD value within the “Parameters” key. Set the value to anything between 1 and 255. The best value is 64, although you can set lower values if you wish to have the packet killed more quickly.

## References

1. https://www.maketecheasier.com/3-ways-to-increase-network-speed-via-registry-editor-windows/
2. http://www.speedguide.net/articles/windows-8-10-2012-server-tcpip-tweaks-5077
3. https://technet.microsoft.com/pt-br/library/cc739819(v=ws.10).aspx
4. http://subinsb.com/default-device-ttl-values
