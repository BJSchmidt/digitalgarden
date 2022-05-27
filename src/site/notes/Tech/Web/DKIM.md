---
{"dg-publish":true,"permalink":"/tech/web/dkim/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# DKIM Overview

DKIM is an email authentication technology used to prevent forged sender addresses (email spoofing) by cryptographically verifying the presence of a domain name identifier in an email message. The message body and some parts of the message headers are cryptographically signed by the sender, which allows a domain to claim and prove responsibility for an email message, while also verifying the signed parts of the message have not changed in transit.

# Technical Details

DKIM works by adding one or more `DKIM-Signature:` header fields to an email when it gets sent. These `DKIM-Signature` blocks contain a series of tag=value pairs used to authenticate the message. The most relevant tag=value pairs are:

- Domain name identifier `d=contoso.com;`
- Selector `s=selector2;`
- List of signed header fields `h=from:to:subject:date;`
- Body hash `bh=AXj2kkirGGSYl+AtfjQWuscPhCA91QiwzIeIr86TpTI=;`
- and the signature of the headers and body `b=i3eAEvzyKZG9Vq/CcxxSqqi9dvmNVqzCurB3oJEoEPo+PwcYMH7UVF9CfcB614O1j3AWYoI/t5xRPcpR0ILWzNBwxfg4wIf7CLiCp7ks1qABAVpMs9GHP67sI6kQSV9IEAXTIi7DSfwk9bTC39zY8GcwGA/aUdl5EAFE50M8N/o=;`

On the receiving side cryptographic techniques are used to verify the message and sender. The cryptographic public key is in the sending domain's DNS, in the `selector._domainkey subdomain`. ie `selector1._domainkey.contoso.com` txt record. So DNS is queried using the domain name and the selector from the `DKIM-Signature:` header field to get a txt record that contains (among other things) the public part of the cryptographic keypair used to sign the message. The receiving mail system then uses the public key to validate the message. The results of this validation are added to the message headers in a new `authentication-results:` header field.

It should also be noted that DKIM allows for multiple selectors which allows the domain to publish multiple keys and select among them for aging, delegation and other deployment purposes.

# Lookup a Domain's DKIM Records

From the `DKIM-Signature:` header field in an email, lookup `%selector%._domainkey.domain.com`

For example this DKIM-Signature from gmail:

```
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed;
 d=gmail.com; s=20161025;
 h=mime-version:from:date:message-id:subject:to;
 bh=GwGu6WsZv/Pvcs+/zafIPWMt3PDJ/TA6wqESFLo7Qo8=;
 b=iyJqb7y81oQDo7voB1H1X8tQBmM1kJm7qsOTfVGWDBdzJ7T9UszfPRAQQwdsIoCOvu
 Zqg8pHCN3fBx0TYMHdS9PGUgmcpiuyPM61qC9Ph3sGhRa6O5IzaknvwuPjqFsC6fynkK
 pSarjb4WjXfaet7n3TKuryKqPsDor+PnU4e8rjpMEbYYG4SDRC4xfXmB+kEDIpby6SBt
 6gNMRaTzAhun/trrl5B8CJorStn5JET5I9dSzotwgImYKR6BvahYeBW8yHHrnJdBHfXQ
 5qDaX7gpem4Qe/+Pnedn6q4rxtYTqpM3NDRCxGIW6iaV3F7SraYUpw2TDY+NLATgTKv+
 bopg==
```

You could do the following DNS lookup:

``` powershell
Resolve-DnsName -Name 20161025._domainkey.gmail.com -Type txt | fl

Name    : 20161025._domainkey.gmail.com
Type    : TXT
TTL     : 285
Strings : {k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAviPGBk4ZB64UfSqWyAicdR7lodhytae+EYRQVtKDhM+1mXjEqRtP/pDT3sBhazkmA48n2k5NJUyMEoO8nc2r6sUA+/Dom5jRBZp6qDKJOwjJ5R/OpHamlRG+YRJQqR, tqEgSiJWG7h7efGYWmh4URhFM9k9+rmG/CwCgwx7Et+c8OMlngaLl04/bPmfpjdEyLWyNimk761CX6KymzYiRDNz1MOJOJ7OzFaS4PFbVLn0m5mf0HVNtBpPwWuCNvaFVflUYxEyblbB6h/oWOPGbzoSgtRA47SHV53SwZjIsVpbq4LxUW9IxAEwYzGcSgZ4n5Q8X8TndowsDUzoccPFGhdwIDAQAB}
```

# Additional Resources

https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail

http://dkim.org/

http://dkim.org/info/DKIM-teaser-03.pdf

http://dkim.org/Misc/DKIM-perform-en.pdf
