# Distribution

I published this repository to share the English edition I use locally, including its source changes and the exact installed package.

| Item | Value |
| --- | --- |
| Package | `dsh-ppt-flashmade` |
| Version | `0.7.1-english.20261029.1` |
| Upstream | <https://github.com/Bingtang1019/dsh-ppt-fusion> |
| Source baseline | `a19f4d3832e92b4c722e305c7b9b67cae9ad8153` |
| Release archive | `dsh-ppt-flashmade-0.7.1-english.20261029.1.tgz` |
| Published | 1 November 2026 |

The release archive is unchanged from the installed package, including its bundled `@liustack/pptwise` dependency. It contains the original package README; the repository README has been rewritten for public installation. `SHA256SUMS.txt` in the release verifies the archive bytes. `INSTALLED-PACKAGE.json` inventories its files and SHA-256 hashes, excluding bundled `node_modules` dependencies, which remain covered by the archive checksum.

The Python engine environment is installed separately on the user's machine. It is not included in the archive. Credentials, DSH profile configuration, conversation history, and locally authored decks are not part of this distribution.

Original authors retain their rights and supplied license notices. The upstream metadata declares MIT, but the captured upstream source and archive omit the root `LICENSE` file. See `NOTICE`, `python-assets/vendor/NOTICE`, and `docs/licensing.md` for the supplied attribution and dependency terms.
