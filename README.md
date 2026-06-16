# GG Homepage Timeline

Month-by-month timeline widget for the Global Gathering homepage. Hovering a month
updates the detail card below the row. Built as a single static `index.html` for
deployment on Vercel and embedding via iframe.

## Tracking

Hover and click events are logged to the Google Apps Script endpoint. All events
write to the **`2026Registration`** sheet/tab:

- `Timeline_<Mon>` — fired once per month box on first hover (e.g. `Timeline_Jun`)
- `Timeline_Jan_CFP` — fired on the "Learn more" button click

## Embedding

```html
<iframe
  id="gg-widget"
  src="https://gg-homepage-timeline.vercel.app"
  width="100%"
  height="100"
  style="border:none;display:block;overflow:hidden;"
  scrolling="no"
></iframe>
<script>
  window.addEventListener("message", function(e) {
    if (e.data && e.data.ggWidgetHeight) {
      document.getElementById("gg-widget").height = e.data.ggWidgetHeight;
    }
  });
</script>
```

The widget posts its height to the parent (`{ ggWidgetHeight }`) on load, resize,
and content changes so the iframe can auto-size.
