# Opsec Check

A private scam checker for independent builders and community organisers. Paste in a message, job offer, DM or link that feels off, and a small open-source AI model running **on your own device** tells you how risky it looks, quotes the warning signs, and suggests what to do next. Nothing you paste is sent anywhere.

Built with and for the [H.E.R. DAO](https://her-dao.xyz) community: 2,000+ independent builders in 20+ hubs across Africa, Asia, Europe and the Americas.

- **Live site:** https://opsec-check.netlify.app
- **Try it in your browser (experimental):** https://opsec-check.netlify.app/check
- **Give feedback:** https://tally.so/r/zEM6OE

> **Status: early pilot (November 2026).** Opsec Check can be wrong. It never says a message is definitely safe. If in doubt, check through a channel you already trust.

## Why it exists

Our members are targeted by scams built for them: fake job interviews that ask you to install software, impersonators posing as funders, organisers and old contacts, and links asking you to "verify" an account or wallet. One member was asked by an old contact to book a call. On the call, strangers said they couldn't hear and sent a link to "download a new version of Zoom". The link was malicious, and the contact's account had been hacked.

Cloud AI tools could help, but they'd mean sending the very messages people are worried about to someone else's servers. So Opsec Check is small and local.

## How it works

| | Desktop version | Browser version (experimental) |
|---|---|---|
| Model | Qwen3.5-2B (Q8_0), 2 billion parameters | Qwen3.5-2B (4-bit, about 1 GB) |
| Runs with | [llamafile](https://github.com/mozilla-ai/llamafile) by Mozilla.ai | [WebLLM](https://github.com/mlc-ai/web-llm) |
| Install | One 2.9 GB file | None (downloads into the browser once) |
| Works offline | Yes | Yes, once loaded |
| Reliability | Reliable on recent Mac, Windows and Linux laptops | Doesn't yet work reliably on every laptop, especially older ones with built-in graphics |

The behaviour comes from the instructions in [`system-message.txt`](system-message.txt): the threat patterns our members face, and a plain-language reply format (risk level, red flags, what to do).

## Run the desktop version

1. **Download** [Qwen3.5-2B-Q8_0.llamafile](https://huggingface.co/mozilla-ai/llamafile_0.10/resolve/main/Qwen3.5-2B-Q8_0.llamafile) from Mozilla.ai's official Hugging Face page.
2. **Check it's the genuine file.** The SHA256 checksum must be exactly:
   ```
   e4ac37318fffd222d802373a5e0c2ec7f78aa3af3744f01eec75a3750e130386
   ```
   - Mac: `shasum -a 256 ~/Downloads/Qwen3.5-2B-Q8_0.llamafile`
   - Windows (after renaming in step 3): `certutil -hashfile Qwen3.5-2B-Q8_0.llamafile.exe SHA256`

   Hugging Face labels this file "Suspicious" because 1 of 57 antivirus engines flags it. Microsoft Defender, Kaspersky, Sophos and others find nothing ([VirusTotal report](https://www.virustotal.com/gui/file/e4ac37318fffd222d802373a5e0c2ec7f78aa3af3744f01eec75a3750e130386/detection)).
3. **Run it.**
   - Mac: `cd ~/Downloads && chmod +x Qwen3.5-2B-Q8_0.llamafile && ./Qwen3.5-2B-Q8_0.llamafile`
   - Windows: rename the file to end in `.exe`, then double-click it.
4. Open http://localhost:8080, paste the contents of [`system-message.txt`](system-message.txt) into **Settings → System Message**, and start a new chat.

## Privacy

- Messages are checked on your own device and never sent anywhere. No account, no tracking, no analytics.
- The browser version keeps an on-device count of messages you've checked. It's never sent anywhere; you can choose to share it in the feedback form.
- Read-aloud uses only voices that run on your device.
- Model files are pinned to an exact version and checksum, so behaviour can't change silently.

## Accessibility

Atkinson Hyperlegible typeface, visible keyboard focus, labelled form fields, screen-reader announcements and focus moving to results, reduced-motion support, on-device read-aloud, and replies in the language of the message. Not yet tested widely with disabled users; that's in progress.

## Roadmap

- A community threat library of anonymised, opt-in examples from members
- A public test set, re-run at every release, including what the model misses
- Fine-tuning a small model on the threat library
- A published threat model and an independent security review
- Community review of every threat-pattern update before release
- One-click installers and more reliable browser support

## Repository contents

- `site/index.html`: the project site
- `site/check.html`: the in-browser checker
- `system-message.txt`: the Opsec Check instructions and threat patterns
- `LICENSE`: Apache 2.0

## Credits and licences

Opsec Check is released under the [Apache 2.0 licence](LICENSE). It builds on Qwen3.5-2B (Apache 2.0), Mozilla.ai's llamafile (Apache 2.0) and WebLLM (Apache 2.0).

Contact: contact@her-dao.xyz · [@_HerDAO](https://x.com/_HerDAO)
