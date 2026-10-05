# data impulse: what $1/GB pay-as-you-go proxies really cost, which plan to pick, and how to start on $5

Most people who type "data impulse" into a search bar already saw the number somewhere first. A comparison table, a scraping tutorial, a forum thread with someone claiming residential proxies at a dollar a gigabyte. So the actual question behind the search is rarely "what is this company" — it's "is that price real, and what does the bill look like once the crawler is running at 3 a.m.?"

Below is the pricing model, the full plan list, the places where costs quietly change, and the setup path, so you can decide before spending anything.

## The 30-second version

DataImpulse sells proxy traffic by the gigabyte rather than renting it by the month. Residential sits at **$1/GB**, datacenter at **$0.50/GB**, mobile at **$2/GB**, and premium residential at **$5/GB**. There is no subscription. The minimum purchase is $5. Traffic you buy does not expire. The residential pool is advertised at 90M+ IPs across 195 countries, and the company says it sources those IPs through its own opt-in app instead of reselling other networks' pools — which is the main reason it can price at $1/GB while Bright Data and Oxylabs list around $6–8/GB for standard residential.

That first-party claim matters more than it sounds. When a provider resells IPs from an aggregator, those addresses carry the abuse history of every previous buyer across every reseller. A pool that only its own users touch tends to arrive at a protected target cleaner. It is also the one claim on this list you can't verify from the pricing page, so treat it as the vendor's position rather than a measured fact.

## Every plan currently on the price list

Four proxy types, each with the same tier naming, which makes reading the table easier than most providers' pricing pages. Prices are in USD, pay-as-you-go, no recurring charge.

| Proxy type & plan | Traffic | Price | Effective rate | Billing | Get it |
| --- | --- | --- | --- | --- | --- |
| Residential — Intro | 5 GB | $5 | $1.00/GB | One-time, non-expiring | [Grab the $5 residential test pack](https://bit.ly/dataimPulse) |
| Residential — Basic | 50 GB | $50 | $1.00/GB | One-time, non-expiring | [Buy the 50 GB residential plan](https://bit.ly/dataimPulse) |
| Residential — Advanced | 1 TB | $800 | $0.80/GB | One-time, non-expiring | [Get the 1 TB residential tier](https://bit.ly/dataimPulse) |
| Residential — Custom+ | 5 TB and up | Quote-based (reported entry around $4,000) | Negotiated | One-time, non-expiring | [Request the enterprise residential quote](https://bit.ly/dataimPulse) |
| Datacenter — Intro | 10 GB | $5 | $0.50/GB | One-time, non-expiring | [Start with 10 GB of datacenter traffic](https://bit.ly/dataimPulse) |
| Datacenter — Basic | 100 GB | $50 | $0.50/GB | One-time, non-expiring | [Buy the 100 GB datacenter plan](https://bit.ly/dataimPulse) |
| Datacenter — Advanced | 1 TB | $450 | $0.45/GB | One-time, non-expiring | [Get the 1 TB datacenter tier](https://bit.ly/dataimPulse) |
| Datacenter — Custom+ | 5 TB and up | Quote-based (reported entry around $2,250) | Negotiated | One-time, non-expiring | [Request the datacenter enterprise quote](https://bit.ly/dataimPulse) |
| Mobile — Intro | 2.5 GB | $5 | $2.00/GB | One-time, non-expiring | [Try 2.5 GB of mobile proxies](https://bit.ly/dataimPulse) |
| Mobile — Basic | 25 GB | $50 | $2.00/GB | One-time, non-expiring | [Buy the 25 GB mobile plan](https://bit.ly/dataimPulse) |
| Mobile — Advanced | 1 TB | $1,600 | $1.60/GB | One-time, non-expiring | [Get the 1 TB mobile tier](https://bit.ly/dataimPulse) |
| Mobile — Custom+ | 5 TB and up | Quote-based (reported entry around $8,000) | Negotiated | One-time, non-expiring | [Request the mobile enterprise quote](https://bit.ly/dataimPulse) |
| Premium Residential — Intro | 1 GB | $5 | $5.00/GB | One-time, non-expiring | [Test the premium residential pool](https://bit.ly/dataimPulse) |
| Premium Residential — Basic | 10 GB | $50 | $5.00/GB | One-time, non-expiring | [Buy 10 GB of premium residential](https://bit.ly/dataimPulse) |
| Premium Residential — Custom+ | 5 TB and up | Quote-based (reported entry around $20,000) | Negotiated | One-time, non-expiring | [Request the premium residential quote](https://bit.ly/dataimPulse) |

Two things are worth pulling out of that grid. The 20% volume discount on residential and mobile only kicks in at the 1 TB tier, so if you're buying 100 GB of residential you pay the same $1/GB as someone buying 5 GB. And the enterprise rows are quote-based — the starting figures above come from third-party breakdowns, not a published rate card, so confirm them with sales before you put them in a budget.

## What the $5 actually gets you

The "$5 trial" is the phrase most people arrive with, and it's worth being precise, because it's a paid starter pack, not free bandwidth. First-time customers can buy 5 GB of residential for $5 (or 10 GB datacenter, 2.5 GB mobile, 1 GB premium residential). One per account. If you later buy a *different* proxy type, the $5 entry price opens up again on that new type.

Here's the part that catches people: once you're past that first purchase, the minimum top-up or additional same-type plan is $50. Adding a second residential plan is not another $5 experiment.

Traffic doesn't expire, so there's no clock pressure on that first 5 GB — you can run a real test against your actual targets and let the balance sit for weeks before deciding. That's a meaningful difference from providers where a monthly allocation burns off whether you use it or not. If your crawl calendar is lumpy (heavy during a reporting week, idle for a fortnight after), the pay-as-you-go model is structurally cheaper than a subscription you only half-use.

## Where the real cost shows up

The $1/GB headline is the base rate for country-level routing. Several things move it:

**Advanced targeting is billed at double on residential.** Country selection is free. State, city, ZIP code and specific ASN selection route your traffic at 2× the standard per-GB rate, which turns $1/GB into $2/GB for that portion. Datacenter proxies list state/city/ZIP/ASN as included features instead — confirm with support before you budget either way, because this is the single biggest variable in a residential estimate.

**Concurrency has a ceiling.** Accounts are capped at 2,000 active connections; past that, requests fail with `407 THREADS_EXHAUSTED` until you reduce parallelism. For a wide multi-threaded crawler that's an architectural detail worth knowing on day one.

**There's no managed scraping layer.** No unblocker API, no SERP endpoint, no dataset product. You get raw proxy connections and you write the retries, parsers and CAPTCHA handling yourself. Teams that want a black-box scraper should look elsewhere; teams with their own Python stack will find the missing layer is exactly the part they didn't want to pay for.

> Practical rule of thumb: route each job to the cheapest tier that still succeeds. Datacenter ($0.50/GB) for unprotected pages and your own infrastructure, residential ($1/GB) for e-commerce, SERPs and social, mobile ($2/GB) only when a target genuinely rejects residential. Paying residential rates for public pages is the most common way a cheap proxy bill stops being cheap.

## Getting from signup to a working request

The flow is standard account-then-order, with a couple of specifics worth knowing in advance.

1. Register with email, Google or LinkedIn. You pick a contact channel (email, Telegram, WhatsApp, Viber, Skype) and a use case from a dropdown, then verify the email link.
2. Log in. You land on the Plans tab, which prompts you to buy a paid trial since you have no plans yet.
3. Click **+ Create new order**, choose the proxy type, hit Buy Now, pick your plan label and GB quantity, and continue. The price recalculates live as you change the GB figure.
4. Pay by card (Stripe, Visa/Mastercard) or crypto (Cryptomus — USDT, Bitcoin, Ethereum, Litecoin). Card processing is instant; nothing waits on a sales call or account approval.
5. Grab credentials from the **Proxy Access** section of your plan tab: login, password, host and port. Next to it, **Usage** shows remaining traffic and the top-up button.
6. Configure: rotation interval, ASN exclusions, anonymous filtering, hostname format, proxy type and protocol. Save the configuration. Country geo-targeting is selectable here without a surcharge.

For raw connection details, the rotating endpoints are port **823** for HTTP/HTTPS and **824** for SOCKS5, through `gw.dataimpulse.com`. Rotating gives you a new IP per request; sticky sessions hold one IP on a port in the 10000–20000 range, settable from 1 to 120 minutes with 30 minutes as the default. Sticky is what you want for a login flow or a paginated sequence where the session has to stay coherent.

Authentication is either username/password or an IP whitelist — the whitelist option exists so you can fire requests without embedding credentials in every call. Country, city and session parameters can also be pushed into the proxy username, which is how most anti-detect browser and Playwright/Puppeteer setups wire it up. Client libraries read these the same way any HTTP proxy works, so `httpx`, Selenium and Scrapy all take it without a special SDK.

There's also a usage dashboard that breaks spend, traffic and request counts down by plan, with a detail table granular enough to show per-minute request volumes. Useful for debugging a spike; noisy if you try to use it as a daily monitoring view.

## Which tier fits which job

| Your workload | Sensible tier | Why |
| --- | --- | --- |
| Bulk parsing of public pages, internal APIs | Datacenter, $0.50/GB | IP reputation doesn't matter when nothing is checking it |
| SEO rank tracking, SERP checks | Residential, $1/GB | Search engines flag datacenter ranges quickly |
| E-commerce and marketplace scraping | Residential, $1/GB | Protected targets block datacenter subnets fast |
| Account management, long logged-in sessions | Residential with sticky sessions | Rotating IPs break session continuity |
| Cross-region ad verification | Residential with country targeting | You need consumer IPs in the market you're checking |
| Mobile app APIs, hardest anti-bot targets | Mobile, $2/GB | Real 4G/5G carrier IPs clear checks residential can't |
| High-trust targets where standard residential fails | Premium residential, $5/GB | Smaller filtered pool, dedicated account manager |

## What independent testing and reviews actually show

Worth separating measurable claims from marketing here.

Shifter ran the pool through a live comparison and measured **172,893 active IPs across five countries**, against 306,410 on the deepest network in their test — roughly 60% of the top pool. Median response times landed between **430 and 501 ms**, which put DataImpulse among the faster networks measured, including several charging three times as much. They also flagged France as the thinnest market in their sample (63 operators versus 148 on the deepest network), and disclosed a commercial interest in the comparison. Take the numbers, discount the framing.

Proxyway's April 2025 benchmark work, cited by reviewers covering the mobile product, confirmed the regular residential pool had grown substantially, with over 300,000 unique US addresses observed. DataImpulse publishes a **99.51% success rate** on its own site, which is a vendor figure rather than an audited one, and cites a **4.8/5 G2 rating**. HostAdvice's review tested live chat and got a human reply in about seven minutes, which lines up with the 24/7 human support claim rather than a bot-first queue.

Third-party reviews also mention a **7-day money-back guarantee on first purchases, excluding crypto payments**. If you're weighing the $5 test, that's the term to verify with support before you pay, since the guarantee comes from review coverage rather than a line on the pricing page.

## Where this is the wrong tool

- You want a managed scraping API with unblocking and parsing handled for you. Not here.
- You need the absolute deepest pool for the most defended targets at scale. Bright Data advertises 400M+ residential IPs; DataImpulse's 90M+ is mid-tier, and IP overlap becomes a real problem on very large crawls.
- You want a free tier to poke at forever. The entry point is $5 paid.
- Your budget assumes city-level targeting at base rates. On residential, that's 2×.
- You're a one-off, 2 GB project. You'll pay $1/GB and the $50 minimum on later top-ups won't matter to you at all — which is fine, but don't expect a volume break you won't reach.

## FAQ

**Is DataImpulse actually $1/GB, or is that a promotional rate?**
It's the standing pay-as-you-go residential rate for country-level routing, not a limited-time deal. The genuine discounts are volume-based: $0.80/GB at the 1 TB residential tier and $1.60/GB at 1 TB mobile.

**Do I lose unused traffic?**
No. Purchased GB stays in the account until consumed. DataImpulse states this explicitly and third-party reviews consistently repeat it, including Shifter's breakdown noting unused credits roll over.

**Can I mix proxy types on one account?**
Yes. Datacenter, residential, mobile and premium residential sit under the same pay-as-you-go account, so you can route one job through datacenter and another through residential without a second vendor.

**What happens when traffic runs out mid-crawl?**
Requests return `407 TRAFFIC_EXHAUSTED`. Top up from the Usage section, or switch on auto top-up with your own threshold so the balance refills before it hits zero.

**Which plan should a first-time buyer pick?**
The $5 residential test pack in most cases — 5 GB is enough to benchmark success rates against your real targets, and it doesn't expire while you evaluate. Drop to the $5 datacenter pack instead if everything you're scraping is unprotected; that's 10 GB for the same money.

If you'd rather skip the explainer and just look at the current numbers yourself, 👉 [open the DataImpulse pricing and signup page](https://bit.ly/dataimPulse) and compare it against your own traffic estimate. Five dollars and a real crawl against your own targets will tell you more than any comparison table, including this one.
