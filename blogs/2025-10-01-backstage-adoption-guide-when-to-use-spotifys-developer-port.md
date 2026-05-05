---
title: "Backstage Adoption Guide: When to Use Spotify’s Developer-Portal Framework"
url: "https://earthly.dev/blog/backstage-adoption-guide/"
date: "2025-10-01T00:00:00-04:00"
author: "Brandon Schurman"
feed_url: "https://earthly.dev/blog/feed.xml"
---
<!-- vale HouseStyle.Spacing = NO -->
<div class="notice--info">
<p><strong>TL;DR:</strong></p>
<ul>
<li>I interviewed 20+ Backstage teams from companies of all types and sizes<br />
</li>
<li>I asked them about their experience: what worked, and what didn’t<br />
</li>
<li>Here’s their advice (and warnings) to help you get started (or not) with the ever-so-popular open-source IDP framework</li>
</ul>
</div>
<p>If you’ve spent more than five minutes in the <a href="https://humanitec.com/platform-engineering-slack">platform engineering Slack</a>, you’ve heard about Backstage. It’s the open-source darling of internal developer portals (IDPs), claiming 67% of the market and promising to tame the chaos of microservices with a single pane of glass.</p>
<p>For many teams, Backstage has been a huge win. But here’s the catch: building a production-ready IDP is a serious investment. Some teams abandon the effort halfway, while others celebrate gains in productivity and DevEx.</p>
<p>I wanted to know why Backstage clicks for some organizations but falls flat for others, so I spoke with 20 engineering teams — from scrappy startups to global enterprises — who’ve lived the Backstage life. They shared what worked, what didn’t, and what they wish they’d known before starting.</p>
<p>This guide distills their advice into practical tips you can use to decide whether Backstage is the right move for your team, and how to make your IDP initiative a success… without burning months of engineering time.</p>
<figure>
<img alt="" src="https://earthly.dev/.netlify/images?url=/blog/assets/images/backstage-adoption-guide/backstage-market-share.png" /><figcaption>Backstage leads the IDP market with 67% share, <a href="https://newsletter.getdx.com/p/backstage-and-the-developer-portal-market">according to DX research</a></figcaption>
</figure>
<hr />
<h2 id="backstage-in-60-seconds">Backstage in 60 Seconds</h2>
<p>At its core, Backstage is a <strong>service catalog</strong>. A single place where developers can find details about every microservice and component: docs, ownership, dependencies, onboarding steps, and more.</p>
<p>On top of that, Backstage offers two big draws:</p>
<ul>
<li>Scaffolder: Templates for spinning up new services with best practices baked in.<br />
</li>
<li>Plugins: From scorecards to security checks (and plenty of custom ones you’ll <del>probably</del> <em>definitely</em> end up writing).</li>
</ul>
<p>Interestingly, not every team uses the service catalog. For some, the scaffolder was the only feature they needed, and it delivered enough value on its own.</p>
<p>A word of caution: <strong>where you start can make or break your initiative</strong>. Roll out too much at once, and you’ll burn cycles on unclear value and confused users. Make sure you have a sharp focus and a clear ROI argument before you start. As one user put it:</p>
<p><strong>“Don’t try to pull in every Backstage tool at once. Start with one (catalog, docs, or scaffolder), roll it out, get feedback, then add the next.”</strong> <em>— <a href="https://www.linkedin.com/in/zeshan-ziya/">Zeshan Ziya</a> (Axelerant)</em></p>
<hr />
<h2 id="when-backstage-makes-sense-and-when-it-doesnt">When Backstage Makes Sense (and When It Doesn’t)</h2>
<p>Backstage isn’t a silver bullet. It only pays off when it fits your org’s size, culture, and appetite for DIY, and when it’s pointed squarely at a real pain (microservice sprawl, onboarding drag, inconsistent templates, tool sprawl, etc.). Use this quick test to self-qualify before you commit.</p>
<!-- markdownlint-disable-next-line MD026 -->
<h3 id="backstage-makes-sense-if">Backstage makes sense if:</h3>
<ul>
<li>You’ve got scale pain: Multiple teams and dozens (or hundreds) of services mean nobody can answer “who owns what?” without a hunt.<br />
</li>
<li>You want a developer-first home base you can deeply tailor with custom plugins, processors, and data enrichments<br />
</li>
<li>You can spare ~3–5+ engineers to build &amp; maintain it.<br />
</li>
<li>You have (or can get) top-down support from management to encourage (or require) usage of your IDP<br />
</li>
<li>Your paved-road / golden-path story primarily targets <em>new</em> services as opposed to <em>existing</em>, legacy services<br />
</li>
<li>Your culture tolerates iterative rollouts &amp; experimentation: start with catalog or onboarding, prove value, expand<br />
</li>
<li>You want docs that live with code (i.e. markdown files managed with source control alongside services)</li>
</ul>
<!-- markdownlint-disable-next-line MD026 -->
<h3 id="backstage-may-not-be-right-if">Backstage may not be right if:</h3>
<ul>
<li>You’re a very lean org (&lt; ~30 - 40 engineers) or have only 1 (or zero) part-time maintainers<br />
</li>
<li>You expect a turn-key developer portal that works out-of-the-box<br />
</li>
<li>Your platform/SRE team has zero frontend/TypeScript capacity (and no budget to add it)<br />
</li>
<li>You primarily want leadership dashboards (Scorecards, DORA metrics, etc) as opposed to a developer-first homepage<br />
</li>
<li>You lack executive backing (the “build it and they will come” story rarely works for Backstage)<br />
</li>
<li>You don’t have 6-12 months to properly build your IDP and get it widely adopted<br />
</li>
<li>You’re already entrenched in DIY solutions that aren’t worth replacing with Backstage</li>
</ul>
<p><strong>“We already built so much DevEx infra that was highly specific to our company. We tried retrofitting Backstage, but at that point it was just a UI layer and it didn’t seem worth it.”</strong> <em>— <a href="https://www.linkedin.com/in/yeshwanthvshenoy/">Yeshwanth Shenoy</a> (Okta, ex-Rakuten)</em></p>
<p><strong>Rule of thumb:</strong> If the time you’re currently wasting finding owners, bootstrapping infra, or re-explaining onboarding materials easily adds up to a few engineer-months a year, Backstage can pay for itself. If not, start lighter, or consider using a vendor.</p>
<hr />
<h2 id="is-backstage-free">Is Backstage Free?</h2>
<p><strong>“The homepage literally says ‘an open-source <em>framework</em> for building developer portals’. It doesn’t say ‘a free developer portal.’ You still have to build the thing.”</strong> <em>— <a href="https://www.linkedin.com/in/utf9k/">Marcus Crane</a> (Halter, ex-Lightspeed)</em></p>
<figure>
<img alt="" src="https://earthly.dev/.netlify/images?url=/blog/assets/images/backstage-adoption-guide/free-software.png" /><figcaption>Open-source software isn’t always “free”</figcaption>
</figure>
<p>I don’t know who needs to hear this, but <em>open-source ≠ free</em> and Backstage is Exhibit A. Even if you never pay Spotify a cent, you’ll still spend real money (and calendar time) in four places:</p>
<ul>
<li><strong>Engineering hours</strong> — 3-5 full-time engineers seems to be the ideal size for a Backstage support team (those with less often struggle with workload)<br />
</li>
<li><strong>Front-end expertise</strong> — plugins are React/TypeScript; several Platform teams had to upskill or hire FE help<br />
</li>
<li><strong>Infrastructure &amp; SRE</strong> — you run the thing: CI/CD, auth, Postgres, monitoring, backups, staging environments, etc<br />
</li>
<li><strong>Commercial add-ons</strong> — Some plugins are paid, like Spotify’s own Soundcheck, and they can cost as much as a standalone vendor</li>
</ul>
<p>The SRE costs should not be underestimated. As one user put it:</p>
<p><strong>“Once people started relying on Backstage, it really needed to be treated like a production service. It had to be up and reliable all the time, otherwise we literally couldn’t ship or troubleshoot anything.”</strong> — <a href="https://www.linkedin.com/in/juliozynger/"><em>Julio Zynger</em></a> <em>(Zenjob, ex-SoundCloud)</em></p>
<p>Back-of-the-napkin numbers:</p>
<ul>
<li>DIY Backstage with 3 engineers in a mid-size org: US $380-650k per year (incl. modest infra)<br />
</li>
<li>Fully managed SaaS IDP for 200 engineers @ $35/dev/mo: $84K per year<br />
</li>
<li>Hybrid DIY core + premium plugins and fewer (1-2) devs: $150-250k per year</li>
</ul>
<p>Your mileage will vary, but the lesson is clear: building an IDP is a major investment that needs to be planned with ROI in mind.</p>
<h2 id="common-pitfalls-with-backstage">Common Pitfalls with Backstage</h2>
<p>These are some of the common challenges I heard from the 20+ Backstage teams I’ve spoken to.</p>
<h3 id="under-estimating-head-count-and-fe-skills">1. Under-estimating head-count (and FE skills)</h3>
<p><strong>“You need someone who can actually write TypeScript if you want to keep building plugins. That’s hard when your org is all Go devs.”</strong> <em>— <a href="https://www.linkedin.com/in/lucasweatherhog/">Lucas Weatherhog</a> (Giant Swarm)</em></p>
<p>Most teams that thrive on Backstage dedicate 3-5 engineers, including at least one comfortable in React/TypeScript. Under-staff it, and you may struggle to make meaningful progress. A single engineer supporting 130 users on Backstage said this:</p>
<p><strong>“Almost all my time goes into keeping the catalog data accurate. There’s no bandwidth left to build plugins.”</strong> — <a href="https://www.linkedin.com/in/alexandr-puzeyev/"><em>Alexandr Puzeyev</em></a> <em>(Tele2 Kazakhstan)</em></p>
<h3 id="docs-for-everyone-not-quite">2. Docs for everyone? Not quite</h3>
<p><strong>“TechDocs works great for the engineers, but when we asked the designers and PMs to learn GitHub and write Markdown, it just wasn’t going to happen. They stuck with Confluence.”</strong> — <a href="https://www.linkedin.com/in/rorynelsonscott/"><em>Rory Scott</em></a> <em>(Duo Security, ex-Fanatics)</em></p>
<p>Backstage shines for code-adjacent docs. Non-engineering teams usually keep their own tools, and that’s okay.</p>
<p><strong>“Backstage feels like it’s built for developers first. The UI, the YAML, the whole mindset. Tools like Cortex look great on a leadership dashboard, but they don’t speak to engineers the way Backstage does.”</strong> — <a href="https://www.linkedin.com/in/adamtester/"><em>Adam Tester</em></a> <em>(Deel)</em></p>
<h3 id="chasing-100-adoption">3. Chasing 100% adoption</h3>
<p>I previously wrote about this on <a href="http://platformengineeringisdead.com">platformengineeringisdead.com</a> (as part of a <a href="https://earthly.dev/blog/platform-eng-is-dead/">PlatformCon stunt</a>). Successful Backstage initiatives aim for 80% of use-case coverage. Pushing for the last 20% often burns more hours than it’s worth, especially with Scaffolder, where retro-templating legacy services quickly snowballs the backlog.</p>
<p>If your goal is universal standards, consider tools that enforce them outside the template path (<a href="https://earthly.dev/">Earthly Lunar</a>). Meanwhile, lean on automation to lighten the catalog load:</p>
<p><strong>“We generate the catalog-info.yml files automatically from our internal service registry. Developers only jump in to tweak things if the script gets something wrong.”</strong> — <a href="https://www.linkedin.com/in/jamesandrewvaughn/"><em>Andy Vaughn</em></a> <em>(AppFolio)</em></p>
<h3 id="missing-exec-sponsorship">4. Missing exec sponsorship</h3>
<p><strong>“If you’re a big, tech-heavy organization and you really have leadership support to invest in developer experience, then you should adopt something like Backstage. But if leadership support isn’t there, don’t even go down that road.”</strong> — <a href="https://www.linkedin.com/in/yaser-toutah-87108a11b/"><em>Yaser Toutah</em></a> <em>(Talabat, ex-Expedia Group)</em></p>
<p>Getting enough capacity to support Backstage — and persuading other teams to adopt it — requires leadership backing. Teams that treated Backstage as an after-hours side project and waited for organic uptake usually stalled out within months.</p>
<h2 id="how-to-succeed-with-backstage-and-prove-roi">How to Succeed with Backstage (and Prove ROI)</h2>
<p>Building an IDP takes real effort, but many teams see a clear pay-off once they can measure the benefits.</p>
<p>Backstage demands proof. If you can’t show hard numbers, your portal will be the first line-item to vanish in the next budget review. Here are several example metrics to turn your “nice portal” into a “business win”.</p>
<table>
<colgroup>
<col style="width: 33%;" />
<col style="width: 33%;" />
<col style="width: 33%;" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Use-case</th>
<th style="text-align: left;">What to track</th>
<th style="text-align: left;">How to frame it</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><strong>Developer-experience</strong></td>
<td style="text-align: left;">Quarterly pulse surveys</td>
<td style="text-align: left;">“DX score jumped from 6.4 → 8.1.”</td>
</tr>
<tr class="even">
<td style="text-align: left;"><strong>New-hire onboarding</strong></td>
<td style="text-align: left;">Days to first merged PR</td>
<td style="text-align: left;">“Ramp-up shrank from 14 days to 5.”</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><strong>Service scaffolding</strong></td>
<td style="text-align: left;">Hours DevOps spent vs. self-service template time</td>
<td style="text-align: left;">“60 sec template vs. 4–6 weeks manual build.”</td>
</tr>
<tr class="even">
<td style="text-align: left;"><strong>Developer throughput</strong></td>
<td style="text-align: left;">DORA lead-time &amp; deployment-frequency</td>
<td style="text-align: left;">“Ship frequency up 30%, lead-time down 25%.”</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><strong>Incident response</strong></td>
<td style="text-align: left;">PagerDuty / OpsGenie MTTR before vs. after service dashboard</td>
<td style="text-align: left;">“Mean time-to-resolve fell from 90 min to 55 min.”</td>
</tr>
<tr class="even">
<td style="text-align: left;"><strong>Docs find-time</strong></td>
<td style="text-align: left;">Small time-in-motion study → extrapolate org-wide hours saved</td>
<td style="text-align: left;">“We free ~2 FTEs a year just by centralising docs.”</td>
</tr>
</tbody>
</table>
<p><strong>“We proved we could deliver a microservice into an environment in about 60 seconds. It used to take four to six weeks.”</strong> — <a href="https://www.linkedin.com/in/matthew-law-367b275/"><em>Matt Law</em></a> <em>(The Warehouse Group)</em></p>
<p>A simple playbook:</p>
<ol type="1">
<li><strong>Anchor on a pain with a price-tag</strong> — Three to five engineers for 6–12 months costs real money. Show what it will save or unlock.<br />
</li>
<li><strong>Run a laser-focused pilot</strong> — If docs sprawl is the sore spot, tackle only TechDocs first. Partner with one or two friendly teams.<br />
</li>
<li><strong>Publish the numbers</strong> — Compare pilot metrics to baseline. Turn the wins into a one-pager for execs and an internal demo for peers.<br />
</li>
<li><strong>Scale with advocacy</strong> — Use leadership sponsorship, early-adopter testimonials, and brown-bag demos to bring in the next wave of teams.<br />
</li>
<li><strong>Rinse &amp; repeat for a new use-case</strong> — When the catalog is humming, circle back to step 1 for Scaffolder, plugins, and other use cases.</li>
</ol>
<p>Keep the loop small, measurable, and relentlessly tied to business value. Backstage will sell itself once the numbers do.</p>
<h2 id="so-is-backstage-really-worth-it">So… Is Backstage Really Worth It?</h2>
<p>When it lands, the pay-off is real: teams report slashing days of boilerplate work, onboarding faster, and spending less time hunting for “who owns this?” But for every smooth rollout there’s a cautionary tale where DIY effort ballooned faster than the ROI could keep up.</p>
<p>Want a deeper dive into the history and current adoption trends? Check out “<a href="https://earthly.dev/blog/backstage-is-at-peak-hype/">Backstage Is at The Peak of Its Hype</a>”.</p>
<p>If you do commit, remember: running Backstage is like launching an internal startup. You’ll need a clear problem statement, executive investors, a roadmap, and a team that treats fellow engineers as customers. (P.S. If the startup life is for you, <a href="https://jobs.earthly.dev/35107">we’re hiring</a>)</p>
<h2 id="ready-to-raise-the-bar-in-engineering-excellence">Ready to raise the bar in engineering excellence?</h2>
<p><a href="https://earthly.dev/"><strong>Earthly Lunar</strong></a> is the SDLC monitoring platform built for the messy reality of engineering at scale. It’s like production monitoring, but for everything that happens <em>before</em> production — bringing real-time visibility into your entire development lifecycle: from commit to deploy, without changing dev infrastructure.</p>
<p><strong>Policy Engine for your SDLC</strong><br />
Lunar monitors your code and CI systems to collect SDLC metadata (config files, test results, IaC usage, dependency declarations, security scans, and more). It continuously evaluates this data against your organization’s engineering standards, then enforces those policies by providing feedback to developers directly in their PRs.</p>
<p>It even integrates with your existing Backstage or other software catalogs.</p>
<p><strong><a href="https://earthly.dev/earthly-lunar/demo">👉 See it in action</a></strong></p>
