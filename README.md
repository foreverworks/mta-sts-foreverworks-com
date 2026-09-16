# MTA-STS policy for foreverworks.com

Served at https://mta-sts.foreverworks.com/.well-known/mta-sts.txt (RFC 8461).

Mode is `testing` while TLS-RPT reports come in. To enforce: change `mode` to `enforce` here and bump the `id` in the `_mta-sts.foreverworks.com` TXT record in the same change.
