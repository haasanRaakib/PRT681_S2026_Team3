# Week 11 — Active Directory + log4net

Two enterprise .NET staples this week: where identities come from (Active Directory) and where the old-school logs go (log4net).

## Active Directory

- the directory tree: forest → domain → OUs → users / groups / computers
- authentication: Kerberos tickets vs NTLM challenges, and why modern setups disable NTLM
- LDAP as the query protocol — browsing AD like a database with `LDAP://...` paths
- groups vs OUs: groups grant access, OUs are for organising and applying policy
- service accounts: why apps get their own identity instead of borrowing a person's
- how this lands in ASP.NET: Windows authentication in IIS, then role checks against AD groups — `[Authorize(Roles = "CORP\\Expense-App-Admins")]`

## log4net

- the .NET Framework classic: loggers with levels `DEBUG` → `INFO` → `WARN` → `ERROR` → `FATAL`
- appenders decide where output goes: console, file, rolling file with size/date caps
- everything configured in `App.config` / `web.config` — change log level or destination without recompiling
- pattern layouts: `%date %-5level %logger — %message%newline`

## Things I sat with

**AD is just a database of who may do what.** Once I stopped treating it as magic it clicked: my Week 4 auth code issues its own JWTs because there is no domain. On a corporate network, AD is the identity database and the app just asks it.

**External config was the whole point of log4net.** The alternative I'd been writing — `Console.WriteLine` scattered through code — needs a rebuild to silence. Flipping one config value to turn `DEBUG` off in production is the actual feature.
