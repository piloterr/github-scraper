<p align="center">
  <a href="https://www.piloterr.com"><img src="images/banner.png" alt="GitHub Scraper API by Piloterr – scrape GitHub data as JSON" width="100%"></a>
</p>

# GitHub Scraper API

[![Discord](https://img.shields.io/badge/Discord-Join%20the%20community-5865F2?logo=discord&logoColor=white)](https://discord.gg/CFj3ph8aHU) [![Get API key](https://img.shields.io/badge/Piloterr-Get%20a%20free%20API%20key-111827)](https://app.piloterr.com) [![API docs](https://img.shields.io/badge/Docs-OpenAPI-0EA5E9)](https://app.piloterr.com/openapi) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

The **Piloterr GitHub Scraper API** lets you extract public data from GitHub as **clean, structured JSON** — no proxies, headless browsers or HTML parsing to maintain. Endpoints available in production:

- **GitHub User Info API** — Retrieve public GitHub user profile data including bio, company, location, follower count, repositories, and associated email addresses.

Use it for lead generation, CRM enrichment, market mapping, investment research or job market analytics.

| Endpoint | Path | Credits | What you get |
|---|---|---|---|
| [GitHub User Info API](#github-user-info-api) | `/v2/github/user/info` | 1 | Retrieve public GitHub user profile data including bio, company, location, follower count, repositories, and associated email addresses. |

## Table of contents

- [How it works](#how-it-works)
- [GitHub User Info API](#github-user-info-api)
- [Code examples in other languages](#code-examples-in-other-languages)
- [Practical use cases](#practical-use-cases)
- [Why Piloterr?](#why-piloterr)
- [FAQ](#faq)
- [Related scrapers](#related-scrapers)
- [Support](#support)

## How it works

1. **Create a free Piloterr account** and copy your API key from the [dashboard](https://app.piloterr.com).
2. **Send a `GET` (or `POST`) request** to `https://api.piloterr.com/v2/...` with the header `x-api-key: YOUR_API_KEY`.
3. **Receive structured JSON** — Piloterr handles rendering, proxies, retries and parsing.

```bash
export PILOTERR_API_KEY="your-api-key"
pip install requests        # Python
# TypeScript: Node.js 18+ (native fetch), run with `npx tsx file.ts`
```

> Every endpoint accepts both `GET` (query string) and `POST` (JSON body with the same fields).

## GitHub User Info API

Retrieve public GitHub user profile data including bio, company, location, follower count, repositories, and associated email addresses.

`GET | POST https://api.piloterr.com/v2/github/user/info` · **1 credit per request** · [Full reference](https://app.piloterr.com/openapi)

### Request parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `query` | string | ✅ | A GitHub user identifier. Multiple formats are accepted: |

### Python example

```python
import json
import os
import requests

response = requests.get(
    "https://api.piloterr.com/v2/github/user/info",
    headers={"x-api-key": os.environ["PILOTERR_API_KEY"]},
    params={
        "query": "https://github.com/example-user",
    },
    timeout=120,
)
response.raise_for_status()
data = response.json()

print(json.dumps(data, indent=2, ensure_ascii=False)[:2000])
```

### TypeScript example

```typescript
type GithubUserInfo = {
  id?: number;
  name?: string;
  email?: string[];
  login?: string;
  company?: string;
  gist_url?: string;
  gpg_keys?: string;
  location?: string;
  ssh_keys?: string;
  followers?: number;
  following?: number;
  avatar_url?: string;
  created_at?: string;
  updated_at?: string;
  public_gists?: number;
  public_repos?: number;
};

const params = new URLSearchParams({
  "query": "https://github.com/example-user",
});

const response = await fetch(`https://api.piloterr.com/v2/github/user/info?${params}`, {
  headers: { "x-api-key": process.env.PILOTERR_API_KEY! },
});
if (!response.ok) throw new Error(`Piloterr error ${response.status}: ${await response.text()}`);

const data = (await response.json()) as GithubUserInfo;

console.log(JSON.stringify(data, null, 2).slice(0, 2000));
```

<details>
<summary><b>POST variant</b></summary>

```http
POST https://api.piloterr.com/v2/github/user/info
x-api-key: YOUR_API_KEY
Content-Type: application/json

{"query": "https://github.com/example-user"}
```
</details>

### Output example

Response shape with placeholder values — field names follow the API reference.

```json
{
  "id": 0,
  "name": "example",
  "email": [
    "example"
  ],
  "login": "example",
  "company": "example",
  "gist_url": "example",
  "gpg_keys": "example",
  "location": "example",
  "ssh_keys": "example",
  "followers": 0,
  "following": 0,
  "avatar_url": "example",
  "created_at": "example",
  "updated_at": "example",
  "public_gists": 0,
  "public_repos": 0
}
```

### Response fields

| Field | Type | Description |
|---|---|---|
| `id` | integer |  |
| `name` | string |  |
| `email` | string[] |  |
| `login` | string |  |
| `company` | string |  |
| `gist_url` | string |  |
| `gpg_keys` | string |  |
| `location` | string |  |
| `ssh_keys` | string |  |
| `followers` | integer |  |
| `following` | integer |  |
| `avatar_url` | string |  |
| `created_at` | string |  |
| `updated_at` | string |  |
| `public_gists` | integer |  |
| `public_repos` | integer |  |

## Code examples in other languages

Ready-to-run examples live in the [`examples/`](examples) folder. Each one reads your key from the `PILOTERR_API_KEY` environment variable.

| Language | User Info |
|---|---|
| cURL (Bash) | [`user-info`](examples/curl/user_info.sh) |
| PHP | [`user-info`](examples/php/user_info.php) |
| C# | [`user-info`](examples/csharp/UserInfo.cs) |
| Go | [`user-info`](examples/go/user_info.go) |
| Java | [`user-info`](examples/java/UserInfoExample.java) |
| Ruby | [`user-info`](examples/ruby/user_info.rb) |
| Node.js | [`user-info`](examples/nodejs/user_info.mjs) |

## Practical use cases

- **Lead generation** — Build target account lists from public company data.
- **CRM enrichment** — Keep firmographics, websites and descriptions up to date.
- **Market mapping** — Map competitors and segments across countries and industries.
- **Investment research** — Screen companies, funding and signals for deal flow.
- **Job market analytics** — Track hiring, roles and salaries where available.

## Why Piloterr?

- **No infrastructure** — no proxies, headless browsers or CAPTCHA solving to run yourself.
- **Structured JSON** — stable, documented fields instead of brittle HTML selectors.
- **Pay per request** — transparent credit cost per endpoint, failed requests are retried for you.
- **One API key, hundreds of sources** — GitHub plus many other e-commerce, search and company data endpoints in the [Piloterr library](https://www.piloterr.com/library).
- **Any language** — plain HTTPS + JSON, with examples for Python, TypeScript, cURL, PHP, C#, Go, Java, Ruby and Node.js.

## FAQ

### Is it legal to scrape GitHub?

Collecting publicly available data is generally allowed in many jurisdictions, but rules depend on your country, the data you collect and how you use it. Avoid personal data unless you have a lawful basis, respect the website's terms where they apply, and get legal advice for your specific use case. This is not legal advice.

### Do I need proxies or a headless browser?

No. Piloterr handles rendering, proxy rotation and retries on its side. You only send an HTTPS request with your `x-api-key` header and receive JSON.

### How much does a request cost?

Credits per call: `/v2/github/user/info` **1**. See the [Piloterr website](https://www.piloterr.com) for plans.

### What data does the GitHub API return?

Each endpoint returns structured JSON: **GitHub User Info** — `id`, `name`, `email`, `login`, `company`, `gist_url`.

### Which languages are supported?

Any language that can make an HTTP request. This README shows Python and TypeScript; the [`examples/`](examples) folder contains cURL, PHP, C#, Go, Java, Ruby and Node.js.

## Related scrapers

- [Company Database Scraper API](https://github.com/piloterr/company-data-api)
- [Crunchbase Scraper API](https://github.com/piloterr/crunchbase-scraper)
- [Europages Scraper API](https://github.com/piloterr/europages-scraper)
- [Fiverr Scraper API](https://github.com/piloterr/fiverr-scraper)
- [G2 Scraper API](https://github.com/piloterr/g2-scraper)
- [Glassdoor Scraper API](https://github.com/piloterr/glassdoor-scraper)
- [All Piloterr scrapers on GitHub](https://github.com/piloterr)

## Support

- 💬 Join the [Piloterr Discord](https://discord.gg/CFj3ph8aHU) to ask questions and share what you build.
- 📚 Browse the [API reference (OpenAPI)](https://app.piloterr.com/openapi) and the [Piloterr library](https://www.piloterr.com/library).
- 🔑 [Get your API key](https://app.piloterr.com).

---

<p align="center">
  <a href="https://www.piloterr.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="images/logo-dark.svg">
      <img src="images/logo.svg" alt="Piloterr" height="32">
    </picture>
  </a>
  <br>
  <sub>Built by <a href="https://www.piloterr.com">Piloterr</a> — web scraping APIs for e-commerce, search, real estate and more, one API key.</sub>
</p>

<sub>GitHub is a trademark of its respective owner. This repository is not affiliated with or endorsed by GitHub. Examples are released under the MIT license.</sub>
