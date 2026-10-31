# MTA-STS policy for foreverworks.com

Served at https://mta-sts.foreverworks.com/.well-known/mta-sts.txt (RFC 8461).

Mode is `enforce`: senders that support MTA-STS deliver only over TLS to the MX hosts listed here. Any change to this file (a new MX host, a mode or max_age change) must bump the `id` in the `_mta-sts.foreverworks.com` TXT record in the same change, or senders keep their cached copy until it expires.
