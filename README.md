# Crypto News MCP Server

An MCP server that provides real-time cryptocurrency news sourced from [NewsData](https://newsdata.io/) for AI agents.

![GitHub](https://img.shields.io/github/license/kukapay/crypto-news-mcp) 
![GitHub last commit](https://img.shields.io/github/last-commit/kukapay/crypto-news-mcp) 
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
[![smithery badge](https://smithery.ai/badge/@kukapay/crypto-news-mcp)](https://smithery.ai/server/@kukapay/crypto-news-mcp)

## Features

- **Tool: Latest News Headlines** - Fetch the most recent cryptocurrency news headlines.
- **Tool: Crypto News Search** - Search for news articles by cryptocurrency or keyword with pagination support using the `nextPage` API feature.
- **Prompt: News Summary** - Generate a prompt to summarize news for a given cryptocurrency or topic.

## Prerequisites

- Python 3.10+
- A [Newsdata.io API key](https://newsdata.io/register?ref=kukapay) 
- Git (for cloning the repository)

## Installation

### Installing via Smithery

To install Crypto News for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@kukapay/crypto-news-mcp):

```bash
npx -y @smithery/cli install @kukapay/crypto-news-mcp --client claude
```

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/kukapay/crypto-news-mcp.git
   cd crypto-news-mcp
   ```

2. **Install Dependencies**:
   ```bash
   pip install mcp[cli] httpx python-dotenv
   ```
   
4. **Install the server as a plugin for Claude Desktop**:
    ```bash
    mcp install main.py --name "CryptoNews"
    ```

    Or configure MCP-compatible clients manually:
    ```
    {
      "mcpServers": { 
        "Crypto News": { 
          "command": "python", 
          "args": [ "path/to/crypto-news-mcp/main.py"],
          "env": {
            "NEWS_API_KEY": "your_newsdata_api_key_here"
          }
        } 
      }
    }
    ```

## Available Tools and Prompts

1. **Tool: `get_latest_news`**  
   Fetches the latest cryptocurrency news headlines.
   - **Usage**: Call `get_latest_news()` in an MCP client.
   - **Output**: A string of headlines with publication dates.
   - **Example**:
     ```
     Bitcoin Price Surges to New High (Published: 2025-04-06T12:00:00Z)
     Ethereum ETF Approval Rumors Grow (Published: 2025-04-06T10:30:00Z)
     ```

2. **Tool: `get_crypto_news`**  
   Searches for news articles by keyword with pagination support.
   - **Parameters**:
     - `query (str)`: The cryptocurrency or keyword (e.g., "bitcoin").
     - `max_pages (int, optional)`: Number of pages to fetch (default: 1).
   - **Usage**: Call `get_crypto_news(query="bitcoin", max_pages=2)`.
   - **Output**: A formatted string with article titles, dates, and descriptions.
   - **Example**:
     ```
     Title: Bitcoin Hits $70K
     Date: 2025-04-06T12:00:00Z
     Description: Bitcoin surged past $70,000 amid bullish market trends.

     Title: Bitcoin Mining Report
     Date: 2025-04-06T09:00:00Z
     Description: New report highlights energy usage in BTC mining.
     ```

3. **Prompt: `summarize_news`**  
   Generates a prompt for summarizing news about a specific topic.
   - **Parameters**:
     - `query (str)`: The cryptocurrency or keyword.
   - **Usage**: Call `summarize_news(query="ethereum")`.
   - **Output**: A prompt string for an LLM to process.
   - **Example**:
     ```
     Please summarize the latest news about ethereum based on the following data:

     {{{{ get_crypto_news("ethereum") }}}}
     ```
## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
