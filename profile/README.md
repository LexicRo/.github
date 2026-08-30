# LexicRo

Hosted REST API for Romanian morphological analysis and verb conjugation.

## The gap

If you've tried to do anything programmatic with Romanian text — parse a sentence, get a noun's inflected form, check whether a verb conjugation is right — you have probably hit the same wall: scraping a dictionary site, wrestling with partial library support, or asking a general-purpose LLM and hoping it gets the grammar right.

Given an arbitrary Romanian sentence, return for each token its lemma, part of speech, case, number, gender, person and tense. This is what spaCy does for English, French and German in a `pip install`. LexicRo is that as a hosted, versioned HTTP contract for Romanian: callable without shipping a model, stamping the version it answered with, and telling you per token whether the answer came from a lexicon or a prediction.

## What it is

LexicRo's product surface is two endpoints, both live:

```
POST /analyze
GET /conjugate/{verb}
```

`/analyze` returns, for every token in a Romanian sentence, its lemma, part of speech (UPOS), Universal Features, and a `source` field naming where that answer came from — a lexicon lookup, a suffix rule, or a model prediction. `source` is provenance, never a confidence score; the guide says so in its own words: *"`source` is not a trust signal."*

Where the lexicon knows more than one reading for a token, the response exposes them in `candidates` instead of silently picking one — about 35.68% of tokens carry a `candidates` list, measured on the UD Romanian RRT test split.

`/conjugate` returns a verb's conjugation table.

## Try it

- **Demo:** [demo.lexicro.com](https://demo.lexicro.com) — no key required.
- **Guide:** [api.lexicro.com/guide](https://api.lexicro.com/guide) (`/analyze`) and
  [api.lexicro.com/guide/conjugate](https://api.lexicro.com/guide/conjugate) (`/conjugate`) — full request/response shapes, rate limits, and known limitations.

## Free tier

The free tier is real and permanent — not a trial. 1,000 requests/day with a key, 10/day
anonymous.

---

## Versioning

Every response stamps `model_version`. The weights, the lexicon snapshot, and the MSD→UD conversion table version together as one unit, and the engine itself is pinned by tag — so pinning against a `model_version` tells you exactly what you're pinned to.

## License

The core is open source (MIT). Licensing terms for the model weights are still being worked out. The weights themselves are not distributed.

## Roadmap

| Phase | Scope |
|---|---|
| 1 | Conjugation + lexical lookup endpoints · Public launch · Free tier |
| 2 | Romanian BERT fine-tuning · `/analyze` morphological endpoint |
| 3 | Grammar checker · CEFR scorer · Pro and Academic tiers |
| 4 | Enterprise features · On-premise packaging · Custom fine-tuning |

## What we're looking for right now

**01 — Honest feedback on the endpoint design**
Does this cover what you actually need? What's missing? What would make you use this over your current approach?

**02 — Early users willing to test v1**
If you're building something with Romanian text — edtech, content tools, document processing, language learning — we'd like to talk. Early users get priority feature input.

**03 — Academic and institutional connections**
We're pursuing EU language-technology funding. If you're at a Romanian university or research institution and this is relevant to your work, a conversation — or even a letter of support — makes a meaningful difference.

**04 — Anyone who's built adjacent to this problem**
If you've scraped DEXonline, built a Romanian spell checker, worked with the UD treebank, or tried to fine-tune anything on Romanian text — we'd genuinely like to hear what you learned.
