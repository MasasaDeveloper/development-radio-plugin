# Development Radio plugin

Development Radio is a podcast for senior engineers: what is new in AI, security and software development, plus the engineering practices behind good decisions. This plugin gives Claude read access to the show's published episode index, so it can find an episode on a topic and return its findings, the primary sources it cites and its timed transcript.

The hosts, Maya and Alex, are AI-generated voices and characters. Every episode links its sources.

## What is in the plugin

- **A connector** to the show's read-only MCP server at `https://developmentradio.dev/mcp` (Streamable HTTP, no account or key).
- **One skill**, `episode-lookup`, which describes when the tools help and how to pass on the sources.

There are no hooks, commands, scripts or local programs.

## Tools

| Tool | What it returns |
|---|---|
| `search_episodes` | Episodes matching your keywords, each with the best-matching passage and the URLs of the sources it cites |
| `list_episodes` | Episodes newest first, with ids, dates and one-line descriptions |
| `get_episode` | One episode's summary, takeaways, chapters and every cited source |
| `get_transcript` | One episode's full timed transcript as Markdown |

All four are read-only.

## Install

### Claude Code

```sh
claude plugin marketplace add MasasaDeveloper/development-radio-plugin
claude plugin install development-radio@development-radio
```

Or try it for one session from a clone of this repository:

```sh
claude --plugin-dir ./development-radio-plugin
```

### claude.ai and Claude Desktop

Add a custom connector with this URL:

```
https://developmentradio.dev/mcp
```

### Other MCP clients

Any client that supports remote Streamable HTTP servers can use the same URL. A ready `server.json` for the MCP Registry is in this repository.

## Example prompts

- "What has Development Radio covered on the Nginx HTTP/2 vulnerability, and what are the primary sources?"
- "Find the episode on Redis lock expiry and quote the part about fencing tokens, with its timestamp."
- "List the latest Development Radio episodes."

## Privacy

When Claude calls a tool, the plugin sends that tool's arguments (your search keywords or an episode id) to `https://developmentradio.dev/mcp`. It sends nothing else: no conversation content, files or account details. The server needs no sign-in, returns only what is already public on developmentradio.dev, and keeps no record of who asks or what they ask. The host, Cloudflare, keeps standard server logs, as it does for any page on the site.

To see which episodes are useful and where the catalogue has gaps, the server keeps aggregate usage counts in Cloudflare Workers Analytics Engine: for each request, the tool used, whether it succeeded, how many results it returned, whether a search found nothing, and the ids of the episodes it returned. It does not store your search keywords, the ids or other arguments you send, your IP address, client details or anything else that identifies you or your conversation. Cloudflare keeps these counts for three months.

Privacy policy: https://developmentradio.dev/privacy/

## Problems and questions

Open an issue in this repository: https://github.com/MasasaDeveloper/development-radio-plugin/issues

## Licence

The plugin files in this repository are released under the MIT Licence; see `LICENSE`. The episodes, transcripts and show notes served by the connector belong to Development Radio and are not covered by that licence.
