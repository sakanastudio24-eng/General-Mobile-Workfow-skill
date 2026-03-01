# Feed UI and Pagination Patterns

## Use This Reference For

- TikTok/Instagram-style vertical full-screen feed experiences.
- Snapping/paging behavior, list modeling, and infinite scroll.
- Cross-platform feed architecture decisions in Android and iOS stacks.

## Core Feed UI Rules

1. Keep one dominant visible item at a time for short-video feeds.
2. Snap to item boundaries; avoid partial-card resting states in full-screen feed mode.
3. Separate concerns:
   - Feed controller (paging, prefetch, retry)
   - Item renderer (video/image/text states)
   - Analytics emitter (impressions, dwell, completion)
4. Preserve scroll position and restore player state after app background/foreground.

## Android References (from provided repos)

- Recycler paging/snapping:
  - <https://github.com/taehwandev/RecyclerViewPager>
  - <https://github.com/jorgecastilloprz/AndroidRecyclerViewSnappingExamples>
- Complex RecyclerView model architecture:
  - <https://github.com/airbnb/epoxy>
- Official paging samples (historical):
  - <https://github.com/android/architecture-components-samples> (archived; use as legacy reference)
- Production-scale modern app sample:
  - <https://github.com/android/nowinandroid>

## iOS References (from provided repos)

- Skeleton loading (historical):
  - <https://github.com/facebookarchive/Shimmer> (archived; treat as concept reference)
- Paging layout approach:
  - <https://github.com/ethanhuang13/UICollectionViewPagingLayout> (verify current availability before depending on it)
- Infinite scrolling example:
  - <https://github.com/tedious/InfiniteScrollView> (verify current availability before depending on it)

## Implementation Checklist

1. Define page size and prefetch window (for example, current ±1 item).
2. Add deterministic item keys/ids for stable diffing.
3. Add loading placeholders and empty/error states.
4. Add offline fallback with cached feed slice and retry controls.
5. Emit analytics for:
   - Impression start
   - 2-second view
   - Completion
   - Like/share/follow actions

## Failure Patterns to Avoid

1. Rendering every cell as a live player instance.
2. Running heavy ranking logic on UI threads.
3. Mixing pagination state with individual cell state.
4. Emitting duplicate impressions during rapid snap transitions.

## Primary Sources

- RecyclerViewPager: <https://github.com/taehwandev/RecyclerViewPager>
- Android snapping examples: <https://github.com/jorgecastilloprz/AndroidRecyclerViewSnappingExamples>
- Airbnb Epoxy: <https://github.com/airbnb/epoxy>
- Architecture samples (archived): <https://github.com/android/architecture-components-samples>
- Now in Android: <https://github.com/android/nowinandroid>
- Shimmer (archived): <https://github.com/facebookarchive/Shimmer>
- UICollectionView paging layout: <https://github.com/ethanhuang13/UICollectionViewPagingLayout>
- InfiniteScrollView: <https://github.com/tedious/InfiniteScrollView>
