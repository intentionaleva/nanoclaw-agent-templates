# Wren

A NanoClaw agent template: a household emergency-preparedness companion. The template itself is in `lifestyle/wren/` and its own README explains what it does, how it is laid out, and what it deliberately leaves out.

This repo keeps the two-level `<category>/<template>` layout the NanoClaw registry expects, so the folder can be copied into a registry fork unchanged when it's time to submit. `docs/wren-handoff.md` is that submission runbook.

## Install into a local NanoClaw

```bash
mkdir -p ~/nanoclaw/templates/lifestyle
cp -R lifestyle/wren ~/nanoclaw/templates/lifestyle/
cd ~/nanoclaw
ncl groups create --template lifestyle/wren --name "Wren"
```

Re-copy after every edit; NanoClaw stamps from the copy, not from this clone. Then wire it to a chat with `/manage-channels` and say hello.

## Check before committing

The registry's checks script has no dependencies and runs on any clone of `nanocoai/nanoclaw-templates`:

```bash
node /path/to/nanoclaw-templates/scripts/check-templates.mjs
```

It only walks the repo it sits in, so copy `lifestyle/wren` into that clone first, or run it from the registry fork when preparing the PR.
