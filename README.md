# UNLAV Shopify CSV Catalog Check

This remote MCP server checks Shopify product CSV exports before import or catalog maintenance. It reports duplicate and whitespace-colliding SKUs, missing variant data, repeated option combinations, conflicting product metadata, and suspicious duplicate groups.

The paid tool is `check_shopify_catalog_csv`. A call costs **3 USDC on Base mainnet** through x402 v2. `ping` and `catalog_service_info` are free.

- MCP Streamable HTTP endpoint: `https://7days.unlavsofts.xyz/mcp`
- Legacy MCP SSE endpoint: `https://7days.unlavsofts.xyz/mcp/sse`
- Service page: `https://7days.unlavsofts.xyz/services/catalog-check/`
- Health endpoint: `https://7days.unlavsofts.xyz/mcp/health`
- Network: Base mainnet (`eip155:8453`)
- Asset: USDC

Input is the complete UTF-8 CSV text and an optional filename. The service processes CSV data in memory and does not write it to payment receipt logs. The result is a JSON diagnostic report bound to the exact input with SHA-256. The service does not connect to or modify a Shopify store.

Limits: 10 MiB and 10,000 product rows per call.

## MCP client configuration

Use an MCP client that supports Streamable HTTP and x402 MCP payments. Add the primary endpoint above, call `catalog_service_info` to inspect the current terms, and then call `check_shopify_catalog_csv` with `csv_text`. The SSE endpoint remains available for older clients.

An unpaid call returns an x402 payment requirement containing the exact amount, Base network, USDC asset, receiving address, and Bazaar discovery metadata. The client signs the payment authorization; this repository contains no wallet secret or signing key.

## Support

Contact `unlav-revenue-agent@agentmail.to` with the request timestamp and transaction hash. Do not email store credentials or customer CSV data.
