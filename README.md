# Scrapester
<p align="center">
  <img src="assets/image.png" alt="Scrapester Logo" width="200"/>
</p>

[![PyPI version](https://badge.fury.io/py/scrapester.svg)](https://badge.fury.io/py/scrapester)
[![npm version](https://badge.fury.io/js/scrapester.svg)](https://badge.fury.io/js/scrapester)

[![npm downloads](https://img.shields.io/npm/dm/scrapester)](https://www.npmjs.com/package/scrapester)
[![PyPI downloads](https://img.shields.io/pypi/dm/scrapester)](https://pypi.org/project/scrapester/)


[![GitHub stars](https://img.shields.io/github/stars/Bugsterapp/scrapester)](https://github.com/Bugsterapp/scrapester/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/Bugsterapp/scrapester)](https://github.com/Bugsterapp/scrapester/commits/main)


[Documentation](https://docs.scrapester.lol) |
[Python SDK](https://pypi.org/project/scrapester/) |
[JavaScript SDK](https://www.npmjs.com/package/scrapester) |
[Playground](https://scrapester.lol)

Turn any website into LLM-ready clean data.

## Overview
Scrapester is a powerful web scraping tool that converts website content into clean, markdown-formatted data perfect for LLM processing. With support for both single-page scraping and full website crawling, Scrapester makes it easy to gather web content in a structured, consistent format.

## Features
- 🔍 **Smart Content Extraction**: Automatically removes noise and extracts meaningful content
- 📝 **Markdown Output**: Clean, structured content perfect for LLMs
- 🕷️ **Website Crawling**: Scrape entire websites with configurable depth and limits
- 🚀 **Multiple SDKs**: Official Python and JavaScript support
- ⚡ **High Performance**: Built for speed and reliability
- 🛡️ **Error Handling**: Robust error handling and rate limiting protection

## Installation

### Python
```bash
pip install scrapester
```

### JavaScript/TypeScript
```bash
npm install scrapester
# or
yarn add scrapester
```

## Quick Start

### Python
```python
from scrapester import ScrapesterApp

# Initialize the client
app = ScrapesterApp(api_key="your-api-key")

# Scrape a single page
result = app.scrape("https://example.com")
print(result.markdown)

# Crawl an entire website
results = app.crawl(
    "https://example.com",
    options={
        "max_pages": 10,
        "max_depth": 2
    }
)
```

### JavaScript/TypeScript
```typescript
import { ScrapesterApp } from 'scrapester';

// Initialize the client
const app = new ScrapesterApp('your-api-key');

// Scrape a single page
const result = await app.scrape('https://example.com');
console.log(result.markdown);

// Crawl an entire website
const results = await app.crawl('https://example.com', {
    maxPages: 10,
    maxDepth: 2
});
```

## Response Format

Scrapester returns clean, structured data in the following format:

```typescript
interface CrawlerResponse {
    url: string;          // The scraped URL
    markdown: string;     // Clean, markdown-formatted content
    metadata: {          // Page metadata
        title: string,
        description: string,
        // ... other meta tags
    };
    timestamp: string;   // ISO timestamp of when the page was scraped
}
```

## API Reference

### ScrapesterApp

#### Constructor
```typescript
new ScrapesterApp(
    apiKey: string,
    baseUrl?: string,    // default: "http://localhost:8000"
    timeout?: number     // default: 600 seconds
)
```

#### Methods

##### scrape(url: string)
Scrapes a single URL and returns clean, markdown-formatted content.

##### crawl(url: string, options?)
Crawls a website starting from the given URL. Options include:
- `maxPages`: Maximum number of pages to crawl
- `maxDepth`: Maximum crawl depth
- `includePatterns`: URL patterns to include
- `excludePatterns`: URL patterns to exclude

## Error Handling

Scrapester provides detailed error information through the `APIError` class:

```typescript
class APIError extends Error {
    statusCode?: number;
    response?: object;
}
```

Common error scenarios:
- `429`: Rate limit exceeded
- `400`: Invalid request
- `401`: Invalid API key
- `500`: Server error

## Development

### Running Tests
```bash
# Python
pytest tests/

# JavaScript
npm test
```

### Building from Source
```bash
# Python
pip install -e ".[dev]"

# JavaScript
npm install
npm run build
```

## Contributing
We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

## Support

- 📖 [Documentation](https://docs.scrapester.dev)
- 💬 [Discord Community](https://discord.gg/scrapester)
- 📧 [Email Support](mailto:support@scrapester.dev)

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
