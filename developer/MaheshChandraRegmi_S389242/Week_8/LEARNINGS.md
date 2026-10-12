# Week 8 — Database fundamentals + ER diagram practice

Weeks 6 and 7 I was writing SQL and EF code straight into the Tasks schema. This week I slowed down and did the database work the other way around: design first on paper, SQL second.

## Database topics I covered

- `INNER JOIN` vs `LEFT JOIN` — LEFT is the one I actually want for "all expenses, plus the category name if they have one"
- indexes: what a lookup costs with and without one, why they slow down `INSERT`/`UPDATE`
- normalization 1NF → 2NF → 3NF, and when I'd denormalize on purpose (reporting tables)
- transactions and ACID — `BEGIN` / `COMMIT` / `ROLLBACK`, and what actually comes back on rollback
- SQLite vs Postgres vs SQL Server — file vs server, where each fits (SQLite for the Week 6/7 demos was the right call)
- parameterized queries vs string concatenation — revisited the `$title` style from Week 6 and why it kills SQL injection

## ER diagram practice

Redrew the ExpenseTracker schema as an ER diagram before touching any code:

- `User 1 —— * Expense`
- `Category 1 —— * Expense`
- `User * —— * Category` through a `UserCategory` junction table (per-user category budgets)

Then converted the diagram to `CREATE TABLE` statements by hand — PKs, FKs, and `NOT NULL` fell out of the diagram instead of being guesses.

## Things I sat with

**Cardinality on paper is cheaper than migrations later.** Drawing the M:N between users and categories exposed the junction table I would otherwise have bolted on halfway through coding it.

**Crow's foot notation is just vocabulary.** A bar means exactly one, the crow's foot means many, a circle means zero. Once I stopped mixing up the symbols, the diagrams read like sentences.
