# MTA-STS policy for foreverworks.com

This repository holds the MTA-STS policy of foreverworks.com, a small text file that tells other mail servers to deliver mail to this domain only over verified TLS ([RFC 8461](https://www.rfc-editor.org/rfc/rfc8461)).

The policy must be served over HTTPS at `https://mta-sts.foreverworks.com/.well-known/mta-sts.txt`. GitHub Pages does that for free: this repository is the website, `.well-known/mta-sts.txt` is the policy, `CNAME` names the host, and `.nojekyll` makes Pages serve the dot-folder as it is. A push to `main` publishes the file.

What each line of the policy means:

- `version: STSv1` is the only version of the format.
- `mode: enforce` makes a sending server refuse to deliver when it cannot reach one of the listed hosts over a valid TLS connection. `testing` only reports failures and `none` turns the policy off.
- `mx:` lines list the mail hosts that may receive mail for the domain. They must match the domain's MX records, and `*.` at the start matches any one subdomain label.
- `max_age: 86400` is how many seconds (one day) a sender may keep its copy of the policy.

To check it from your own machine:

```sh
curl -s https://mta-sts.foreverworks.com/.well-known/mta-sts.txt
dig +short TXT _mta-sts.foreverworks.com
```

The first command prints the file. The second prints the DNS record that announces the policy, in the form `"v=STSv1; id=<value>"`. Senders re-fetch the policy only when that `id` changes.

Change these together: when you edit the policy (a new `mx` host, a different `mode` or `max_age`), change the `id` in the `_mta-sts.foreverworks.com` TXT record in the same step, and keep the `mx:` lines in step with the domain's MX records. If the `id` stays the same, senders keep using their cached copy until `max_age` runs out.
