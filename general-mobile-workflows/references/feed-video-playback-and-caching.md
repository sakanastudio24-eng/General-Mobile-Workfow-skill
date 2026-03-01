# Feed Video Playback and Caching

## Use This Reference For

- Autoplaying video inside scrolling feeds.
- Reducing startup latency and rebuffering.
- Designing player lifecycle in Android/iOS feed cells.

## Playback Lifecycle Rules

1. Keep one active player for the focused item.
2. Preload next item metadata and warm media pipeline where possible.
3. Pause immediately on item losing focus or app background events.
4. Resume only when visibility threshold is met.
5. Release off-screen resources aggressively on low-memory signals.

## Android References (from provided repos)

- ExoPlayer repository:
  - <https://github.com/google/ExoPlayer>
  - Status note: repository indicates deprecation in favor of AndroidX Media3.
- AndroidVideoCache:
  - <https://github.com/danikula/AndroidVideoCache>
  - Useful for HTTP caching patterns; evaluate format/protocol support before production use.

## iOS References (from provided repos)

- VIKit:
  - <https://github.com/VideoFlint/VIKit> (verify current availability and maintenance before production dependency)

## Practical Tuning Checklist

1. Track time-to-first-frame and rebuffer ratio per network tier.
2. Keep adaptive bitrate enabled and set conservative startup bitrate.
3. Prefetch only a small window (for example, next one or two items) to avoid bandwidth waste.
4. Cache short replay segments for immediate back-scroll playback.
5. Guard autoplay with mute-by-default and user intent rules where required by product policy.

## Failure Patterns to Avoid

1. Instantiating one full player per visible and preloaded cell.
2. Prefetching too aggressively on metered or constrained networks.
3. Ignoring app lifecycle and audio focus transitions.
4. Caching without eviction policy or disk budget controls.

## Primary Sources

- ExoPlayer repo (deprecated in favor of Media3): <https://github.com/google/ExoPlayer>
- AndroidVideoCache: <https://github.com/danikula/AndroidVideoCache>
- VIKit: <https://github.com/VideoFlint/VIKit>
- Android Media3 docs: <https://developer.android.com/media>
