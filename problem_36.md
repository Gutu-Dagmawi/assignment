# Problem 36: Distributed Web Crawler URL Manager

## Problem Description
You are building the URL frontier for a distributed web crawler. The system must manage URLs to visit, avoid duplicates, respect domain rate limits, and prioritize important pages.

### The System Rules
1.  **URL Properties**: Each URL has:
    *   `URL String`
    *   `Domain` (extracted from URL)
    *   `Priority` (1-10, higher = more important)
    *   `Discovery Time`
2.  **Duplicate Detection**:
    *   Never visit the same URL twice.
    *   Maintain a "Visited Set" (simulated with sorted array + binary search).
3.  **Domain Rate Limiting**:
    *   No more than `R` requests to the same domain within `T` time units.
    *   If a domain is "cooling down", skip to the next URL from a different domain.
4.  **Priority Scheduling**:
    *   Higher priority URLs should be visited first.
    *   Within the same priority, use FIFO.

## Must Use Data Structures
*   **Max-Heap**: For priority-based URL selection.
*   **Queue**: For FIFO within priority tiers (or Array of Queues by priority).
*   **Sorted Array + Binary Search**: For the Visited Set (duplicate detection).
*   **Circular Array**: For per-domain rate limit tracking (last `R` request times).

## Operations to Implement (CLI Commands)
*   `ADD_URL <url> <priority>`: Add a URL to the frontier.
*   `CRAWL`: Fetch the next valid URL (highest priority, not duplicate, domain not rate-limited).
*   `SET_RATE_LIMIT <r> <t>`: Configure rate limiting.
*   `STATUS`: Show frontier size, visited count, domain stats.

## Sample Execution

```text
> SET_RATE_LIMIT 2 5  (2 requests per domain per 5 time units)

> ADD_URL https://example.com/page1 5
> ADD_URL https://example.com/page2 5
> ADD_URL https://other.com/home 8

> CRAWL (Time 0)
Crawled: https://other.com/home (Priority 8).

> CRAWL (Time 1)
Crawled: https://example.com/page1 (Priority 5).

> CRAWL (Time 2)
Crawled: https://example.com/page2 (Priority 5).

> ADD_URL https://example.com/page3 10
> CRAWL (Time 3)
Domain 'example.com' rate-limited (2 requests in last 5 units). Skipping...
No other URLs available. Idle.

> CRAWL (Time 6)
Rate limit expired. Crawled: https://example.com/page3 (Priority 10).
```
