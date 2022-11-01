# `[Bookmarklet]` - Enable right-click and selecting text

## Background

Some websites don't want users to be able to `right-click` or `select text` because..... reasons 🤷‍♂️.

They accomplish this by preventing the default behavior of (at least) the `oncontextmenu` and `onselectstart` events listeners respectively. `Event listeners` are just functions that run only when in response to a certain event from the user/browser. One way to prevent the default behavior associated with an event is for its event listener to `return false`.

<details>
    <summary>Guess which country abuses this technique?</summary>
    <h1>🇰🇷 South Korea</h1>
</details>

<details>
    <summary>Click here to find out why this is silly</summary>
For some reasons, those websites are overly protective of their precious content. They're paranoid that someone will steal it. This technique only prevents the most casual users copying and pasting text or images into a search engine, on social media, or on their blog. A slightly more motivated user could easily bypass these "protections" in mere seconds. This is because when a user browses a website, (pretty much) <strong>all</strong> the website's code is sent to the user. Once it's on their computer, they can do anything they want, including copy every bit of it. These measures are silly because they make things more difficult for the most casual and innocent/harmless users while doing nothing to stop a more determined website/content thief.
</details>

## User Story

- When I'm browsing a website on the computer I want to be able to:
  - highlight to select any element I want.
  - right-click anywhere I damn well please.

## Solution

It's possible to remove `event listeners` manually, but a bookmarklet can accomplish this much faster. [Bookmarklets](https://www.freecodecamp.org/news/what-are-bookmarklets/) are magic. They appear to be an ordinary browser bookmark but then clicked, they run a predefined JavaScript snippet.

It's super easy to remove `event listeners` by reassigning them as `null`. This effectively erases the event listeners and the default browser behavior will occur when the event is fired. The code below iterates through every element in the DOM, and the `Document` interface and removes all event listeners that were feebly trying to sabotage basic, reasonable browser interactions.

```js
// The console version:
Array.from(document.all).forEach((el) => {
  el.oncontextmenu = null;
  el.onselectstart = null;
  el.ondragstart = null;
});
document.oncontextmenu = null;
document.onselectstart = null;
document.ondragstart = null;

// The bookmarklet version. Paste the code below as the URL of a bookmark, then click the bookmark to run it.
javascript: (() => {
  Array.from(document.all).forEach((el) => {
    el.oncontextmenu = null;
    el.onselectstart = null;
    el.ondragstart = null;
  });
  document.oncontextmenu = null;
  document.onselectstart = null;
  document.ondragstart = null;
})();
```

## Try it yourself!

### Site A

[Site A](https://www.gukjenews.com/news/articleView.html?idxno=2580291) applies its reasonable interaction sabotage to the `<body>` element.

https://user-images.githubusercontent.com/24983797/199253697-3f252960-4b8a-412a-98fb-8f9c72e5dcef.mov

### Site B

[Site B](https://ideas0419.com/654) applies its paranoid user-hostile event listeners directly to the `Document` interface.

https://user-images.githubusercontent.com/24983797/199255564-9ee48bf2-1f34-4bd8-96bb-3e29a0e5106d.mov

## Further Reading

- StackOverflow [answer](https://stackoverflow.com/a/66295628/10117759) with the basic code snippet.
- MDN Docs pages about [`events`](https://developer.mozilla.org/en-US/docs/Web/Events), [`event handlers`](https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers) in general, [`contextmenu`](https://developer.mozilla.org/en-US/docs/Web/API/Element/contextmenu_event), [`selectstart`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession/selectstart_event), and [`dragstart`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dragstart_event).
