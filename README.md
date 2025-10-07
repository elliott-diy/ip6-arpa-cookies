# ARPA Cookie Demo

This is a small demo showing how `ip6.arpa` reverse DNS zones interact in unexpected ways with the [Public Suffix List](https://publicsuffix.org/).

Normally, browsers prevent cookies from being set at a top-level domain (e.g. `.com`) so they can’t be shared across unrelated sites.  

But because of how `ip6.arpa` is handled, you can scope cookies to `2.ip6.arpa`, the only publicly routed IPv6 reverse zone (oversimplified, but I wanted to keep this short).  

As a result, cookies can be read across *any* site hosted under that zone, even if they’re unrelated.

---

## How it works

- **[cookie.c…2.ip6.arpa](https://cookie.c.e.0.b.0.7.4.0.1.0.0.2.ip6.arpa/)** - sets a cookie with `Domain=2.ip6.arpa`
- **[monster.9…2.ip6.arpa](https://monster.9.4.8.e.0.7.4.0.1.0.0.2.ip6.arpa/)** - reads and displays the cookie

Since both fall under the same `2.ip6.arpa` parent, the browser treats them as part of the same “cookie scope,” allowing global sharing within that zone even though they should be treated as separate sites.

---

## Why this matters

- **TL;DR:** It doesn’t; nobody sane hosts production websites on `ip6.arpa`.
- It does, however, highlight a quirk in how cookie scoping and the Public Suffix List interact with unusual domains.
- The same concept applies to `in-addr.arpa` for IPv4, though it’s much harder to demonstrate.
- In theory, this could be misused for tracking or command-and-control if someone deliberately abused `.arpa` hosting. I won’t go into those fun details here, but please don’t do that.
--- 

## Acknowledgements

- Thanks to [lemonyte](https://9.4.8.e.0.7.4.0.1.0.0.2.ip6.arpa/) for hosting the sister site on his IPv6 block, which makes the cross-site demo possible.

---

## References

- Blog: [elliott.diy/blog/arpa](https://elliott.diy/blog/arpa) - if this 404s, I haven’t written it yet. Sorry, university is busy! :(
- Public Suffix List: [publicsuffix.org](https://publicsuffix.org/)
