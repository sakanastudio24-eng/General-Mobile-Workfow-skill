# Feed Backend, Ranking, and Social Graph Patterns

## Use This Reference For

- Designing timeline fan-out and personalized feed retrieval.
- Adding recommendation pipelines for "For You" and "Explore" surfaces.
- Shipping social feed backends quickly with practical infrastructure choices.

## Feed Backend Architecture Baseline

1. Split write path and read path.
2. Use append-only activity events as source of truth.
3. Build timeline materialization strategy:
   - Fan-out on write for fast reads.
   - Fan-out on read for high-celebrity/high-fanout accounts.
4. Add ranking layer after candidate generation.
5. Enforce moderation/safety filters before final ranking output.

## References (from provided repos)

- Stream Framework (Django activity feeds):
  - <https://github.com/tschellenbach/Stream-Framework>
- Stream JavaScript client concepts:
  - <https://github.com/getstream/stream-js>
- Microsoft recommenders examples:
  - <https://github.com/recommenders-team/recommenders>
- TensorFlow Recommenders:
  - <https://github.com/tensorflow/recommenders>
- Supabase platform repo (for auth/db/storage foundations):
  - <https://github.com/supabase/supabase>
- Instagramy (unofficial; use cautiously and do not rely on private/unstable interfaces):
  - <https://github.com/instagrampy/instagramy>

## Ranking Pipeline Blueprint

1. Candidate generation:
   - Follow graph
   - Interest graph
   - Freshness/trending pool
2. Feature enrichment:
   - User features
   - Content features
   - Context/session features
3. Multi-objective scoring:
   - Engagement
   - Retention
   - Safety and quality penalties
4. Re-ranking and dedup:
   - Diversity
   - Creator caps
   - Repetition suppression

## Service-Level Checklist

1. Define feed SLA by endpoint (p95 latency, error budget).
2. Add cursor-based pagination and idempotent page tokens.
3. Add replay-safe event ingestion for likes, follows, watches, shares.
4. Add anti-abuse signals and rate limits.
5. Add observability:
   - Feed request traces
   - Rank feature freshness lag
   - Candidate pool hit rates

## Failure Patterns to Avoid

1. Tight coupling between feed serving and heavy model inference.
2. Missing fallback rankings when model service is degraded.
3. Ranking without moderation/safety gating.
4. Unbounded fan-out for high-degree nodes.

## Primary Sources

- Stream Framework: <https://github.com/tschellenbach/Stream-Framework>
- Stream JS: <https://github.com/getstream/stream-js>
- Microsoft Recommenders: <https://github.com/recommenders-team/recommenders>
- TensorFlow Recommenders: <https://github.com/tensorflow/recommenders>
- Supabase: <https://github.com/supabase/supabase>
- Instagramy: <https://github.com/instagrampy/instagramy>
