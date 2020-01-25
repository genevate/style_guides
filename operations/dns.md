# Domain Name System (DNS) Styles

- Use a [Registry Lock](https://krebsonsecurity.com/2020/01/does-your-domain-have-a-registry-lock)
  which helps protect domain name records from being changed. *This may increase the time to make
  key changes to the locked domain (i.e. DNS changes).*
- Use DNSSEC for both signing zones and valiating responses.
- Use access control lists for traffic and monitoring of applications.
- Time to Live (TTL)
  - Default all settings to 5 days.
  - Use shorter settings (i.e. less than an hour) prior to making changes then set back to defaults
    after changes are applied.
- [Enable SPF](https://scotthelme.co.uk/email-security-spf)
