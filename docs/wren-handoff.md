# Wren: handoff for Claude Code

Goal: open a pull request adding `lifestyle/wren/` to `nanocoai/nanoclaw-templates`. The source is this repo (`intentionaleva/wren`, folder `lifestyle/wren/`). GitHub handle: `intentionaleva`. Do this only once Wren has been stamped and tested on a real install.

## 1. Fork and clone

Fork `nanocoai/nanoclaw-templates` to `intentionaleva/nanoclaw-templates` on github.com (one click, Fork button), then:

```bash
gh repo clone intentionaleva/nanoclaw-templates
cd nanoclaw-templates
git remote add upstream https://github.com/nanocoai/nanoclaw-templates.git
git fetch upstream && git checkout -b add-lifestyle-wren upstream/main
```

## 2. Drop the template in

```bash
cp -R ~/path/to/wren/lifestyle/wren lifestyle/wren   # from your clone of intentionaleva/wren
```

Confirm the layout is exactly two levels: `lifestyle/wren/plugin.json` exists, and `author.url` in it is your handle.

## 3. Run the registry checks

```bash
node scripts/check-templates.mjs
node scripts/build-index.mjs
git diff --exit-code index.json || echo "index.json changed: commit it"
```

Expected: `check-templates: N template(s) OK: … lifestyle/wren …`. `index.json` is generated from every `plugin.json` and CI fails if it drifts, so the regenerated file goes in the same commit. The checks walk every template; unrelated failures in other folders are not yours.

## 4. Stamp and test against a real install

From your NanoClaw install (the `nanoclaw` folder, host running):

```bash
mkdir -p ~/nanoclaw/templates/lifestyle
cp -R lifestyle/wren ~/nanoclaw/templates/lifestyle/
cd ~/nanoclaw
ncl groups create --template lifestyle/wren --name "Wren test"
```

Check the create response for a `templateReport` array. It should be empty. Then:

```bash
ncl groups list                                     # copy the Wren test id
ncl tasks list --group <group-id> --status paused   # three tasks, all paused
ncl wirings create --channel-type cli --platform-id local --agent-group-id <group-id>
pnpm run chat "Hi"
```

Wren should introduce itself in three lines and start block 1 of onboarding. Answer the five blocks with your real household; the risk pass should name the NRW flood map and a date, and (if the `osm` server booted) propose meeting places with foot times. If the `osm` tools are missing, check that the sandbox allowlist permits `nominatim.openstreetmap.org`, `overpass-api.de` and `router.project-osrm.org`; the template still works without them.

When done: `ncl groups delete --id <group-id>`.

## 5. Re-read the diff for secrets, commit, push

```bash
cd nanoclaw-templates
git add lifestyle/wren index.json
git diff --cached | grep -iE 'sk-|ghp_|token|secret|api_key' || echo "no secrets"
git commit -m "Add wren template (lifestyle/)"
git push -u origin add-lifestyle-wren
```

## 6. Open the PR

```bash
gh pr create --repo nanocoai/nanoclaw-templates --base main --head intentionaleva:add-lifestyle-wren \
  --title "Add wren template (lifestyle/wren): household emergency-preparedness companion" \
  --body-file PR.md
```

`PR.md` content:

```markdown
## What it does

Wren is a household emergency-preparedness companion for private people and families. It runs a ten-question onboarding (people and age bands, pets, home and regular locations, trips, medical and access needs, goal, budget, check-in day), looks up the real hazards for each location with the source and check date shown, and builds one plan tiered red (this week, free, under an hour each), amber (4 to 8 weeks, stock and kits, spread to the budget) and green (3 to 12 months, power, heating, comms, training). It drafts the family emergency communication card (ready.gov structure), then checks in weekly, reviews the kit monthly for expiries, and re-runs the risks quarterly.

Guidance is drawn from ready.gov (FEMA) and the German BBK brochure "Vorsorgen für Krisen und Katastrophen" (11/2025); for other countries it searches for the national civil-protection body. Scope is deliberately narrow: no weapons, no survivalism, no medical advice beyond official first aid, no business continuity.

## Category

`lifestyle/`, next to `family-assistant`. Nothing in the catalog or open PRs covers preparedness.

## Tasks (all created paused)

- `weekly-check-in` (Sun 18:00): at most three due items, one question, no repeated nags
- `monthly-kit-review` (1st, 10:00): expiries, rotation, battery and alarm tests
- `quarterly-plan-review` (1 Jan/Apr/Jul/Oct, 10:00): risks re-run, season check, household changes, one drill

Wren updates the weekly schedule to the household's chosen day at the end of onboarding and resumes it; the other two only on a yes.

## MCP servers and credentials

One optional server, `osm`: `osm-mcp@0.3.1` (OpenStreetMap geocoding, nearby POIs, routes, isochrones). No key, no placeholder, public endpoints. Without it the template runs end to end and skips place lookups. Hazard maps and official pages use the runtime's web search. No paid services.

## Testing

`node scripts/check-templates.mjs` passes. Stamped with `ncl groups create --template lifestyle/wren` and driven through onboarding, risk pass, plan and a check-in on a real install.

## Author

Eva (`intentionaleva`), set in `plugin.json`.
```

## 7. After opening

Reply to review comments in the PR. If maintainers ask for a different category or a smaller persona, both are quick: the persona is 70 lines, well under the 200 cap.
