# NanoClaw agent templates

Agent templates for [NanoClaw](https://github.com/nanocoai/nanoclaw), made by Eva ([@intentionaleva](https://github.com/intentionaleva)). Each folder is a complete template: open it to read what the agent does, what it needs, and how to set it up.

| Template | What it does |
|----------|--------------|
| [**Wren**](lifestyle/wren) | Household emergency-preparedness companion. Looks up the real hazards where you live, builds a red/amber/green plan sized to your family and budget, and checks in until it's done. |
| [**Nina**](lifestyle/nutrition-claim-check) | No-BS nutrition fact checker. Send a claim you saw and get a sourced verdict with an evidence grade and receipts. |
| [**Paula**](lifestyle/plant-based-coach) | Go-plant-based coach. Learns what you like, suggests three dishes at a time, finds the recipe and a shop nearby, and checks in on your day. |
| [**Rese**](hr/reference-check) | Consent-first reference checks by phone over Dial. One message in, a neutral structured summary out, no scoring. |

The folders follow the `<category>/<template>` layout of the official [NanoClaw template library](https://github.com/nanocoai/nanoclaw-templates), so each one can be copied there unchanged.

## Install a template

From a clone of this repo, copy the template into your NanoClaw install and create an agent from it. Wren as the example:

```bash
mkdir -p ~/nanoclaw/templates/lifestyle
cp -R lifestyle/wren ~/nanoclaw/templates/lifestyle/
cd ~/nanoclaw
ncl groups create --template lifestyle/wren --name "Wren"
```

Then connect it to a chat with `/manage-channels` and say hello. Some templates need an API key or a service connected first; the template's own README says which.

## Add a template

Put it in its own folder under a category (`lifestyle/`, `hr/`, …) with a `plugin.json` and a `README.md`, then add a row to the table above.

## License

MIT, see [LICENSE](LICENSE).
