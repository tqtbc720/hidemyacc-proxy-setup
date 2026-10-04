# HidemyAcc proxy: How to Set Up a Residential Proxy for Every Profile and Which Plan Actually Fits

You install HidemyAcc, spin up five profiles, and then hit the Proxy tab. That's usually where things get messy — not because the setup is complicated, but because a lot of people assume the browser handles the IP address for them.

It doesn't. HidemyAcc changes what your browser looks like. Your IP address stays exactly where it was, which means every profile you create is still walking out the door from the same place.

## Why HidemyAcc Alone Doesn't Change Your IP

An antidetect browser spoofs fingerprint parameters: canvas hashes, WebGL image data, WebGL metadata tied to your graphics card, audio context, client rects, font measurements, screen resolution. HidemyAcc's own documentation is fairly explicit that it fabricates this hardware-level data so a site reads the profile as a genuine device rather than a virtual machine.

None of that touches your network layer.

Leave the Proxy tab on *Without Proxy* and the profile runs on the same IP address as your real machine. Two accounts, one IP, same subnet — that's the pattern account-linking systems look for first, no matter how clean the fingerprints are.

The reverse is also worth saying plainly: a residential proxy with a leaked WebRTC address, a mismatched timezone, or a location that contradicts the IP is just as detectable. The two halves have to agree.

## What HidemyAcc Accepts in the Proxy Tab

Hit **+ New Profile**, then open the **Proxy** tab. You get four choices:

- **Free Proxy** — HidemyAcc's own pool, roughly 10,000 proxies, available from the Base package upward. Choose a country and the system assigns one at random.
- **Your Proxy** — your own proxy, entered manually.
- **Without Proxy** — real IP, as discussed.
- **Proxy Manager** — pull from proxies you've already stored, instead of retyping credentials.

Pick *Your Proxy* and you'll choose a connection type. HidemyAcc supports HTTP, Socks4, Socks5, plus presets for Tinsoftproxy and TMproxy. SSH shows up in the quick-profile URI formats, which is a small hint that the underlying engine supports more than the dropdown makes obvious.

Credentials go in as one string:


ip:port:username:password


Paste it, hit **Import**, and the fields fill themselves. Then click **Check Proxy**. If the connection works, HidemyAcc prints the proxy's IP, country, region, city and timezone underneath. If it doesn't, you get "Can't connect to proxy server" and nothing else — no diagnostic, no error code. That single line is the source of most support threads about this browser.

The **Proxy Manager** is the part worth setting up early if you're running more than a handful of profiles. You can bulk-add proxies, apply tags, attach expiry dates, leave notes, and run a bulk **Check Proxy** across the whole list. There's also a bulk *Add Proxy* action that pushes proxies onto existing profiles without opening each one. Export gives you a CSV with profile name, proxy type, proxy, location, tag, expiry and notes.

One limitation to know before you plan around it: bulk export, run, delete and copy-ID operations are part of the Business package, and export covers cookies, history, bookmarks and local storage. If your workflow depends on moving profile data around, that matters more than the proxy list.

## Step-by-Step: Wiring a Residential Proxy into a Profile

For a concrete example, 9Proxy publishes a HidemyAcc integration guide, and the steps line up with HidemyAcc's own documentation. Here's the sequence, including the part most walkthroughs skip.

1. **Get the browser and account.** Download the HidemyAcc app, then register inside the app. 9Proxy's guide notes that signing up through a web browser won't work — registration has to happen in the application. HidemyAcc offers a 7-day trial, which is enough to test a proxy setup before paying for anything.
2. **Create the proxy on the provider side.** In your 9Proxy dashboard, create a sub-account, assign traffic to it, and generate a session. You'll pick your targeting (country, and depending on your plan, state, city, ZIP or ISP) and choose sticky or rotating.
3. **Open the profile settings.** Click **Create new profile**, then the **Proxy** tab, then select **Your Proxy**.
4. **Choose a protocol.** SOCKS5 is the common recommendation because it handles more traffic types and doesn't rewrite requests the way HTTP proxies do. HidemyAcc accepts HTTP, HTTPS and SOCKS5 here.
5. **Fill in host, port, username and password.** With 9Proxy's GB-based residential plans, the host and port come straight from the dashboard. The username isn't just a login — it carries your targeting and session settings in a structured string:


<subaccount>-country-<country_code>-st-<state_code>-city-<city_code>-isp-<isp_code>-ssid-<session_id>-sst-<session_time>


A real-shaped example looks like `useruser123-country-US-ssid-rhdN1907ma`. The password is your sub-account password.

If you're on an IP-based plan instead, the workflow differs: 9Proxy's guide has you port-forward the proxy locally through the desktop client first, then enter your **local IP and port** in HidemyAcc rather than a remote host. Skipping the port-forward step is the usual reason an IP-based plan appears to do nothing.

6. **Check the connection.** Click **Check Proxy** and confirm the flag and geo-data appear.
7. **Save and launch.** Click **Create** (or **Update** on an existing profile), then **Run**. HidemyAcc loads an IP checker page automatically, so you can see the exit IP and fingerprint in the same window before you log into anything.

If you're starting from zero, you'll need a provider account before step 2: 👉 [Sign up for 9Proxy and generate your first residential proxy](https://bit.ly/9-Proxy).

## Static vs Rotating: What Actually Changes Inside HidemyAcc

This is the part that decides whether your setup holds up, and it's buried in the browser's tabs rather than the provider's dashboard.

**Timezone and Geolocation** adjust automatically from the proxy. If you see a mismatch on an IP checker site, HidemyAcc lets you set the timezone manually. Fix it — a profile claiming to be in Warsaw while reporting your actual local time is a cheap signal to catch.

**WebRTC** is where rotating proxies create problems. HidemyAcc exposes an IP through WebRTC on each profile run, and the browser detects that IP once, at launch. With a **static** proxy you can leave the setting on Altered, and sites will read the proxy's IP as yours. With a **rotating** proxy, the proxy address changes constantly while the WebRTC-detected address stays frozen from the first request. HidemyAcc's documented recommendation is to set WebRTC to **Disable** when you're rotating. Leaving it on Real exposes your home IP, which defeats the entire point of the exercise.

Practical rule: sticky residential sessions for accounts you need to keep logged in, rotating for tasks where each request should look like a different person.

## Why the Free Proxy Pool Isn't a Long-Term Answer

The Base package includes access to about 10,000 free proxies. For confirming that your profile configuration works, that's genuinely useful and costs nothing.

But HidemyAcc's own documentation describes these as shared datacenter proxies, used across accounts, and recommends using your own proxy for better security. That description is the whole problem in one sentence: datacenter ranges are flagged more aggressively than residential IPs, and shared means other people's traffic history is attached to the address you're using.

For throwaway testing, free is fine. For anything you care about keeping alive, you want IPs that aren't shared with strangers.

## One IP Per Profile, Not One IP For Ten

HidemyAcc's own FAQ answers this directly: each browser profile should use a separate proxy server to avoid duplicated IPs and account linking. Ten profiles behind one proxy is ten accounts with the same address in the logs — the fingerprints are irrelevant at that point.

That constraint is what turns proxy choice into a budget question. Profile count drives the plan, not the other way around.

## 9Proxy Plans and Current Pricing

9Proxy is a residential proxy provider that advertises 20M+ residential IPs across 90+ countries, with HTTP, HTTPS and SOCKS5 support, targeting down to country, state, city, ZIP and ISP level, and authentication by username/password, IP whitelisting, or sub-accounts. Support runs through Telegram, email and a ticket system.

Two pricing models, and they reward completely different workloads:

**IP-based plans** — a fixed number of residential IPs with unlimited bandwidth. Better when bandwidth is unpredictable: long sessions, heavy pages, downloads, video.

| Package | Price | Effective rate | Bandwidth |
| --- | --- | --- | --- |
| 100 IPs | $24 | ~$0.24 per IP | Unlimited per IP |
| 500 IPs | $72 | ~$0.14 per IP | Unlimited per IP |
| 1,000 IPs + 500 bonus | $126 | ~$0.08 per delivered IP | Unlimited per IP |
| 100,000 IPs | $2,300 | ~$0.023 per IP | Unlimited per IP |
| 500,000 IPs | $8,625 | ~$0.017 per IP | Unlimited per IP |

Unused IPs on this model are listed as non-expiring. 👉 [Check the current IP-based packages](https://bit.ly/9-Proxy)

**GB-based plans** — you pay for traffic and generate as many endpoints as you want, with no per-IP activation. Better for high-rotation work where each request moves very little data. All GB plans carry 180-day validity.

| Package | Price per GB | Total | Validity |
| --- | --- | --- | --- |
| 5 GB | $3.00 | $15 | 180 days |
| 50 GB + 5 GB bonus | $2.10 | $105 | 180 days |
| 100 GB | $1.50 | $150 | 180 days |
| 200 GB | $1.00 | $200 | 180 days |
| 1,000 GB | $0.80 | $800 | 180 days |
| 2,000 GB | $0.75 | $1,500 | 180 days |
| 10,000 GB | $0.68 | confirmed at checkout | 180 days |

👉 [See the GB-based plans and generate endpoints](https://bit.ly/9-Proxy)

There are also **bundle packages** that combine IP access with GB traffic for setups that need both sustained sessions and heavy rotation — worth pricing against your actual numbers rather than guessing.

Two things above the standard plans matter if you're running this as a business. The Enterprise program includes unlimited data validity (everything doesn't vanish after 180 days) plus a team setup of one owner and up to five members, with per-member traffic controls, activity logs and shared bandwidth that doesn't expire. And vendor-side automation worth knowing about: 9Proxy documents an auto-refresh that detects and replaces dead IPs within about a minute, and an IP reuse feature for addresses used in the previous 24 hours.

Prices are published rates and they do get adjusted — the current numbers on the pricing page are the ones that count.

## Which Plan Fits Your HidemyAcc Setup

Think in profiles, then multiply.

**Under 20 profiles, mostly logins and manual work.** One IP per profile means you need 20 IPs or fewer. The 100-IP package at $24 covers it with room to spare, and unlimited bandwidth removes the anxiety of leaving a session open all day. If your profiles only run short, light tasks, a small GB package plus sticky sessions can come out cheaper — 5 GB is enough to find out how fast you actually burn traffic.

**100–500 profiles for marketplaces, social accounts or client work.** This is where the 500-IP and 1,000-IP tiers make sense, and where you should care about sticky sessions more than rotation. Accounts that log in from a different city every hour look wrong. Keep the session alive, keep the profile's timezone locked to the IP, and disable WebRTC if anything rotates.

**Scraping or data collection through HidemyAcc.** Rotating GB-based plans fit better, because each request pulls a few hundred kilobytes and you'd waste money paying per IP. Run the same batch through a small package first and count successful responses, not requests sent — that number reorders most price comparisons.

**Agencies and teams.** If more than one person touches the proxy pool or the billing, the Enterprise tier's seat structure and non-expiring shared bandwidth are cheaper than running separate accounts and reconciling them later.

👉 [Start with a small package and scale once you know your real usage](https://bit.ly/9-Proxy)

## Troubleshooting the Common Failures

**Check Proxy returns "Can't connect to proxy server."** Usually one of three things: wrong protocol selected (SOCKS5 credentials entered under HTTP is the classic), expired proxy, or — on IP-based 9Proxy plans — a skipped port-forward step. Verify the proxy works outside HidemyAcc first. If it does, the problem is your profile configuration, not the provider.

**The proxy works, but the profile shows your home IP.** Check the WebRTC tab. If it's set to Real, that's your answer. Set it to Altered for static proxies, or Disable when rotating.

**Everything connects but sites behave oddly.** Compare the profile's reported timezone and language against the proxy location. A US residential IP paired with an unexpected locale and a European timezone is a combination real users don't produce.

**Profiles keep getting linked.** Count proxies against profiles. If the numbers don't match one-to-one, that's the issue, and no amount of fingerprint tuning fixes it.

**Bulk operations are greyed out.** Bulk export, run, delete and copy-ID are Business-tier features in HidemyAcc. Check your plan before assuming a bug.

## Quick Answers

**Does HidemyAcc include proxies?** From the Base package up, yes — around 10,000 free proxies. They're shared datacenter IPs, and HidemyAcc's own docs recommend your own proxy for real work.

**Which protocol should I pick?** SOCKS5 unless you have a specific reason not to. It handles more traffic types and doesn't rewrite requests.

**Can I run several profiles on one proxy?** You can, and you'll get accounts linked to each other. One proxy per profile.

**Does 9Proxy work with HidemyAcc?** Yes — 9Proxy publishes a dedicated HidemyAcc setup guide covering both its GB-based and IP-based products.

**What's the cheapest way to test it?** HidemyAcc's 7-day trial plus a small proxy package. Buy the smallest tier that covers your profile count, run one real task end to end, then size up based on what you actually consumed.

The setup itself takes about five minutes per profile once you've done one. The decisions that matter are earlier: one proxy per profile, the right billing model for how your traffic actually behaves, and WebRTC handled correctly for whichever session type you chose.

👉 [Open a 9Proxy account and set up your first HidemyAcc profile](https://bit.ly/9-Proxy)
