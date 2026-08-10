---
layout: default
title: DNS Walkthrough
---

# DNS Walkthrough

## What happens when someone types your address

Think of DNS as the internet's phone book. Nobody memorizes IP addresses
(long strings of numbers that actually locate a server) — instead, you
type a name like `tomazdrumond.github.io`, and DNS translates that name
into the address a computer needs.

**The four players in that translation, in order:**

1. **Resolver** — the first stop. When you type an address, your device
   asks a resolver (usually run by your internet provider, or a public
   one like Cloudflare's 1.1.1.1) to figure out where that name actually
   points.
2. **Root and TLD nameservers** — if the resolver doesn't already know
   the answer, it asks a root server "who handles `.io` addresses?",
   gets pointed to the right place, then asks that server "who handles
   `github.io`?"
3. **Authoritative nameserver** — the server that holds the actual,
   definitive record for the domain — GitHub's own nameservers, since
   they own `github.io`. It gives the final, correct answer.
4. **Response** — that answer travels back through the resolver to your
   device, which now knows exactly which server to connect to, and
   loads the page.

## What a CNAME record actually is

A CNAME (Canonical Name) record doesn't point to a number — it points to
another name, which then gets looked up the same way. It's an alias:
"this name is just another way of saying that name, go look that one up
instead."

## What this means for the future FlyRank subdomain

When `tomazdrumond.flyrank.ai` is provisioned, Ops will create a CNAME
record on their end. That record's value will be `tomazdrumond.github.io`
— pointing the new subdomain at the site that already exists. My half of
the job: add that custom domain inside GitHub Pages' settings, wait for
the change to propagate, and confirm HTTPS is working.
