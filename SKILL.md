---
name: ai-citation-finder
description: Use to find the pages that AI assistants (ChatGPT, Google AI Overviews, Perplexity, Gemini) read and cite when buyers ask who to choose, check whether the business is on each one, and turn every page into a concrete action (outreach email, submission form, listing to claim, helpful forum reply, video to make). The fix step after ai-visibility-checker. Use for "get on the lists AI cites", "why does ChatGPT recommend my competitor", AI citation opportunities, GEO off-page, or "how do I get mentioned by AI".
---

# AI Citation Finder

The AI Visibility Checker tells you whether AI names you. This skill tells you
**which pages make AI name someone else, and how to get onto each one.**

AI assistants rarely invent a recommendation. They read a small set of pages
(independent "best of" lists, directories, review sites, Reddit threads, YouTube
videos) and repeat what those pages say. In most markets that set is 5 to 30
pages. Get onto them and you get into the answer.

Works free with Claude's web search. A DataForSEO connector makes it better, with
real ChatGPT answers and their cited sources instead of Claude's own.

## Before you start

1. **Web search must be on.** Without it you cannot see any sources. If it is off,
   say so and stop.
2. **Read `site-brief.md`** if it exists: brand name, domain, what they sell, where,
   competitors. If there is no brief, ask for those five things in one message.
3. **Check for the DataForSEO connector** (tools mentioning `chat_gpt`,
   `llm_responses`, `llm_mentions`). If present, use it in Step 2. If not, use the
   free path and say once, in the report notes, that the data came from Claude's
   own search, not live ChatGPT answers.
4. **Check for the Gmail connector.** If present, outreach becomes Gmail DRAFTS.
   If not, drafts go in the report and a file.

## Step 1: The buyer questions

Write 5 to 8 questions a buyer asks when they are ready to **choose**, not learn:
"best [service] in [city]", "top [product] for [audience]", "[competitor]
alternatives", "is [competitor] worth it", "[service] near [area] reviews".

If `05-ai-visibility.html` or a gap list exists, take its top gaps first.

Show the list and wait for an OK or edits. This is the only stop before the report.

## Step 2: Collect the sources behind each answer

For each question:

**Free path (always available):**
- Web search the question. Keep the top 10 results.
- Answer the question as an AI assistant would, using what you found, and list
  the sources you would cite. Record which businesses the answer names.

**With DataForSEO (better):**
- Get the live ChatGPT answer for the question (ChatGPT scraper / LLM responses).
  Record the businesses it names and every URL it cites.
- Optionally pull LLM-mentions top pages / top domains for the question's keyword.

Record per question: businesses named, is this brand named (yes / no), and the
source URLs.

Budget: at most 8 questions, about 10 sources each. Say how many you checked.

## Step 3: Clean the list

Merge every source URL into one list and count how many questions each one
showed up in (its reach). Then **drop**:
- competitors' own websites
- competitors' own "best of" lists that rank themselves first
- pages not updated in 2+ years (say so if no date is visible)
- pages not about this service or area
- dead pages

Classify what's left as one of: `list` (independent best-of list), `directory`,
`review` (review platform), `forum` (Reddit, forums, communities), `video`
(YouTube), `news`, `other`.

## Step 4: Check the business on each page

Open each kept page. Is the brand on it? Mark **yes only if you can quote the line**.
If you could not open a page, mark it `unknown` and say why. Never guess.

## Step 5: The route onto each page

Pick one route per page:
- **EDITORIAL:** a person writes it. Find the author and a PUBLIC contact
  (contact page, email shown on the site, LinkedIn, X). Never guess an email.
- **SUBMISSION:** a form or "get listed" page. Give the URL.
- **CLAIM:** a directory or review profile to claim or create.
- **REVIEWS:** inclusion depends on reviews on that platform. Quote the rule if published.
- **PAID:** inclusion is sold. Quote the wording and price if public, and say if a free route exists.
- **COMMUNITY:** a thread. Quote the self-promotion rule. Only a genuinely helpful
  answer, with a disclosure line, or "skip".
- **MAKE IT:** a YouTube video or article that answers the question and doesn't exist yet.
- **NOT WINNABLE:** closed or owned by a rival. Keep it in the table, out of the action list.

Add effort (low / medium / high) and how fast it usually shows up in answers
(days / weeks / months). Sort the action list fastest wins first. A quick win is
low effort and days or weeks.

## Step 6: Draft the work (never send, never post)

For each EDITORIAL page in the top 5: open it, find one specific true detail about
it (quote it), and write an email under 120 words: one line showing you read the
page, one line on who you are, a 2 to 3 sentence write-up of the business in that
page's own style they could paste straight in, an offer of photos or a customer
quote. No link request, no flattery, no "I hope this finds you well".
- Gmail connector present: create each as a **draft**. Never send.
- Otherwise: save all drafts to `06-outreach-drafts.md`.

For SUBMISSION pages: list the form fields and fill them from the brief. Mark
anything the brief doesn't cover.

For COMMUNITY threads: draft the helpful answer only if you can genuinely help.

Facts in drafts come only from the brief or the business's own site. Mark anything
you'd have to guess as `[CONFIRM]`.

## Output

**`06-ai-citations.html`**: fill `templates/ai-citations.html.template` with a
`data.json`, then render:

```
python3 scripts/render.py templates/ai-citations.html.template data.json 06-ai-citations.html
```

Tokens: `SUBJECT`, `HEADLINE`, `SUBHEAD`, `RUN_DATE`, `DATA_WINDOW`, `BRAND`,
`QUESTIONS_CHECKED`, `SOURCES_COUNT`, `ON_COUNT`, `ON_CLASS` (`is-fail` when 0),
`NAMED_COUNT`, `QUICK_WINS`, `STANDING_HEADLINE`, `STANDING_VERDICT`,
`STANDING_NOTE`, `SOURCE_NOTE` (which data path was used), `DATA_NOTES`.

Row blocks:
- `QUESTION_ROW`: `ROW_QUESTION`, `ROW_NAMED`, `ROW_YOU` (Named / Not named),
  `ROW_YOU_CLASS` (pass / fail), `ROW_SOURCES` (count or top 2 domains)
- `SOURCE_ROW`: `ROW_PAGE`, `ROW_URL`, `ROW_TYPE`, `ROW_TYPE_CLASS` (list=comm,
  directory=nav, review=trans, forum/video/news/other=info), `ROW_REACH`
  ("3 of 6"), `ROW_ON` (On it / Not on it / Unknown), `ROW_ON_CLASS`
  (pass / fail / na), `ROW_ROUTE`
- `ACTION_ROW`: `ROW_ROUTE`, `ROW_EFFORT`, `ROW_SPEED`, `ROW_PAGE`, `ROW_WHY`, `ROW_ACTION`
- `DRAFT_ROW`: `ROW_PAGE`, `ROW_KIND`, `ROW_WHERE`
- `NEXT_ROW`: `ROW_NEXT`, `ROW_NEXT_WHY`

## Honesty rules

- "On it" needs a quoted line. Zero pages is a real answer: say it plainly.
- Never invent a contact, a date, a price or a citation.
- AI answers change between runs. Say when the data was pulled and that one run is noise.
- Nothing gets sent, posted or submitted by this skill. The person presses send.
- No review gating, no fake reviews, no promotional forum posts.

## Closing the loop

> Work the action list this week, then re-run this skill and `ai-visibility-checker`
> on the same day next month. The number to watch is how many of these pages you're on.
