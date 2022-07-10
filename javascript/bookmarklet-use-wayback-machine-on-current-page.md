# `[Bookmarklet]` - Use Wayback Machine for the current URL

The [Wayback Machine](https://archive.org/web/) is a free tool that allows you to see historical versions of websites. It captures snapshots of websites at certain intervals so even if a website goes offline or changes substantially, the snapshots remain accessible forever.

## User Story

- I want to easily view historical snapshots of the current website I'm on.
- If I'm visiting a webpage that no longer exists (broken URL) and I'm not redirected to a generic 404 URL, I want to see what the page looked like when it was live.

## Solution

Use your favorite browser to make a bookmark and paste this as the URL.

I named my bookmarklet as the ⏪ symbol. In my mind, it's an obvious association because it _rewinds_ web history and shows the old version of the site.

```javascript
javascript: (() => {
  window.location.replace(
    `https://web.archive.org/web/*/${window.location.href}`
  );
})();
```

When you visit a broken URL (that doesn't redirect you to a 404 URL) or want to see an older snapshot of the page, click your bookmarklet. Enjoy! 🎉
