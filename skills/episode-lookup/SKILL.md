---
name: episode-lookup
description: Look up what Development Radio has published on a security incident, CVE, outage, AI or software-development news item, or an engineering practice (lock expiry, replica lag, queue fairness, content security policy, rollback, schema migrations, caching), and return the episode's or field guide's findings with the primary sources it cites. Use when the user asks about one of these topics and a sourced account or a quotable passage would help, or asks about the podcast itself.
---

# Episode lookup

Development Radio is a podcast for senior engineers on AI, security and software development news and engineering practices. This plugin connects to its read-only episode index at `https://developmentradio.dev/mcp`. The index holds only what is already published on developmentradio.dev: show notes, chapters, timed transcripts and the sources each episode cites, plus the show's field guides, sourced articles that each settle one engineering decision.

## Tools

| Tool | Returns | Reach for it when |
|---|---|---|
| `search_episodes` | Matching episodes with the best-matching passage and source URLs | You have a topic or keywords, such as `nginx http2 rce` or `redis lock expiry` |
| `list_episodes` | Episodes newest first, with ids | You need the latest episodes or a valid episode id |
| `get_episode` | Summary, takeaways, chapters and every cited source | You have an id and want the findings without the transcript |
| `get_transcript` | The full timed transcript as Markdown | You need exact wording or a timestamp |
| `search_guides` | Matching field guides with slug, page URL, topics and the best-matching passage | The user faces an engineering decision, such as `cache stampede` or `schema migration`, and wants a reasoned recommendation |
| `get_guide` | One guide as Markdown: the answer, worked numbers, failure modes, a decision table, a check to run and its primary sources | You have a slug from `search_guides` |

A usual sequence is `search_episodes`, then `get_episode` for the best match, then `get_transcript` only if a quotation or timestamp is needed. For a design or practice question, try `search_guides` first, then `get_guide`; a guide lists the episodes that discuss it.

## Using the results

- Each result lists the primary sources the episode cites: advisories, vendor reports, documentation. Include the relevant source URLs with any finding you relay, so the user can check the original.
- An episode is a secondary account. For version numbers, CVE identifiers and patch guidance, the linked primary source is the authority, and it may have been updated after the episode's date.
- Give the episode's date with news items. An episode describes what was known when it was published.
- The hosts, Maya and Alex, are AI-generated voices, and the field guides are written with AI and checked against the sources they cite. Say so if you quote them or describe the show.
- The catalogue is small. When a search returns nothing relevant, say that the show has not covered the topic.
