# LexicRo — Romanian Language Intelligence Infrastructure

> Building the Romanian NLP API that should already exist.

---

If you've ever tried to do anything programmatic with Romanian text — parse a sentence, get the correct inflected form of a noun, check whether a verb conjugation is right — you've probably hit the same wall.

There's no clean API for it. You end up scraping DEXonline, wrestling with verbecc's Romanian support, or calling a general-purpose LLM and hoping it gets the grammar right. None of that is good enough for production.

**The specific gap:** given an arbitrary Romanian sentence, return for each token its lemma, part of speech, grammatical case, number, gender, person, and tense. This is what spaCy does for English, French, and German in a `pip install`. For Romanian, no equivalent exists as a callable REST API.

Romanian NLP tooling currently sits at roughly **15% of what exists for English**. The academic resources are there — DEXonline, RoLEX, the UD Romanian Treebank — they're just not packaged in a way that developers can actually use. That's what LexicRo is for.

---

## What we're building

A hosted REST API — with an open-source core — covering the endpoints Romanian developers actually need:

```
# Morphological analysis
POST /analyze
→ lemma, POS, case, gender, number, person, tense per token

# Full verb conjugation
GET /conjugate/{verb}
→ all moods and tenses, including perfect simplu and viitor I

# Noun/adjective inflection
GET /inflect/{word}
→ all cases, numbers, genders

# Lexical lookup
GET /lookup/{word}
→ definition, gender, plural, etymology (DEXonline data)

# CEFR difficulty scoring
POST /difficulty
→ A1–C2 level estimate, calibrated to Romanian B1/B2 exams
```

The core is open source (MIT). Model weights are CC BY-NC — free for research and non-commercial use, commercial use goes through the hosted API. A generous free tier (1,000 req/day, no credit card) from day one.

---

## Built on what already exists

We're not starting from scratch. The data and models are there — they just need engineering.

**Data:** DEXonline (313k+ lemmas), RoLEX (330k morphosyntactic entries), UD Romanian Treebank (9k+ annotated sentences), OSCAR Romanian corpus.

**Models:** Fine-tuning `bert-base-romanian-cased-v1` for morphological tagging. verbecc for conjugation, extended with full B1+ tense coverage. ML-predicted conjugation templates for unknown verbs.

**Infrastructure:** FastAPI, Docker, full OpenAPI spec, Python and JavaScript SDKs.

### Roadmap

| Phase | Scope | Timeline |
|---|---|---|
| 1 | Conjugation + lexical lookup endpoints · Public launch · Free tier | 3 months |
| 2 | Romanian BERT fine-tuning · `/analyze` morphological endpoint | 6 months |
| 3 | Grammar checker · CEFR scorer · Pro and Academic tiers | 9–12 months |
| 4 | Enterprise features · On-premise packaging · Custom fine-tuning | 12–18 months |

Phase 1 is the straightforward part — wrapping verbecc and DEXonline cleanly. That ships first. The morphological analyser is the hard part and follows in phase 2.

---

## What we're looking for right now

**01 — Honest feedback on the endpoint design**
Does this cover what you actually need? What's missing? What would make you use this over your current approach?

**02 — Early users willing to test v1**
If you're building something with Romanian text — edtech, content tools, document processing, language learning — we'd like to talk. Early users get priority feature input and free Pro access during the build phase.

**03 — Academic and institutional connections**
We're pursuing EU grant funding (Horizon Europe, CEF Digital, Digital Europe Programme). If you're at a Romanian university or research institution and this is relevant to your work, a conversation — or even a letter of support — makes a meaningful difference.

**04 — Anyone who's built adjacent to this problem**
If you've scraped DEXonline, built a Romanian spell checker, worked with the UD treebank, or tried to fine-tune anything on Romanian text — we'd genuinely like to hear what you learned.

---

## On the business model

Open core, hosted API, freemium tiers. The free tier is real and permanent — not a trial. Commercial tiers fund continued development. If you want to self-host the whole thing, the code will be there.

We're pursuing EU language equality grants partly because Romanian deserves proper NLP infrastructure regardless of whether the commercial model scales immediately. Romanian is an official EU language spoken by 24 million people, and it should have the same digital language tooling as French or German. The [EU Language Equality initiative](https://digital-strategy.ec.europa.eu/) sets a 2030 deadline for exactly this — we're building toward it.

---

## Get involved

| | |
|---|---|
| 🌐 **Website** | [lexicro.com](https://lexicro.com) |
| 📬 **Waitlist** | [lexicro.com/waitlist](https://lexicro.com/waitlist) |
| 💬 **Feedback** | [lexicro.com/feedback](https://lexicro.com/feedback) |
| ✉️ **Email** | [contact@lexicro.com](mailto:contact@lexicro.com) |

---

*LexicRo — April 2026 — Working in public from day one.*
