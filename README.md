# PPT Flashmade — English edition

This is the English edition of **PPT Flashmade** that I use in DeepSeek Harness. It brings together 24 pptwise themes, editable PowerPoint export through ppt-master, slide previews, and a workflow for reviewing the rendered deck before delivery.

I adapted [Bingtang1019's PPT Fusion](https://github.com/Bingtang1019/dsh-ppt-fusion). The original project and its dependencies keep their authorship and licenses; my changes are listed below.

[Download this edition](https://github.com/DSH-Extensions-list/dsh-ppt-flashmade/releases/tag/v0.7.1-english.20261029.1) · [CLI reference](docs/cli.md) · [Upstream project](https://github.com/Bingtang1019/dsh-ppt-fusion)

## What it does

- Creates presentations for product demos, business reviews, teaching, research, pitches, and reports.
- Exports editable DrawingML slides, including native charts and tables.
- Reuses templates and brand styles, with 24 themes available as starting points.
- Provides slide previews and rendered review through the DSH workflow.
- Includes optional animation and narration paths from upstream.

The registered skill is **`dsh-ppt-fusion`**. The preview, proposal, and review tools are `dsh_ppt_preview`, `dsh_ppt_propose`, and `dsh_ppt_review` when the DSH host provides their required services.

## Install this edition

Download `dsh-ppt-flashmade-0.7.1-english.20261029.1.tgz` and `SHA256SUMS.txt` from the [release page](https://github.com/DSH-Extensions-list/dsh-ppt-flashmade/releases/tag/v0.7.1-english.20261029.1). In the download directory, verify the archive:

```sh
sha256sum -c SHA256SUMS.txt
```

Install it into the DSH profile you use:

```sh
dsh plugin --profile desktop add -w /absolute/path/to/dsh-ppt-flashmade-0.7.1-english.20261029.1.tgz
```

Replace `desktop` with `web` or your own profile name if needed. Use the CLI belonging to that DSH installation, then restart the host after installation.

**Requirements:** Node.js 22.19 or newer and a compatible DSH host. The exact peer ranges are in [package.json](package.json). The first engine setup needs `uv`, network access, and the pinned Python dependencies in `python-assets/requirements.lock`.

On first use, ask the agent to run the plugin's `dsh-ppt doctor --repair` command. The loaded skill maps `dsh-ppt` to the installed CLI. This prepares the Python engine under `$DSH_HOME/ppt-fusion/venvs/`; it is separate from the plugin archive. See the [upstream installation notes](docs/install.md) for engine diagnostics and other install modes; their npm examples install upstream, rather than this English edition.

Installing `dsh-ppt-flashmade` from npm gives you upstream. Use the release archive above to get this edition.

## Use it

Ask DSH to use the `dsh-ppt-fusion` skill and give it the audience, purpose, and any constraints. For example:

> Use dsh-ppt-fusion to make a 10-slide presentation explaining this project to a technical audience. Use the documents in this workspace as sources. Keep the slides in English, use editable charts where there is real data, and review the rendered slides before exporting the PPTX.

For an existing presentation, attach or point to the reference deck and say what should change. Deck sources and exports stay in the task workspace.

The separate `pptx` skill is an optional alternative for PptxGenJS or template-editing work. It is **not bundled here**. Use one authoring engine for each deck.

## What I changed

This release is **`0.7.1-english.20261029.1`**, based on upstream `0.7.1`.

- Enabled the English skill and translated the main design reference and registration instructions.
- Made conversation, slide copy, notes, and reports default to English unless another language is requested.
- Kept already authorized local deck creation moving without extra planning approvals, while preserving approval for revisions to an existing published deck.
- Limited reference loading and image-review batches.
- Changed generated-image attribution to English.
- Updated `sharp` to `0.35.5` and overrode `image-size` to `2.0.4`.

Some upstream technical references and developer comments are still multilingual. An upstream update can replace these adaptations, so check the diff before upgrading.

## Source and release package

This repository contains the upstream source plus my local changes. The release archive is the exact package captured from my installed edition. [DISTRIBUTION.md](DISTRIBUTION.md) records its provenance and checksum; it has not been rebuilt for this publication.

For development, use Node.js 24:

```sh
npm ci --ignore-scripts --legacy-peer-deps
npm run typecheck
npm run lint
npm test
npm run build
```

The DSH host supplies the peer packages; `--legacy-peer-deps` keeps this standalone source install from trying to install a second host. The committed npm lockfile records the dependencies for this edition. The pnpm lockfile is retained from upstream and does not describe the updated dependency versions.

Type checks, lint, unit tests, and a CLI build are software checks. Opening, editing, saving, and reopening exports in PowerPoint/WPS, plus animation and narration playback, still need native-app verification. Linux export or rendering alone does not establish those results.

## Credits and licensing

- [Bingtang1019 / dsh-ppt-fusion](https://github.com/Bingtang1019/dsh-ppt-fusion) — the original DSH plugin, declared MIT.
- [pptwise](https://www.npmjs.com/package/@liustack/pptwise) — themes and the DSH presentation frontend, MIT.
- [ppt-master](https://github.com/elvisw/ppt-master) — the DrawingML engine, MIT.

See [NOTICE](NOTICE), [the vendored notices](python-assets/vendor/NOTICE), and [the dependency licensing notes](docs/licensing.md). The captured upstream source and package omit the root `LICENSE` file referenced in some upstream docs; I have retained the supplied notices and recorded that omission here.
