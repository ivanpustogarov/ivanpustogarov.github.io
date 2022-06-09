---
layout: page
title: Bitcoin and Tor deanonymization
description: Deanonymizing criminals who use anonymization technologies
img: assets/img/network.jpg
importance: 3
category: work
---

<a href="https://github.com/ivanpustogarov/hsportscanner" title="GitHub"><i class="fab fa-github" style="font-size:18px">&nbsp; https://github.com/ivanpustogarov/hsportscanner</i></a>

<a href="https://github.com/ivanpustogarov/bcclient" title="GitHub"><i class="fab fa-github" style="font-size:18px">&nbsp; https://github.com/ivanpustogarov/bcclient</i></a>


In this set of projects, we analyzed anonymity level provided by the Tor network and
Bitcoin. 

Anonymization technologies are a double-edged sword. On the one hand, they help
fight censorship in countries with oppressive regimes, prevent tracking by
large tech corporation, and allow one to send money across borders without
restriction mandated by the global banking system. On the other hand the very
same technologies can be used by malicious actors to commit various
cybercrimes, such extortion, blackmailing, money laundering, and selling drugs
and other prohibited/dangerous items online.

Our goal in this set of projects was to analyze ways Tor and Bitcoin are used
by criminals, evaluate anonymity provided by these two systems and to find ways
to deanonymize cybercriminals who use these technologies to hide their
traces.

### Tor

Tor is a volunteer-operated network of relay servers, each running an
open-source software developed by the Tor project. It can be used by anyone to
conceal their location and prevent network surveillance or traffic analysis.
This achieved by the user sending traffic through multiple Tor relays before it
reaches the target server/web-site.  In this way, the destination web-site sees
the IP address of the last relay in the path instead of the user's IP address.
Similarly, the user's ISP can only see that the user connects to the first
relay in the path, and thus cannot learn what web-site the users is
connecting to.

### Onion Services

In a similar way, Tor can also provide anonymity to websites.  In order to hide
its location/IP address from  the both the clients and the ISP, the server
would choose a random Tor relay that would be used to forward clients'
traffic to the server and back.

This type of functionality turns to be very useful to operate a marketplace to
sell drugs and other illegal items.

### Bitcoin network anonymity

While Bitcoin’s transaction are publicly available and can often be linked to
the same entity, the real identities are still hidden behind pseudonymous
Bitcoin addresses.  Moreover the relation between different transactions can be
broken using Bitcoin mixers.  Given bitcoin high market price, this makes it a
useful tool for illegal activities such as money laundering, infecting
companies with ransomware, extortionware, and selling illegal items.

### Deanonymization

In this set of projects we found a number of limitations and design flaws in
both Tor Bitcoin networks that allowed us to deanonymize its users.  We showed
possibility for complete deanonymization of a large number of Tor hidden
services and were the first to describe a practical off-path network-level
deanonymization attack on Bitcoin clients. Finally, in this project, we showed
that users that connect to the Bitcoin network through Tor are vulnerable to
Man-in- the-Middle attacks.
