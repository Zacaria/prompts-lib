# AGENTS.md
Only for projects with no real users yet.

## Ground rules
- No backward compatibility, no data migrations
- Replace what you change with the simplest code that works, and update every caller in the same change

## Every change, in this order
1. Docs first: update the relevant docs and make sure they don't contradict the code or each other
2. Tests: test behavior, skip the small details, and watch them fail first
3. Smallest implementation: write only enough to pass the tests, nothing extra
4. Clean up: delete the code, files and docs this change made unused. Not sure? Ask me

## Don't
- Keep old code "just in case"
- Delete a database or reset data without asking me

## Before you say done
- Run the tests and read the output yourself
- Tell me what you deleted
- Didn't run a check? Say so

## When I correct you
- Add a line at the top of Lessons: "When X, do Y"
- Same mistake twice means that lesson is unclear. Rewrite it, don't add another
- Over 20 lessons? Merge duplicates, delete outdated ones, then show me

## Lessons

