# Contributing

This list exists because free-AI roundups get licenses and limits wrong. The most valuable contribution is a **correction with a source link**.

## What earns a merge

**Corrections to license claims.** If we say a model is non-commercial and it isn't, or vice versa, that is the highest-severity error in this list and we want it fixed immediately. Include the license URL.

**Corrections to published limits.** Only useful if the provider publishes them. Link the provider's own docs, not an aggregator.

**New tools that are genuinely free** and genuinely good. See the bar below.

## The bar for inclusion

A tool gets added if we can answer all three:

1. **Is the license clear?** Link to the license file. If the code license and the weight license differ, say so — that is the interesting part.
2. **Does it actually run?** Not a dead repo, not a "coming soon", not a paid product with a free tier that expires in 7 days.
3. **Is it free in a way that survives scrutiny?** Free tier that can vanish at any moment goes in the table *with* a warning, not as a recommendation.

## What does not get added

- Uncensored or "abliterated" builds from personal accounts. The technique is legitimate but the provenance is unverifiable, and a modified weight file can be fine-tuned on anything.
- SEO listicles, courses, or affiliate content.
- Anything whose only claim is a GitHub star count.
- Models where the only documentation is a Twitter thread.

## How to submit

Open an issue using the **Broken link / wrong info** template. For anything license-related, the fastest path is a direct PR against the table row in question.

If you are correcting the Spanish version, note that `README.es.md` is a full translation, not a summary. Keep them in sync — a fix to one without the other is an incomplete fix.

## Style

- **Cite the source inline.** A number without a source is a rumour.
- **Label confidence honestly.** "Provider-published" and "community-reported" are not the same and the distinction is the entire value of the list.
- **Lead with the trade-off.** A tool with a caveat is more useful than a tool that sounds free.
- No emoji beyond section markers. This is a reference document, not a social post.

## Verifying a hardware claim

If you add a VRAM or RAM figure, say which model variant, which quantization, and which resolution/frame count you measured. "Needs 24GB" is meaningless — Wan2.2 has variants from 3.4GB to 80GB.

## Code of conduct

Be accurate and be decent. See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).
