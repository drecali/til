# `[DevTools]` - Filter failed or pending network requests

## User Story

- As a developer/researcher using Chrome DevTools to work on a web project, sometimes I want an easy way to focus on failed network requests so I can investigate and debug more efficiently.
- I hate visual clutter and scrolling so it'd be ideal to hide all other requests.

## Background

Modern websites tend to make a **ton** of requests so the Network panel of Chrome's DevTools can be overwhelming without some filtering. A common filter to use is `Fetch/XHR`. This can help somewhat, but it can still leave a lot of requests. If you're developing a website, it may be useful to see **all** failed requests without any other filter applied.

## Solution

In the `Network` tab of DevTools there's a text input element with a placeholder that says `Filter`. Click there and input `status-code:0` (or whatever status code is relevant to you). This refers to [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status), the most famous/common of which are `404`, `200`, `500`, and `418`.

`status-code:0` doesn't refer to an actual status. Rather, it refers to the lack of a valid status code. These include CORS errors, canceled requests, requests blocked on the client, or requests that could not be sent for some reason.

💥 Bonus: Check out the video to see what `status-code:0` also shows `pending` requests. It's really nice to see how many requests are pending at a given time.

![image](https://user-images.githubusercontent.com/24983797/176451248-8c41964c-4a81-4d39-bb40-496c32b41b76.png)

https://user-images.githubusercontent.com/24983797/176448510-2feb7c02-b798-4044-9ab4-d22843ce7fcc.mov

## Why not just sort by the `Status` column?

That is also a decent option with its own pros and cons

- Pros:
  - Doesn't hide any requests you may want to see
  - No typing required
- Cons
  - Doesn't hide any requests so there's lots of scrolling to do
  - The statuses are sorted alphabetically so unfortunately the 2 classes of failed requests (`status-code:0` and `400+`) are at opposite ends of the sort 😥, so you likely won't be able to see them at the same time.

![image](https://user-images.githubusercontent.com/24983797/176463229-193083a9-426f-413f-8712-78082f80ee90.png)
