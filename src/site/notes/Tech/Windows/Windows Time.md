---
{"dg-publish":true,"permalink":"/tech/windows/windows-time/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# Query Current Time Source

```powershell
w32tm /query /source
```

also

```powershell
 w32tm /query /peers
 ```

# Resync Time

```powershell
w32tm /resync
```

[Secure Time Seeding – improving time keeping in Windows](https://docs.microsoft.com/en-in/archive/blogs/w32time/secure-time-seeding-improving-time-keeping-in-windows)

## Manual ReSync From pool.ntp.org

```powershell
w32tm /config /syncfromflags:manual /manualpeerlist:"pool.ntp.org"
```

# Time Sync for a Remote Workforce

https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/domain-time-synchronization-in-the-age-of-working-from-home/ba-p/1440820

# [[Tech/Windows/Windows|Windows]] NTP Client Flags

The best documentation I can find for what the flags mean is here:

[https://docs.microsoft.com/en-us/openspecs/windows_protocolsms-sntp/fef409e4-5297-4f18-850b-e386f7e10fea](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-sntp/fef409e4-5297-4f18-850b-e386f7e10fea)

The flags are a hex bitmask:

- 0x01 SpecialInterval - The value of the **SpecialPollInterval** element is used as the polling interval for this time source.

- 0x02 UseAsFallbackOnly - Use this time source only when all other time sources have failed. No preference is given among fallback time sources when multiple time sources are configured with this option.

- 0x04 SymmetricActive - Use the symmetric active mode when communicating with this time source.

- 0x08 Client - Use the client mode when communicating with this time source.

So 0xb is:

- 0x01 SpecialInterval
- 0x02 UseAsFallbackOnly 
- 0x08 Client

[https://docs.microsoft.com/en-us/archive/blogs/w32time/configuring-the-time-service-ntpserver-and-specialpollinterval](https://docs.microsoft.com/en-us/archive/blogs/w32time/configuring-the-time-service-ntpserver-and-specialpollinterval)

[https://docs.microsoft.com/en-us/archive/blogs/askds/configuring-your-pdce-with-alternate-time-sources](https://docs.microsoft.com/en-us/archive/blogs/askds/configuring-your-pdce-with-alternate-time-sources)

Multiple time sources are delineated by a space. For two time sources, the following form would be used:

 `<Time Source #1>[,<Bitwise Flags #1>] <Time Source #2>[,<Bitwise Flags #2>]`
