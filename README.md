# Wren

A NanoClaw agent template: a household emergency-preparedness companion. The template itself is in `lifestyle/wren/` and its own README explains what it does, how it is laid out, and what it deliberately leaves out.

This repo keeps the two-level `<category>/<template>` layout the NanoClaw registry expects, so the folder can be copied into a registry fork unchanged.

## Install into a local NanoClaw

```bash
mkdir -p ~/nanoclaw/templates/lifestyle
cp -R lifestyle/wren ~/nanoclaw/templates/lifestyle/
cd ~/nanoclaw
ncl groups create --template lifestyle/wren --name "Wren"
```

Re-copy after every edit; NanoClaw stamps from the copy, not from this clone. Then wire it to a chat with `/manage-channels` and say hello.
