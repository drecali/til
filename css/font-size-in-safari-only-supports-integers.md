# `font-size` in Safari only supports integers

Safari is evil. Unlike Chrome, it only allows `integer` pixel sizes for font-size and likely other CSS properties. In my case, this was an issue when a design used `font-size: 12.5px`. It worked in Chrome, but Safari interpreted it as `font-size: 12px`. (I am aware that relative units like `em` or `rem` are better for accessibility and mobile-friendliness. In this case, the design called for a very specific pixel dimension.)

Here's Safari's `font-size` changing abruptly:

https://user-images.githubusercontent.com/24983797/173212308-7c142def-140e-498b-8e69-6bd2363ec4e6.mov

Here's Chrome's `font-size` changing gradually:

https://user-images.githubusercontent.com/24983797/173212319-b7c9841d-94f6-4dbe-80d6-8faeb0968821.mov

You can check for yourself with these interactive demos:

- [https://jsfiddle.net/fo4egv7n/](https://jsfiddle.net/fo4egv7n/)
- [https://jsfiddle.net/64hwk8bt/1/](http://jsfiddle.net/64hwk8bt/1/)
- On StackOverflow [this answer](https://stackoverflow.com/a/57042369/10117759) has a code snippet you can try yourself. The question was edited to include a screenshot of the `font-size` [train wreck](https://stackoverflow.com/questions/56998778/can-i-have-12-5px-font-size) on Safari.

## History

Unfortunately, this seems to be a known issue on Safari and was reported as early as 2010. It also doesn't seem addressed in the MDN Docs for [font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size).

- [https://bugs.webkit.org/show_bug.cgi?id=46987](https://bugs.webkit.org/show_bug.cgi?id=46987)
- [https://bugs.webkit.org/show_bug.cgi?id=228545](https://bugs.webkit.org/show_bug.cgi?id=228545)
- Here are some quotes from a WebKit developer in those issues. I'm not sure what those mean or the reasoning behind this `font-size` limitation that goes against other major browsers.
  > `We purposely round the font sizes (to integer values) so that we get a higher hit rate in our various caches.` > `We round text sizes to integer values to increase cache hit rates.`
  - I think [this line](https://trac.webkit.org/browser/webkit/trunk/Source/WebCore/platform/graphics/FontDescription.h#L48) of Safari's source code is responsible the strange behavior.
    ```c
    (unsigned computedPixelSize() const { return unsigned(m_computedSize + 0.5f); })
    ```

## Attempted solutions

- `text-rendering: geometricPrecision;` seems to only work for SVG text. See this [interactive demo](https://jsfiddle.net/7wozo5eL/10/) and [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/text-rendering).
- `-webkit-font-smoothing: antialiased;` did not work.
  > Non-standard: This feature is non-standard and is not on a standards track. Do not use it on production sites facing the Web: it will not work for every user. There may also be large incompatibilities between implementations and the behavior may change in the future. ([MDN Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/font-smooth))

## Additional reading about sub-pixel rendering

Some of these may be out of date, but they were interesting to read anyway.

- 2014 article: [Browser Rounding and Fractional Pixels](https://cruft.io/posts/percentage-calculations-in-ie/) with links to more resources.
  - [Pixel/Percentage Rounding Test Page](https://cruft.io/static/rounding/)
- [Sub-Pixel Problems in CSS](https://johnresig.com/blog/sub-pixel-problems-in-css/)
- [Browsers and Fractional Pixels](http://www.simonbattersby.com/blog/browsers-and-fractional-pixels/)
- [Sub-pixel Rounding](http://tylertate.com/blog/frontend/2012/01/05/subpixel-rounding.html)
- [font-size rounding](https://meyerweb.com/eric/css/tests/font-size-rounding.html)
- [Rounding-off](https://meyerweb.com/eric/thoughts/2010/02/10/rounding-off/)
- [Pixel-perfect rendering with devicePixelContentBox](https://web.dev/device-pixel-content-box/)
- Smashing Magazine's [Getting the Hang of Web Typography](https://books.google.co.kr/books?id=eeMHTSi0DHsC&pg=PA9&lpg=PA9&dq=safari+sub-pixel+rendering&source=bl&ots=bTL3YMUXFw&sig=ACfU3U0G_hQAlLejDiNfChr_a4OFX4W4gg&hl=en&sa=X&ved=2ahUKEwjJzv6VwY74AhXqxosBHTo1Ch4Q6AF6BAghEAM#v=onepage&q=safari%20sub-pixel%20rendering&f=false)
- StackOverflow Q&A: [Safari is not respecting decimals in CSS filter: blur()](https://stackoverflow.com/questions/68899373/safari-is-not-respecting-decimals-in-css-filter-blur)
- [Do websites need to look exactly the same in every browser?](http://dowebsitesneedtolookexactlythesameineverybrowser.com/)
- Hacker news discussion titled [Let's fix `font-size`](https://news.ycombinator.com/item?id=26633148).
