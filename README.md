# Pocket Bookkeeper

Paste bank or UPI statement lines and get them sorted into freelancer-style categories (software, internet, travel, food, office, ads, bank and taxes, personal, income), with totals and a CSV download. A small open-source AI model does the sorting **on your own device**, so your statement never leaves your phone or laptop.

Built for the **Hacktoberfest Open-Source AI Challenge: Week 2 (Side Hustle)** on DEV.

**Live demo:** https://YOUR-USERNAME.github.io/pocket-bookkeeper/

## Who it's for

Freelancers and tiny shops who dump a month of statement lines into a spreadsheet and spend an evening labelling them before tax time or before sending numbers to an accountant. It could be sold as a small paid tool or as a per-month cleanup service.

## The open-source AI at its core

- **Model:** [all-MiniLM-L6-v2](https://huggingface.co/Xenova/all-MiniLM-L6-v2) (ONNX build by Xenova), Apache-2.0, about 23 MB quantized.
- **Runtime:** [Transformers.js](https://github.com/huggingface/transformers.js) (Apache-2.0), running on WebAssembly in the browser.
- **How it works:** every transaction description and a few example phrases per category are turned into vectors. Each transaction goes to the category whose examples are closest. If nothing is close enough, it is marked "Unsure" so you can fix it with a dropdown.
- **Local inference:** no API key, no backend, no per-request cost. Financial data stays on the device.

## Why open innovation matters here

Bank statements are about the most private data a freelancer has. With an open model that runs in the browser, the privacy claim is simple and checkable: there is no server to send the data to. It also costs nothing per statement, so the pricing isn't tied to anyone's API bill, and the categories and example phrases are plain text in `index.html` that anyone can edit for their own country or trade.

## Run it locally

```bash
git clone https://github.com/YOUR-USERNAME/pocket-bookkeeper.git
cd pocket-bookkeeper
python -m http.server 8000
```

Open http://localhost:8000. The first run downloads the model (about 23 MB), then your browser caches it.

## Customize

Edit the `CATS` object in `index.html`: add example phrases that look like your own statements (shops, apps and clients you actually pay), and the sorting improves immediately. No training needed.

## Files

- `index.html`: the whole app (UI and model code)
- `README.md`: this file
- `LICENSE`: MIT

## Limits

This is a sorting aid, not tax or accounting advice. Low-confidence rows are flagged for review. Amounts are read as the last number on each line, so very unusual statement formats may need a quick manual fix.

## License

MIT for this project's code. The model and Transformers.js keep their own Apache-2.0 licenses.
