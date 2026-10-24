# Web Scraping API: Real Credit Costs, Plan Limits, and How ScraperAPI Stacks Up Against ZenRows and ScrapingBee

Most people searching for a web scraping API want the same three answers: what it costs, how many pages they actually get for that money, and whether it survives the sites they're targeting. Here's the short version. A web scraping API handles proxies, CAPTCHAs, and JavaScript rendering for you, so you pay per request instead of maintaining your own proxy pool. ScraperAPI is one of the better-known options in this category, with plans from $49/month, a 7-day trial with 5,000 credits and no credit card, and pricing that is unusually transparent about what each target site costs in credits — which matters more than most comparison posts admit.

> **Quick take:** For e-commerce and straightforward targets, ScraperAPI's Business plan ($299/month, 3M credits) works out to roughly 600,000 successful Amazon requests — about 5x the usable volume of ScrapingBee's $249 plan and far more than ZenRows' protected-request quota at the same spend. For heavily defended sites, independent tests put ScraperAPI behind ZenRows, so know your targets first. Most readers should start with the free 5,000-credit trial, then pick between Hobby and Business. 👉 [Check ScraperAPI's plans and start the 7-day free trial](https://www.scraperapi.com/pricing?fp_ref=coupons)

## ScraperAPI's full plan list, with current prices

There are seven plans on the current pricing page: Hobby, Startup, Business, Scaling (flagged as most popular), Professional, Advanced, and Enterprise. All paid plans include the same core feature set — JavaScript rendering, premium residential and mobile IPs, CAPTCHA and anti-bot handling, automatic retries, and a 99.9% uptime guarantee — so the tiers mostly differ in volume, concurrency, and geotargeting depth.

| Plan | Monthly price | Annual (per month) | API credits | Concurrent threads | Get started |
| --- | --- | --- | --- | --- | --- |
| Hobby | $49 | $44.10 | 100,000 | 20 | [ Start Hobby](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | $149 | $134.10 | 1,000,000 | 50 | [ Start Startup](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | $299 | $269.10 | 3,000,000 | 100 | [ Start Business](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | $475 | $427.50 | 5,000,000 | 200 | [ Start Scaling](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | $975 | $877.50 | 10,500,000 | 300 | [ Start Professional](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | [ Start Advanced](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Custom | Custom | 22,000,000+ | 500+ | [ Talk to sales](https://www.scraperapi.com/?fp_ref=coupons) |

Paying annually takes 10% off every tier, so the effective entry price is $44.10/month on Hobby. Two details worth noting before you compare these numbers to other tools: country-level geotargeting only kicks in from Business upward — Hobby and Startup are limited to US and EU IPs — and the analytics dashboard only keeps 30 days of history on the two lower tiers, with unlimited retention from Business up.

## The real cost is in the credit rates, not the plan price

The number that actually determines your cost per page is how many credits each request burns, and this is where most reviews of any web scraping API go vague. ScraperAPI publishes its multipliers openly: a standard page costs 1 credit, Amazon costs 5, Google and Bing (including subdomains) cost 25, LinkedIn costs 30, and sites behind Cloudflare, Datadome, or PerimeterX add 10 credits per request when the protection gets bypassed. You can look up the exact cost of any URL with the Domain Cost Estimator in the dashboard, and cap any single request with a `max_cost` parameter so one expensive page can't drain your balance.

Run the math on the Business plan and the picture gets concrete. At $299/month for 3,000,000 credits:

- **Standard pages:** up to 3,000,000 requests (1 credit each)
- **Amazon-style e-commerce pages:** about 600,000 requests (5 credits each)
- **Google/Bing results:** about 120,000 requests (25 credits each)
- **Protected pages that require bypassing:** about 176,000 requests, assuming the base page is 1 credit plus the 10-credit bypass fee

That spread is why "3 million credits" can mean wildly different things depending on what you scrape. If your project is 90% Amazon product pages, you're effectively buying 600k requests for $299 — about $0.0005 per successful page, which independent testing (Proxyway's measurements, cited in a 2026 comparison) pegs as the lowest per-page cost among the major providers on easy and e-commerce targets. If your project is mostly Google SERPs, divide the credits by 25 and the plan shrinks fast — at that point compare it against a competitor's SERP-specific pricing rather than trusting the headline credit count. 👉 [See the full credit breakdown on the pricing page](https://www.scraperapi.com/pricing?fp_ref=coupons)

One more trap to know about: JavaScript rendering and other premium options consume extra credits on top of the site multiplier, and the exact rate depends on the request parameters you send. The pricing page itself suggests measuring your usable response count with a trial before converting credits into an expected request volume. That advice is worth taking literally — a five-minute test with your real target URLs beats any spreadsheet estimate.

## Limits that don't show up in the pricing table

Three rules live in the FAQ rather than the plan comparison, and each one can change which tier you need.

**Concurrency failures are turned away, not queued.** If you exceed your plan's concurrent request limit, the API returns a 429 and you retry within your limit. The site states there's no extra charge for going over — the request is simply rejected rather than queued. For a batch job this just means throttling your client, but for a time-sensitive crawl it means your plan's thread count is a hard ceiling on throughput: 20 threads on Hobby, 100 on Business, 500 on Advanced.

**Running out of credits pauses scraping by default.** Your requests stop until credits renew, unless you enable one of two opt-ins. Auto-upgrade (available on Hobby through Professional) bumps you to the next plan automatically when credits run out. Pay-as-you-go (available on Scaling and up) keeps scraping past your limit at a fixed per-credit rate, up to a monthly spending cap you set. If you're running a pipeline that can't pause, either turn one of these on or budget headroom — a silent mid-month stall is the most common surprise here.

**Renewal timing matters for annual plans.** Annual plans can renew early for a fresh batch of credits, which effectively lets you front-load usage if your workload is lumpy.

## How ScraperAPI compares to ScrapingBee and ZenRows

These three dominate the comparison searches, and they're genuinely built for different jobs. At roughly the same $299/month spend, here's what each one's mid-tier plan actually delivers:

|  | ScraperAPI (Business) | ScrapingBee (Business) | ZenRows (Business) |
| --- | --- | --- | --- |
| Price | $299/mo | $249.99/mo | $299.99/mo |
| Billing model | API credits | API credits | Per successful request (CPM) |
| Headline volume | 3,000,000 credits | 3,000,000 credits | 3,000,000 basic results |
| E-commerce/protected volume | ~600,000 requests (5 credits each) | ~120,000 premium requests (25 credits each) | ~120,000 protected results |
| Toughest stealth calls | +10 credits when bypassing protection | Up to ~75 credits per call | 25x base rate (~$7.00/1,000) |
| Free tier | 7-day trial, 5,000 credits, no card | 1,000 credits, no card | $1 allowance, no card |
| Dedicated e-commerce endpoints | Yes (Amazon, Google, more) | No | No |
| JS-rendered median speed | ~3.5s (fastest of the three) | ~4.2s | ~4.8s |

The pattern is consistent across independent tests: on easy and e-commerce targets, ScraperAPI delivers the most usable requests per dollar and the fastest median response. Against aggressive anti-bot systems, the ranking flips. A 2026 head-to-head review reported ScraperAPI's measured success rate on protected sites at roughly 62–64% (Proxyway's mixed-target testing), while ZenRows — which advertises 99.93% — came in around 40% in an independent July 2026 benchmark on twelve hard targets. ZenRows still ranked strongest of the three against Cloudflare; ScraperAPI was weakest, sometimes returning 500s or CAPTCHA pages on the hardest challenges. ScrapingBee sits in the middle on most axes.

Vendor-reported success rates deserve the same skepticism in every direction here: ZenRows' 99.93% and ScraperAPI's 99.99% are both manufacturer figures, and both fall well short in independent runs on difficult sites. The practical takeaway is to test your actual URLs on the free trial before committing to any of them. 👉 [Start the free 5,000-credit trial](https://www.scraperapi.com/?fp_ref=coupons)

Review scores tell a similar story with less drama. ScraperAPI holds a 4.6 on Capterra and 4.7 on Trustpilot, against ZenRows' 4.8/3.4 split and ScrapingBee's 4.9 (no Trustpilot data recorded). None of these numbers should override a test on your own targets, but the Trustpilot gap is large enough to note.

## Who a web scraping API like ScraperAPI fits — and who it doesn't

ScraperAPI earns its price on predictable, high-volume targets. If your workload is Amazon, Walmart-style e-commerce, or ordinary content sites, the combination of published credit rates, structured data endpoints (pre-parsed JSON for marketplaces, which none of its two main competitors offer), the no-code DataPipeline scheduler for recurring jobs, and the lowest measured cost per successful page makes it the straightforward pick.

It's the wrong first choice when your targets fight back hard. If you're specifically scraping sites behind aggressive Cloudflare configurations, the independent numbers say ZenRows handles those better, and its per-protected-page pricing stops looking absurd once every page actually succeeds. Paying ScraperAPI's rates for a 60% success rate on hard targets means funding the failed third of your requests — the tool's cost advantage disappears exactly where you need capability instead of volume.

There's also a scale question. Below about 100,000 credits a month, the Hobby plan at $49 (or $44.10 annually) covers roughly 100,000 standard pages or 20,000 Amazon pages with 20 concurrent threads. If you need less than that, the permanent free plan (1,000 credits, 5 concurrent connections) plus the trial may cover a small side project indefinitely, and ScrapingBee's 1,000-credit free tier is an equivalent starting point on the other side. If you need country-level targeting outside the US and EU on a budget, remember that constraint doesn't lift until Business.

## Common questions before signing up

**Is there a free trial?** Yes. Seven days with 5,000 API credits and no credit card required, on top of a permanent free plan that gives 1,000 credits per month with up to 5 concurrent connections. If you need more test credits, support can grant additional ones for evaluation purposes.

**What happens when I run out of credits?** Scraping pauses until renewal by default. Hobby through Professional can opt into auto-upgrade, and Scaling and above can use pay-as-you-go at a fixed per-credit rate with a monthly cap you define. Nothing bills automatically unless you turn those on.

**Does the price change on renewal?** The pricing page shows a single price per billing cycle rather than a separate first-term promotional rate, so the annual discount is the discount — there's no separate renewal markup published. Confirm the current terms on the billing page at checkout, since promotions change.

**Can I scrape Google and LinkedIn?** Yes, at published multipliers: 25 credits per Google or Bing request, 30 per LinkedIn request. Those rates are among the most transparent in the category — some competitors bury equivalent multipliers in stealth-mode pricing that reaches 75 credits per call.

## Choosing between the plans

A few closing decision rules, based on the numbers above:

- **Just getting started or under ~100k pages/month:** Hobby at $49 covers it. Don't pay for credits you'll burn through by year-end anyway — upgrade only when the 429s become routine.
- **E-commerce pipelines at scale:** Business at $299 is the value center. Six hundred thousand Amazon requests per month, country-level geotargeting, unlimited analytics history, and the structured data endpoints that skip your parsing layer entirely.
- **Recurring, schedulable jobs:** Scaling at $475 adds 5M credits and 200 threads, plus pay-as-you-go overflow so a scheduled job never stalls mid-run.
- **Heavily protected targets dominating your workload:** ScraperAPI's cost edge doesn't apply; ZenRows tested stronger against Cloudflare in independent runs. Match the tool to how hard your sites fight back.

Before you commit, do two things: run your five most important URLs through the trial with the parameters you'll actually use, and check their costs in the Domain Cost Estimator. If the numbers hold up, 👉 [pick your plan on ScraperAPI's pricing page](https://www.scraperapi.com/pricing?fp_ref=coupons) and the annual billing option knocks 10% off whatever tier you land on.
