---
theme: style.css
highlightTheme: github
revealOptions:
  transition: none
---

<!-- .slide: data-background="./images/froot-loops.jpg", class="filter-dark"-->
<h1 class="title highlighter dark-background">103 Early Hints <br><span class="translucent">at Shopify</span></h1>
<h2 class=" highlighter dark-background">Sia Karamalegos</h2>

---

<!-- .slide: data-background="./images/pancakes.jpg" -->

---

## hi, i'm sia

[sia.codes](https://sia.codes/)

<img src="./images/champagne_sia.jpg" alt="Sia dressed up as a champagne bottle at Mardi Gras" height="450px" class="no-outline">

---

<img src="./images/Early_Hints1.png" alt="A cafe table on the left with two cups of coffee" class="plain">

---

<img src="./images/Early_Hints2.png" alt="The cafe table is now joined by a frying pan on the right" class="plain">

---

<img src="./images/Early_Hints3.png" alt="Below the frying pan, we have a refrigerator" class="plain">

---

<img src="./images/Early_Hints4.png" alt="In between the table and the cooking area is a waiter's station with a pot of coffee and a computer for orders" class="plain">

---

<img src="./images/Early_Hints5.png" alt="Arrow from table to waiter's station and again to the kitchen area, both labeled 'GET pancakes'" class="plain">

---

<img src="./images/Early_Hints6.png" alt="Arrow from pan to fridge saying 'GET milk, eggs', and another arrow returning to the pan with milk and eggs" class="plain">

---

<img src="./images/Early_Hints7.png" alt="Arrows from pan to waiter station and then to table both saying 'OK!'" class="plain">

---

<img src="./images/Early_Hints9.png" alt="Same diagram overlaid in large print with 'WHERE IS THE BUTTER?'" class="plain">

---

<img src="./images/Early_Hints10.png" alt="Arrow pointing to the fridge with a sad face" class="plain">

---

<img src="./images/Early_Hints11.png" alt="Starting image of the table, station, and kitchen, but now there is a tiny pat of butter at the station" class="plain">

---

<img src="./images/Early_Hints12.png" alt="Tiny 'BUTTER' with arrow pointing to tiny pat of butter since its hard to notice" class="plain">

---

<img src="./images/Early_Hints13.png" alt="Initial GET pancakes arrows are now joined by arrows from station to table, the first labeled 'butter?' and the second with the actual tiny plate of butter being delivered" class="plain">

---

<img src="./images/Early_Hints14.png" alt="Add back the arrows to and from the fridge and the OK arrows back to the table" class="plain">

---

<img src="./images/Early_Hints15.png" alt="Add back the pancake delivery arrows" class="plain">

---

<img src="./images/Early_Hints16.png" alt="Smiley face because we now have hot pancakes and butter at the same time" class="plain">

---

## Where's the inefficiency?

---

<img src="./images/Early_Hints_think_time.png" alt="Cafe diagram with kitchen region circled" class="plain">

---

<img src="./images/Early_Hints_latency.png" alt="Similar cafe diagram with distance between kitchen and serving station much more stretched" class="plain">

---

## HTTP2 Server Push

- ✅ Proactively send resources <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ❌ Caching got more complicated <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ❌ Realizing positive results was hard <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->

---

<img src="./images/Early_Hints_push1.png" alt="Cafe diagram but no asking for butter and it comes even though it's already on the table" class="plain">

---

<img src="./images/Early_Hints_push2.png" alt="Expanding that to all the other resources - now the table has too many coffees, forks, and butters" class="plain">

---

## 103 Early Hints

- ✅ Only send hints, and let the browser decide <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ✅ Don't make caching harder <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- 🧐 Results are still early stage <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->

---

<img class="plain" src="./images/Early-hints-diagram-1.png">

---

<img src="./images/Early_Hints15.png" alt="Add back the pancake delivery arrows" class="plain">

---

<img class="plain" src="./images/Early-hints-diagram-step1.png">

---

<img class="plain" src="./images/Early-hints-diagram-step2.png">

---

<img class="plain" src="./images/Early-hints-diagram-step34.png">

---

<img class="plain" src="./images/Early-hints-diagram-step5.png">
---

<img class="plain" src="./images/Early-hints-diagram-1.png">

<small>From <a href="https://blog.cloudflare.com/early-hints-performance/">Early Hints update: How Cloudflare, Google, and Shopify are working together to build a faster Internet for everyone</a></small>

---

## 103 Early Hints: the details

- Sends HTTP status code 103 <!-- .element: class="fragment fade-in-then-semi-out" -->
- Content/hints are in the HTTP header <!-- .element: class="fragment fade-in-then-semi-out" -->

---

<div style="display:flex;justify-content:space-between">
  <img class="plain" src="./images/req-res-no-eh.avif" width="45%">
  <img class="plain fragment fade-in" src="./images/req-res-eh.avif" width="45%">
</div>

<small>From <a href="https://developer.chrome.com/blog/early-hints/">Faster page loads using server think-time with Early Hints</a></small>

---

> Cloudflare sits within 50 milliseconds of 95% of the Internet-connected population globally.

---

## Syntax

```
HTTP/1.1 103 Early Hints
Link: <https://example.com>; rel="preconnect"
Link: </style.css>; rel=preload; as=style
Link: </script.js>; rel=preload; as=script
```

Note: Goal today is to explain the concepts. Details on how to set this up are better served with docs and tutorials from Cloudflare and Fastly. If you're considering rolling your own, talk to some of those folks about the common pitfalls.

---

## Resource Hints Review

Early hints can be sent for <br/>
`preconnect` and `preload`.

---

```html
<!-- Preconnect -->
<link rel="preconnect" href="https://cdn.shopify.com">
```

Note: All modern browsers except Firefox

---

```html
<!-- Preload -->
<link
  href="//cdn.shopify.com/.../ShopifySans-Regular.woff2"
  rel="preload" as="font" type="font/woff2" crossorigin="true">
```

Note: All modern browsers

---

<!-- .slide: data-background="./images/fruit_juice.jpg", class="filter-dark"-->
# When to consider Early Hints <!-- .element: class="dark-background highlighter"-->

---

> When a buyer visits a Shopify website, if that **first page experience** is 10% faster, on average there is a 7% increase in conversion.

---

## Should I consider Early Hints?

- ✅ First impressions are important for conversion (use on top landing pages) <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ✅ Server has to do work before sending the HTML <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ❌ Server can immediately send the HTML <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ✅ Server is farther from user than edge/CDN server <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ✅ Traffic is high enough that the edge/CDN server will likely have Early Hints cached <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ✅ Use on resources that do not change often <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->

---

<!-- .slide: data-background="./images/teamwork.jpg", class="filter-dark"-->
# Teamwork <!-- .element: class="dark-background highlighter"-->

---

<img class="plain" src="./images/team_EH.png">

Note: Colin Bendell at Shopify, Alex Krivit at Cloudflare and Kenji Baheeux + Kenichi Ishibashi at Chrome

---

<img class="plain" src="./images/team_EH_puzzle.png">

Note: Colin Bendell at Shopify, Alex Krivit at Cloudflare and Kenji Baheeux at Chrome

---

<!-- .slide: data-background="./images/oatmeal-fruit.jpg", class="filter-dark"-->
# Results <!-- .element: class="dark-background highlighter"-->

---

## Preconnect

```
HTTP/1.1 103 Early Hints
Link: <https://cdn.shopify.com>; rel="preconnect"
Link: <https://cdn.shopify.com>; crossorigin; rel="preconnect"
```

---

## Largest Contentful Paint

<img alt="Box plots showing different OS's all with improved LCP performance when Early Hints was used to preconnect to our CDN" class="plain" src="./images/preconnect_LCP.png" width="55%">

Note: BFCM 2021 test. LCP improved across all regions and operating systems on Chrome browsers when an early hint was used to preconnect to our CDN domain. ~500ms improvement in median LCP

---

## Largest Contentful Paint

<img alt="Box plots showing different OS's all with improved LCP performance when Early Hints was used to preconnect to our CDN" class="plain" src="./images/preconnect_LCP_explained.png" width="85%">

---

<img alt="" class="plain" src="./images/filmstrip_preconnect.png" >

---

# 🤔

Note: take a step back and realize we wouldn't need this if we didn't have a separate CDN domain - so we're using EH to accommodate for a less-than-ideal situation due to legacy architecture. Under HTTP1, domain sharding was a better way to serve assets faster due to the limited number of concurrent connections ~6. Can't instantly switch each time a new HTTP version comes out.

---

## Preload

```
HTTP/1.1 103 Early Hints
Link: <font1.woff2>; rel=preload; as=font; crossorigin...
Link: <font3.woff2>; rel=preload; as=font; crossorigin...
Link: <script.js>; rel=preload; as=script; type=text/javascript
Link: <main.js>; rel=preload; as=script; type=text/javascript
Link: <theme.css>; rel=preload; as=style;
```

---

## Shopify themes use Liquid for templating

- HTML templating language
- Similar to Nunjucks, HAML, Handlebars, Pug, etc.
- Can access data directly in Liquid for SSR
- See layout (wrapper) [example](https://github.com/Shopify-Web-Perf-Team-Internal/perf-shopify-theme/blob/main/layout/theme.liquid) for context

---

## Early Hints via Liquid

```liquid
{{ 'font.woff2'
  | asset_url
  | preload_tag:
      as: 'font',
      type: 'font/woff2',
      crossorigin: true
}}

{{ 'script.js' | asset_url | preload_tag: as: 'script' }}

{{ 'style.css' | asset_url | stylesheet_tag: preload: true }}
```

Note: Liquid: piping into next filter, additional params after filter. Stores can only access EH using Liquid, and only to files on our CDN. Will create both preload tags and EH's.

---

```liquid
{{
  product.featured_image
    | image_url: width: 2 000
    | image_tag:
        preload: true,
        widths: 50, 80, 90, 100, 120, 160, 200, 300, 400, 500,
          600, 700, 800, 1000, 1200, 1500, 1800, 2000
}}
```

Note: Also an example of accessing data object directly in Liquid. Can anyone imagine what might go wrong here???

---

```html
<img srcset="//cdn.shopify.com/s/files/1/0657/6730/9530/articles/
fahrul-azmi-lNpkIWnFzTo-unsplash.jpg?v=1666177560&amp;width=50
50w, //cdn.shopify.com/s/files/1/0657/6730/9530/articles/fahrul-
azmi-lNpkIWnFzTo-unsplash.jpg?v=1666177560&amp;width=100 100w,
//cdn.shopify.com/s/files/1/0657/6730/9530/articles/fahrul-azmi-
lNpkIWnFzTo-unsplash.jpg?v=1666177560&amp;width=200 200w, //cdn.
shopify.com/s/files/1/0657/6730/9530/articles/fahrul-azmi-lNpkIWn
FzTo-unsplash.jpg?v=1666177560&amp;width=300 300w, //cdn.shopify.
com/s/files/1/0657/6730/9530/articles/fahrul-azmi-lNpkIWnFzTo-
unsplash.jpg?v=1666177560&amp;width=350 350w, //cdn.shopify.com/s/
files/1/0657/6730/9530/articles/fahrul-azmi-lNpkIWnFzTo-unsplash.
jpg?v=1666177560&amp;width=500 500w, //cdn.shopify.com/s/files/1/
0657/6730/9530/articles/fahrul-azmi-lNpkIWnFzTo-unsplash.jpg?v=
1666177560&amp;width=750 750w, //cdn.shopify.com/s/files/1/0657/
6730/9530/articles/fahrul-azmi-lNpkIWnFzTo-unsplash.jpg?v=166617
7560&amp;width=1100 1100w, //cdn.shopify.com/s/files/1/0657/6730/
9530/articles/fahrul-azmi-lNpkIWnFzTo-unsplash.jpg?v=1666177560&amp;
width=1500 1500w, //cdn.shopify.com/s/files/1/0657/6730/9530/
articles/fahrul-azmi-lNpkIWnFzTo-unsplash.jpg?v=1666177560&amp;width
=2200 2200w, //cdn.shopify.com/s/files/1/0657/6730/9530/articles/
fahrul-azmi-lNpkIWnFzTo-unsplash.jpg?v=1666177560 2981w" sizes=
"(min-width: 1200px) 1100px, (min-width: 750px) calc(100vw - 10rem),
100vw" src="//cdn.shopify.com/s/files/1/0657/6730/9530/articles/
fahrul-azmi-lNpkIWnFzTo-unsplash.jpg?v=1666177560&amp;width=1100"
width="2981" height="1677" alt="Introduction to preconnect and
preload resource hints">
```

Note: Image srcsets as preload early hints are not yet working - still working on implementation details.

---

<img alt="Github issue title: [Critical] Preloading can cause stores to not load at all #1995" class="plain" src="./images/critical_issue_preload.png" >

---

<!-- .slide: data-background="./images/shame.jpg" -->

---

⚠️ Beware of making your headers too large!

Note: Also consider fetchpriority instead. Where were we? Oh yeah...

---

<!-- .slide: data-background="./images/toast-egg.jpg", class="filter-dark"-->
# ...Results <!-- .element: class="dark-background highlighter"-->

---

<!-- .slide: data-background="./images/rum.jpg", class="filter-dark" -->
# RUM is hard <!-- .element: class="dark-background highlighter"-->

Note: Our preconnect tests were a true A/B test. But for preload, in true engineering style, we might have over optimized the laziness factor and tried to do a before/after test.

---

<img alt="HTTP Archive Chrome User Experience Report charting TTFB over time for Shopify showing TTFB getting worse in recent months" class="plain" src="./images/crux_shopify_ttfb.png" >

Note: So what we actually measured was a TTFB degradation unrelated to EH. Which leads me to the next part of the presentation...

---

## How I blew through my WebPageTest Pro budget in 2 days

---

## 1.2% improvement in p50 LCP

- 16 different merchant websites
- Index, collection, and product pages
- High variation within each 9 runs
- Ranged from -15% to 21%

Note:  Etsy recently conducted an experiment using early hints and measured a 2.5% improvement in LCP for landing pages, based on preconnects and font preloads. They are evaluating other ways of implementing to early hints to maximize the performance gains. Wix tested preconnects and haven't found significant improvement with it yet.

---

## Preload is still a footgun.

---

## Without Early Hints

<img alt="" class="plain" src="./images/waterfall_degradation_no_EH.png" >

---

## With Early Hints 🦶🏻🔫

<img alt="" class="plain" src="./images/waterfall_degradation_EH.png" >

---

<img alt="" class="plain" src="./images/filmstrip_preload_good.png" >

---

<!-- .slide: data-background="./images/cappuccino.jpg", class="filter-dark" -->
# Conclusion <!-- .element: class="dark-background highlighter"-->

---

## Conclusion

- ✅ Early Hints is more promising than HTTP2 Server Push <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ✅ Preconnect showed promising results <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ⚠️ Preload is trickier and needs case-by-case testing <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- ✅ Teamwork makes the dream work <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->
- 🧈 Butter hints are better than no butter hints <!-- .element: class="fragment fade-in-then-semi-out no-bullet" -->

---

<!-- .slide: data-background="./images/gudetama.png", class="filter-dark" -->
<div class="highlighter dark-background" style="padding: 40px 0">
  <h1 class="title dark-background">Thanks!</h1>
  <h2 class="dark-background">Slides, resources, and more at <a href="https://sia.codes">sia.codes</a></h2>
</div>

---

## Photo Credits

<small>
- Pancake image: Photo by <a href="https://unsplash.com/@amysaysamy?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Amy Flak</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Water balloons image: Photo by <a href="https://unsplash.com/@tcooper86?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Tim Cooper</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Froot Loops image: Photo by <a href="https://unsplash.com/@etiennegirardet?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Etienne Girardet</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Oatmeal with fruit image: Photo by <a href="https://unsplash.com/@brookelark?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Brooke Lark</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Toast and egg image: Photo by <a href="https://unsplash.com/@shootdelicious?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Eiliv Aceron</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Rum image: Photo by <a href="https://unsplash.com/@annoand?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Anders Nord</a> on <a href="https://unsplash.com/s/photos/rum?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Little girl with hands over eyes: Photo by <a href="https://unsplash.com/@caleb_woods?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Caleb Woods</a> on <a href="https://unsplash.com/s/photos/shame?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Teamwork image: Photo by <a href="https://unsplash.com/@hannahbusing?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Hannah Busing</a> on <a href="https://unsplash.com/s/photos/team-work?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Cappuccino: Photo by <a href="https://unsplash.com/@jeztimms?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Jez Timms</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Fruit and juice: Photo by <a href="https://unsplash.com/@brookelark?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Brooke Lark</a> on <a href="https://unsplash.com/s/photos/breakfast?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Water gun fight is licensed through Unsplash+
</small>

---

## Chrome CLI to disable Early Hints on WebPageTest

```
--disable-features=EarlyHintsPreloadForNavigation
```
