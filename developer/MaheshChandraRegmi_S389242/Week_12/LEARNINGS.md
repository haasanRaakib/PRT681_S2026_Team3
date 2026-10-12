# Week 12 — Serilog + ELMAH, and a logging round-up

Last stretch of the term, so I finished the logging story from Week 11: Serilog (the modern structured logger) and ELMAH (the ASP.NET error catcher), then compared all three against each other.

## Serilog

- structured logging: `Log.Information("Expense {ExpenseId} created for {Amount}", id, amount)` — the values are stored as properties, not glued into a string
- message templates instead of interpolation, so `"$" + amount` never makes it into a log line
- sinks: console, rolling file, Seq — start with console, add the rest in config
- wires into `Microsoft.Extensions.Logging`, so ASP.NET Core's `ILogger<T>` calls end up in Serilog
- enrichers add context automatically (machine name, request id)

## ELMAH

- plugs into the ASP.NET pipeline and logs **unhandled** exceptions on its own — no try/catch required
- `elmah.axd` gives a web dashboard of every error: stack trace, request, timestamp
- storage backends: memory, XML files, or a database table
- deliberately narrow: errors only, not general app logging

## Comparing the three

- **log4net** — text lines, config-driven, .NET Framework era, still everywhere in legacy apps
- **Serilog** — structured events, first-class in modern .NET, queryable by property (`Amount > 100`)
- **ELMAH** — exception monitoring with a UI; complements a logger rather than replacing one

## Things I sat with

**Structured beats text the first time you filter logs.** Searching a text file for "how many expenses over $100 got logged this week" is hopeless; with Serilog it's a query on a property.

**What I'd actually wire up.** Modern ASP.NET Core app: Serilog with console + file sinks. Legacy Framework app holding an old intranet together: log4net for app logs and ELMAH on top, so unhandled errors land somewhere with a stack trace attached.
