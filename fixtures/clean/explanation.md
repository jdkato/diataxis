# Caching

The build is cached by layer, because a layer rarely changes between builds. The page is served from the cache so that the first request is fast.

The trade-off is staleness: a cached page can be a build behind. The reference lists the flags that tune it.
