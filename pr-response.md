# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:** Renamed `save_to_watchlist` to `add_to_watchlist` in `services/watchlist_service.py` to match the project's naming convention. Updated the corresponding call site in `routes/watchlist/watchlist.py`.
**How I verified:** Searched the codebase for any remaining instances of `save_to_watchlist` and verified the route functions correctly.

## Comment 2 — Deduplication
**What I did:** Added a database query before creating a new `WatchlistEntry` to check if an entry with the given `user_id` and `film_id` already exists. Added an `AlreadyInWatchlistError`.
**How I verified:** Tested by attempting to add the same film twice and confirming that an `AlreadyInWatchlistError` is raised.

## Comment 3 — Missing test
**What I did:** Created `tests/test_watchlist.py` and wrote `test_add_to_watchlist_nonexistent_film_raises`.
**How I verified:** Ran `pytest tests/test_watchlist.py -v` and confirmed the test passes when providing an invalid film ID.

## Comment 4 — Default visibility
**My position:** I decided to keep the default as `public=True`.
**Reasoning:** CineLog is a community-driven app. Making watchlists public by default encourages social discovery and interaction among users.
**Tradeoff acknowledged:** The tradeoff is user privacy. Users who don't realize their watchlists are public might accidentally share viewing intentions they prefer to keep private. We can mitigate this by clearly labeling the visibility on the UI.

## Comment 5 — Sort order
**My position:** I agree with the maintainer and changed the default sort order to "date added" descending.
**Reasoning:** When users check their watchlist, they are usually looking for the movie they just decided they wanted to watch. Showing the most recently added films at the top aligns better with immediate user intent.
**Engagement with reviewer's point:** The reviewer correctly pointed out that "recent additions" are the primary use case. While alphabetical sorting is good for scanning a massive library, watchlists are typically shorter, action-oriented lists where chronological order is more practical.
## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->