# patchright-enhanced 

<a href="https://trendshift.io/repositories/242710?utm_source=trendshift-badge&amp;utm_medium=badge&amp;utm_campaign=badge-trendshift-242710" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/trendshift/repositories/242710/daily?language=TypeScript" alt="whaleyxbt%2Fpatchright-enhanced | Trendshift" width="250" height="55"/></a>

stealth browser automation framework for penetration testing, scraping, and WAF bypass. Built on [Patchright](https://github.com/Kaliiiiiiiiii-Vinyzu/patchright-nodejs).

clean chrome sessions that pass Cloudflare, Kasada, DataDome, and other WAFs out of the box.

that's basically just a wrapper around OG patchright, so it's easier to get started.

## Setup for Linux

```bash
# Install dependencies
npm install

# Install Chrome for Patchright
npx patchright install chrome

# Copy env template and configure
cp .env.example .env

# Add your proxies
# Format: host:port:username:password (one per line)
nano proxies.txt
```

## Configuration

All settings are in `.env`:

| Variable | Default | Description |
|---|---|---|
| `BROWSER_EXECUTABLE_PATH` | `/usr/bin/google-chrome-stable` | Path to Chrome binary |
| `BROWSER_TIMEZONE` | `Europe/Berlin` | Browser timezone |
| `MAX_PARALLEL` | `1` | Number of parallel sessions |
| `START_PAGE_URL` | `https://google.com/` | Initial page to open |

## Usage

```bash
npm run build
npm start
```

it opens a chrome session with the configured proxy and navigates to `START_PAGE_URL`. the session stays open until you close the browser window manually.

## Anti-Detection

my small framework relies entirely on patchright's built-in stealth patches:

- `Runtime.enable` leak patched (JS execution in isolated contexts)
- `--disable-blink-features=AutomationControlled` flag added
- `--enable-automation` flag removed
- `navigator.webdriver` returns `false` natively
- No fingerprint injection, no `addInitScript`, no `Object.defineProperty` overrides
