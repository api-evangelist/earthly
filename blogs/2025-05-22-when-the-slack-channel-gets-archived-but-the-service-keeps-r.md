---
title: "When the Slack Channel Gets Archived, but the Service Keeps Running"
url: "https://earthly.dev/blog/slack-archived-service-running/"
date: "2025-05-22T00:00:00-04:00"
author: "Vlad A. Ionescu"
feed_url: "https://earthly.dev/blog/feed.xml"
---
<!-- vale HouseStyle.Spacing = NO -->
<div class="notice--info">
<p><strong>TL;DR:</strong></p>
<p>We interviewed 100+ companies to understand how they manage engineering governance in the face of dev setup entropy. This post breaks down six patterns we saw — from CI templates to scorecards to DIY platforms — and shows where each one succeeds, fails, or quietly collapses under real-world pressure.</p>
</div>
<blockquote>
<p>It still runs.</p>
<p>The service, buried deep in the infrastructure, still receives traffic. Still logs errors. Still serves a feature that someone, somewhere, might rely on. No one remembers exactly what it does. The README is out of date. The Slack channel was archived two layoffs ago.</p>
<p>Once, it had a team. A mission. Engineers sat in a pod, under warm fluorescent lights, planning features and joking over bad coffee. They gave the service a clever name. They wrote dashboards. They argued over endpoint naming conventions.</p>
<p>And then time passed.</p>
<p>Reorgs swept through. Teams were renamed, merged, dissolved. People left. Ownership blurred. Documentation drifted.</p>
<p>Today, it’s still deployed — but untended. Not quite dead. Not quite alive. Ask the SRE team, and you’ll hear a sigh: “We think it’s critical, but nobody owns it anymore.”</p>
</blockquote>
<p>We heard dozens of stories like this. Different details. Same themes.</p>
<p>A service running in limbo. A checklist ticked, but never read. A vulnerability found, but never fixed.</p>
<p>This is how engineering chaos creeps in. Not through malice — but through entropy. Through drift. Through the thousand tiny decisions that feel right in isolation, but accumulate into a system no one fully understands or controls.</p>
<p><a href="https://earthly.dev/blog/lunar-launch/">In a previous article</a>, we explored the root causes: microservices, the explosion of tooling, the limits of standardization, and the widening gap between policy and reality.</p>
<p>This time, we’re going deeper into the coping mechanisms — what companies are actually doing to survive. These aren’t best practices. They’re stress responses. Workarounds. Cultural antibodies. Sometimes admirable. Sometimes alarming.</p>
<p>If you’ve ever asked yourself, “How are we still standing?” — this article is for you. In the sections below, we’ve captured the six most common patterns we saw — not as endorsements, but as field notes. What’s working. What’s breaking. And what it really looks like to fight chaos at scale.</p>
<h2 id="golden-paths-and-common-cicd-templates">1. “Golden paths” and Common CI/CD Templates</h2>
<p>One approach we heard over and over is the push for <em>common CI/CD templates</em>. The idea sounds simple: build a standardized pipeline. Pre-bake security gates, quality checks, compliance steps. Let every team inherit the best practices automatically.</p>
<p>No more chaos. No more gaps. In theory, it’s brilliant. In practice? It’s a lot more complicated.</p>
<p>One engineering leader at a mid-sized tech company told us a story that stuck with us. Their platform team had spent months building a beautiful, standardized CI/CD pipeline — packed with every imaginable check: security scans, compliance validations, code quality verifications, deployment safeguards.</p>
<p>It was everything you could possibly want… except agility.</p>
<p>When one of their app teams needed to move quickly, building a proof-of-concept that demanded agility, the standardized CI/CD templates slowed them down to a crawl.</p>
<p>The template enforced ten different types of scanning, multiple build artifact signatures, lengthy deployment verification steps — all great for production, but suffocating for a scrappy new project trying to iterate fast.</p>
<p>The result? That team quietly abandoned the corporate pipeline altogether. They built their own lightweight, custom CI/CD flow on the side — completely outside the platform team’s governance. Because their custom pipelines weren’t compatible with the company’s core Kubernetes cluster, they had to additionally spin up an entirely separate production environment, starting from scratch.</p>
<p>They weren’t alone, either. Over time, more and more teams opted out, each for slightly different reasons: slowness, inflexibility, incompatible tech stacks.</p>
<p>What was meant to be a unifying standard ended up fracturing the organization even further.</p>
<p>We heard variations of this story at almost every large company we talked to: Rigid templates that worked beautifully in theory, but in reality, couldn’t flex enough to meet the diversity of needs across dozens (or hundreds) of different teams.</p>
<p>The key pain points with CI/CD templates:</p>
<ul>
<li>They are incredibly hard to retrofit once chaos is already entrenched.</li>
<li>They fit a narrow slice of projects, but real-world engineering is messy.</li>
<li>They require almost religious discipline to maintain and evolve — otherwise, templates rot and drift apart just like codebases do.</li>
</ul>
<p>Templates can be powerful. But when they don’t account for the specific needs of each team, they stop being a solution and become yet another source of resentment and shadow infrastructure.</p>
<h2 id="manual-production-readiness-checklists">2. Manual Production Readiness Checklists</h2>
<p>Another common strategy we heard about is relying on manual production readiness checklists.</p>
<p>The theory is straightforward: Before every launch (or sometimes on every PR) an engineer walks through a list of best practices.</p>
<ul>
<li>Did we scan for vulnerabilities? ✅</li>
<li>Did we run all the tests? ✅</li>
<li>Did we validate compliance artifacts? ✅</li>
</ul>
<p>Check, check, check.</p>
<p>On paper, it felt rigorous. But over time, it became something else entirely. Teams like it because it’s lightweight and flexible. Leaders like it because it feels like accountability without heavy infrastructure. But the cracks start to show over time.</p>
<p>A pattern we saw a few times — and one that hit especially hard — came from a well-known security vendor. Their process required engineers to manually verify key readiness criteria before every production push. Everything from security posture to data integrity was supposed to be double-checked and signed off. But after enough repetition, the checklist became muscle memory. People stopped really thinking about each item. It became easy, natural, even, to just… click through.</p>
<p>And one day, that’s exactly what happened. A very senior engineer, under pressure to push out a fix quickly, ticked off a manual verification step without actually performing the underlying check. No malice. No negligence. Just human imperfection, and an overloaded day.</p>
<p>Unfortunately, that missed step allowed inconsistent data to be shipped to production. This resulted in a massive re-ETL operation to clean up customer data — an expensive, painful computational process — and, worse, dashboard inconsistencies that led to widespread customer complaints.</p>
<p>It wasn’t just a checkbox miss. It was customer pain, operational cost, and real fallout.</p>
<p>We heard variations of this story again and again: Even the best engineers — even the most security-conscious organizations — struggle with the basic truth that humans are imperfect. Especially when they’re busy, tired, or under pressure. Manual checklists work great in theory. But in practice, they degrade over time — becoming rubber stamps that create a false sense of security, until the day it really matters.</p>
<h2 id="scorecards-typically-in-idps">3. Scorecards (Typically in IDPs)</h2>
<p>In the last few years, a new tool has started gaining real traction: engineering scorecards, often embedded inside Internal Developer Platforms (IDPs) like Backstage, Cortex, OpsLevel, and others.</p>
<p>The promise sounds irresistible: Catalog all your services, assign clear ownership, track engineering maturity automatically. See which teams are thriving and which ones are falling behind — all from a single dashboard.</p>
<p>When we first started hearing about scorecards in our interviews, the excitement was palpable. Finally, a way to bring order to the chaos! Finally, real visibility into engineering practices!</p>
<p>But as more companies rolled out these systems, reality set in.</p>
<p>One engineering leader put it best:</p>
<p>“At first, it sounds like you’re going to have x-ray vision into your entire SDLC. In practice, it’s more like getting a blurry polaroid.”</p>
<p>Even the scorecard platforms with the richest plugin ecosystems quickly run into a hard truth: Engineering culture is specific. Every company’s engineering process is as unique as a snowflake — shaped by specific needs, regulatory environments, team philosophies, tech stacks, and risk tolerances.</p>
<p>Encoding that nuance into a conventional scorecarding system is impossible. Most scorecards end up measuring only broad, surface-level signals: Does this service have an owner? Is there an on-call rotation? Is the critical vulnerability SLA being met?</p>
<p>Important, yes — but shallow.</p>
<p>Meanwhile, the deeper layers of engineering quality — the ones buried inside CI/CD pipelines, testing practices, security scans, deployment rigor — are almost invisible.</p>
<p>And worst of all: scorecards operate after the fact. Problems aren’t surfaced early, where developers can fix them easily. They’re discovered weeks or months later, when leadership pulls up a dashboard and asks: “Why are we failing this?” By then, the damage is often done: bad practices have shipped to production, technical debt has compounded, and fixing it means slowing down work that teams thought was already finished.</p>
<p>Scorecards are still a young technology. They’re valuable, especially for driving accountability at the leadership level. But they’re not a silver bullet. They’re a snapshot, not a real-time feedback loop. And when it comes to taming engineering chaos at scale, late, shallow visibility isn’t enough.</p>
<h2 id="relying-on-individual-vendor-tools">4. Relying on Individual Vendor Tools</h2>
<p>When it comes to securing the software development lifecycle, most companies aren’t short on tools. If anything, they’re drowning in them.</p>
<p>A moment that crystallized this problem came from a company in a heavily regulated industry — the kind where compliance isn’t optional, and the risk of a breach could mean existential damage.</p>
<p>To stay safe, they invested heavily. Across the organization, they deployed sixteen different security vendors: SAST scanners, dependency auditors, container image validators, SBOM generators, runtime monitors, and more.</p>
<p>At first glance, it sounds like a fortress. Sixteen overlapping layers of defense. But peel back the surface, and the reality was far more chaotic.</p>
<p>A handful of those vendors were owned centrally by a DevSecOps team. The rest? Scattered across the org — bought by individual app teams, integrated however they saw fit, with wildly inconsistent coverage. And when leadership asked the critical questions — “Are we actually covering every service properly?”, “Are new critical vulnerabilities being fixed within 30 days, like our policy says?”, “Which teams are using which vendors, and are they configured correctly?” — the answer was… silence. No one knew.</p>
<p>There was no central dashboard. No inventory of what was installed where. No unified policy enforcement across the patchwork. Just sixteen different vendor consoles, each living in its own world, each only visible to a small subset of teams.</p>
<p>If a new vulnerability popped up in production, finding it wasn’t the problem. It was governing the detection — making sure the right service was protected, making sure the right person was accountable, making sure the vulnerability was remediated on time.</p>
<p>And that governance layer, the most crucial part, simply didn’t exist. This wasn’t an isolated story. We heard versions of this from multiple companies: An impressive arsenal of specialized tools — but no way to tie them together into a coherent, enforceable, visible system. Specialized vendors go deep. But without a unifying governance layer, depth alone isn’t enough. The chaos stays.</p>
<h2 id="diy-engineering-standards-tracking">5. DIY Engineering Standards Tracking</h2>
<p>For companies where the cost of failure is measured in billions — like major banks, insurance giants, and critical infrastructure providers — chaos isn’t just inconvenient. It’s an existential threat. So it’s not surprising that some of the most sophisticated organizations we spoke to have chosen a different path: build their own internal system to track and enforce engineering standards across every project.</p>
<p>One story we heard from a leading financial institution was particularly striking. Over a decade ago, they realized that relying on piecemeal vendor tools and manual processes wasn’t going to cut it. Too much was at stake — regulatory scrutiny, customer trust, brand reputation. So they went all-in.</p>
<p>They built a sprawling internal platform:</p>
<ul>
<li>Every service had to register.</li>
<li>Every build and deployment was instrumented.</li>
<li>SBOMs were tracked.</li>
<li>Test coverage was logged.</li>
<li>Vulnerabilities were cataloged centrally.</li>
<li>Artifacts were signed.</li>
<li>Deployment practices, CI configurations, code ownership — everything was collected, analyzed, and surfaced to leadership.</li>
</ul>
<p>It was, frankly, awe-inspiring. But then came the caveats.</p>
<p>Building that level of oversight wasn’t just expensive. It took years — more than a decade of iteration, executive sponsorship, and dedicated engineering teams working full-time. Dozens of engineers — not one or two — focused solely on maintaining and evolving the platform.</p>
<p>And even with all that effort, cracks still showed through. One of the leaders we spoke with admitted: “We have a very effective process, but not a very efficient one. Enforcing fixes earlier, during development, is still a huge struggle. Bringing feedback to PRs is where we fall short.”</p>
<p>In other words: They could spot problems. They could pressure teams to fix them. But they couldn’t easily prevent bad practices from landing in the first place, without additional heavy-lift interventions.</p>
<p>This wasn’t a story about failure. It was a story about just how high the bar is — and how, even at the top end, real-time governance across the SDLC remains painfully difficult. DIY systems can work. But they require an astronomical investment — and even then, they leave critical gaps that are still hard to close.</p>
<h2 id="doing-nothing">6. Doing Nothing</h2>
<p>Not every company has the resources, or the will, to tackle engineering chaos head-on. Sometimes, the strategy is simpler: write down the right policies, install the right tools, and trust that things will work out.</p>
<p>Everything looked good on paper: policies in place, tools deployed, evidence filed.</p>
<p>But behind the scenes, a different picture often emerges. One story that came up again and again involved how companies handle vulnerability reports. The compliance framework would require that you “catalog known vulnerabilities” for every release. But it wouldn’t necessarily prescribe how those vulnerabilities should be fixed. So teams would dutifully run a scan, generate a long PDF listing all the vulnerabilities, upload it to the compliance evidence system… and move on. The report was created. The checkbox was ticked. And nobody ever opened that file again.</p>
<p>The tool was technically used. The policy was technically followed. But the actual vulnerabilities — the very issues the policy was meant to protect against — often went unaddressed.</p>
<p>As one security lead half-joked to us: “In our industry, we are world-class at knowing what our vulnerabilities are. We’re just not so great at fixing them.” This isn’t laziness. It’s systemic reality.</p>
<p>When companies have hundreds of microservices, dozens of disconnected tools, and no unified enforcement layer, the scale becomes overwhelming.</p>
<p>And so, little by little, governance turns into compliance theater: Doing just enough to pass an audit. Proving you know about the risks, without proving you’re mitigating them.</p>
<p>The risk isn’t visible day-to-day. Until, of course, the day something slips through — and the gap between “knowing” and “doing” becomes very, very real.</p>
<h2 id="why-none-of-these-alone-are-enough">Why None of These Alone Are Enough</h2>
<p>Each approach solves part of the problem. No single strategy solves everything. Here’s how each of the six strategies stacks up across key needs:</p>
<table style="width: 100%;">
<colgroup>
<col style="width: 14%;" />
<col style="width: 14%;" />
<col style="width: 14%;" />
<col style="width: 14%;" />
<col style="width: 14%;" />
<col style="width: 14%;" />
<col style="width: 14%;" />
</colgroup>
<thead>
<tr class="header">
<th>Need</th>
<th>CI Templates</th>
<th>Manual Checklists</th>
<th>Scorecards in IDPs</th>
<th>Individual Vendors</th>
<th>DIY</th>
<th>Do Nothing</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Strict enforcement</strong></td>
<td>✅</td>
<td>❌</td>
<td>❌</td>
<td>⚠️</td>
<td>⚠️</td>
<td>❌</td>
</tr>
<tr class="even">
<td><strong>Early feedback (shift-left)</strong></td>
<td>✅</td>
<td>⚠️</td>
<td>❌</td>
<td>⚠️</td>
<td>⚠️</td>
<td>❌</td>
</tr>
<tr class="odd">
<td><strong>Ease of insertion in existing projects</strong></td>
<td>❌</td>
<td>✅</td>
<td>✅</td>
<td>⚠️</td>
<td>❌</td>
<td>✅</td>
</tr>
<tr class="even">
<td><strong>Full coverage across teams</strong></td>
<td>❌</td>
<td>✅</td>
<td>⚠️</td>
<td>⚠️</td>
<td>⚠️</td>
<td>❌</td>
</tr>
<tr class="odd">
<td><strong>Depth</strong></td>
<td>✅</td>
<td>❌</td>
<td>❌</td>
<td>✅</td>
<td>✅</td>
<td>❌</td>
</tr>
<tr class="even">
<td><strong>Leadership visibility</strong></td>
<td>❌</td>
<td>❌</td>
<td>✅</td>
<td>⚠️</td>
<td>✅</td>
<td>❌</td>
</tr>
<tr class="odd">
<td><strong>Scalability</strong></td>
<td>❌</td>
<td>❌</td>
<td>✅</td>
<td>⚠️</td>
<td>⚠️</td>
<td>✅</td>
</tr>
<tr class="even">
<td><strong>Developer autonomy</strong></td>
<td>❌</td>
<td>✅</td>
<td>✅</td>
<td>⚠️</td>
<td>⚠️</td>
<td>✅</td>
</tr>
</tbody>
</table>
<p>✅ = Good<br />
⚠️ = Partial / Hard / Mixed<br />
❌ = Bad</p>
<p>Today, organizations are choosing a combination of strategies, each compensating for the others’ blind spots. Some are barely holding it together. Some are building brilliant internal systems — but at astronomical cost.</p>
<h2 id="conclusion">Conclusion</h2>
<p>If this all sounds familiar — if you’ve seen these patterns, lived these stories, or fought these fires — you’re not alone.</p>
<p>Every strategy we examined solves a slice of the problem. But what’s missing isn’t effort. It’s integration. The real challenge isn’t checklists, scorecards, or even security tools — it’s that they’re disconnected, shallow, or easy to ignore.</p>
<p>The common thread is a lack of end-to-end visibility and enforceability across the software development lifecycle.</p>
<p>In my (<a href="https://earthly.dev/">biased</a>) opinion, a strong solution would:</p>
<ul>
<li>Instrument the actual places where work happens — CI/CD pipelines and codebases — in a way that is compatible with the diverse nature of today’s tech stacks</li>
<li>Collect and centralize rich SDLC metadata across services and teams</li>
<li>Enforce engineering standards programmatically, not as dashboards, but as PR checks and release gates</li>
<li>Give leadership live visibility into adherence, not just shallow metrics</li>
</ul>
<p>Not another tool on the side. Not yet another dashboard. Not a spreadsheet. Not a PDF uploaded to a compliance folder. What’s needed is a unified layer that connects policy, practice, and production — and closes the loop before the damage is done, not after.</p>
<div class="bg-blue-50 rounded-lg py-6 my-6 cta-container" id="blog-bottom-cta-control">
<div class="mb-4">
<svg class="mb-3 block lunar-logo-cta" fill="none" height="119" viewBox="0 0 501 119" width="501" xmlns="http://www.w3.org/2000/svg">
<path d="M76.0247 30.8587L60.9741 56.9803H60.8721L45.9746 31.1138L76.0247 30.8587Z" fill="#83FF50" stroke="#83FF50" stroke-miterlimit="5.3333" stroke-width="0.510184">  <path d="M86.2689 35.5604H5.45508V0.000343323H86.2689V35.5604Z" fill="white">  <g> <g opacity="0.83"> <path d="M76.156 30.7127L76.105 30.8147H76.054V30.8658L45.9529 31.1208V31.0698H15.8008L15.5967 30.7127L30.7493 4.48903H61.0544L76.156 30.7127Z" fill="#96FF5B" fill-opacity="0.6471"> </g> </g> <path d="M76.0913 30.8193L61.0403 56.9418H60.9893L76.0403 30.8193H76.0913Z" fill="white"> <path d="M61.0593 57.3182L61.0083 57.4202L45.9067 83.5419H15.6526L0.5 57.3182L15.6526 31.0945H15.8056L30.7031 56.9611H60.8553L61.0593 57.3182Z" fill="#00D6FF" stroke="#00D6FF" stroke-miterlimit="5.3333" stroke-width="0.510184"> <path d="M60.8504 56.9579H30.7493L15.8008 31.0914H45.9529L60.8504 56.9579Z" fill="#7DFFFF" stroke="#7DFFFF" stroke-miterlimit="5.3333" stroke-width="0.510184"> <path d="M76.2476 82.8961L76.5027 83.3042H76.0435L64.5642 83.4063L45.9424 83.5593L61.0439 57.4377H90.992L76.2476 82.8961Z" fill="#32E6FF" stroke="#32E6FF" stroke-miterlimit="5.3333" stroke-width="0.510184">  <path d="M99.3161 118.67H38.1445V48.6722H99.3161V118.67Z" fill="white">  <g> <g opacity="0.86"> <path d="M91.6823 109.142L91.2231 109.907H60.969L45.8164 83.6833L45.8674 83.5813L60.969 57.4597H61.02L45.9184 83.5303L64.5403 83.3772L76.0706 83.2752H76.5297L91.3762 109.142H91.6823Z" fill="#00D5FF" fill-opacity="0.5451"> </g> </g> <path d="M76.2471 82.8963L76.5022 83.3044H76.043L61.1455 57.4379H90.9915L76.2471 82.8963Z" fill="#20E6FF" stroke="#20E6FF" stroke-miterlimit="5.3333" stroke-width="0.510184"> <path d="M106.19 83.3025H76.4973L76.2422 82.8943L90.9356 57.436H91.2417L106.19 83.3025Z" fill="#2AF0FF" stroke="#2AF0FF" stroke-miterlimit="5.3333" stroke-width="0.510184">  <path d="M111.413 113.465H71.5156V79.0269H111.413V113.465Z" fill="white">  <g> <g opacity="0.95"> <path d="M106.388 83.663L91.6948 109.121H91.3887L76.4912 83.3058H106.184L106.388 83.663Z" fill="#29EFFF" fill-opacity="0.8"> </g> </g> <path d="M121.491 57.0653L106.338 83.2889H106.185L91.2878 57.4224H61.1357L60.9316 57.0653L60.9827 56.9632L76.0332 30.8416V30.7906H106.338L121.236 56.6061L121.491 57.0653Z" fill="#32F8B9" stroke="#32F8B9" stroke-miterlimit="5.3333" stroke-width="0.510184">  <path d="M144.229 118.67H83.6699V48.2127H144.229V118.67Z" fill="white">  <g> <g opacity="0.85"> <path d="M136.625 83.2665L121.472 109.49L91.2178 109.898L106.217 84.0318L106.013 83.6747H106.166L121.319 57.451L121.064 57.0428H121.523L136.625 83.2665Z" fill="#32F6B8" fill-opacity="0.5647"> </g> </g> <path d="M155.73 81.0842V33.086H176.278V40.3849H162.95V53.4754H172.708V60.7743H162.95V73.7853H176.278V81.0842H155.73Z" fill="#090909"> <path d="M194.371 44.125L191.673 63.0069H197.068L194.371 44.125ZM190.563 70.0678L188.817 81.0955H181.28L189.452 33.1766H199.369L207.382 81.0955H199.766L198.099 70.0678H190.563Z" fill="#090909"> <path d="M229.225 44.6987C229.225 41.922 227.876 40.4939 225.1 40.4939H220.736V55.8058H225.1C226.21 55.8058 227.242 55.4091 228.035 54.6157C228.828 53.8224 229.225 52.791 229.225 51.6803V44.6987ZM224.941 33.1157C228.987 33.1157 231.923 34.2264 233.827 36.4478C235.493 38.3519 236.286 41.1286 236.286 44.5401V51.5216C236.286 54.9331 235.017 57.7892 232.399 60.1692L237.793 81.1139H229.939L225.576 63.0253H224.941H220.736V81.1139H213.517V33.195H224.941V33.1157Z" fill="#090909"> <path d="M249.271 40.4135H241.575V33.1146H264.186V40.4135H256.49V81.1128H249.271V40.4135Z" fill="#090909"> <path d="M277.201 60.7683V81.0782H269.981V33.1594H277.201V53.4694H285.928V33.0801H293.148V80.9989H285.928V60.7683H277.201Z" fill="#090909"> <path d="M319.322 81.0842H299.646V33.1654H306.866V73.8647H319.322V81.0842Z" fill="#090909"> <path d="M325.026 60.9974L315.347 33.0712H323.28L328.675 50.287L333.991 33.0712H342.004L332.245 60.9974V81.0693H325.026V60.9974Z" fill="#090909"> <path d="M491.932 44.6987C491.932 41.922 490.583 40.4939 487.807 40.4939H483.443V55.8058H487.807C488.917 55.8058 489.949 55.4091 490.742 54.6157C491.535 53.8224 491.932 52.791 491.932 51.6803V44.6987ZM487.648 33.1157C491.694 33.1157 494.63 34.2264 496.534 36.4478C498.2 38.3519 498.993 41.1286 498.993 44.5401V51.5216C498.993 54.9331 497.724 57.7892 495.106 60.1692L500.5 81.1139H492.646L488.283 63.0253H487.648H483.443V81.1139H476.224V33.195H487.648V33.1157Z" fill="#49728B"> <path d="M457.229 44.125L454.532 63.0069H459.927L457.229 44.125ZM453.421 70.0678L451.676 81.0955H444.139L452.31 33.1766H462.227L470.24 81.0955H462.624L460.958 70.0678H453.421Z" fill="#49728B"> <path d="M422.21 55.2386V81.0784H414.99V33.1595H422.21L430.937 58.4613V33.0802H438.156V80.999H430.937L422.21 55.2386Z" fill="#49728B"> <path d="M396.539 81.0784V81.0784C390.631 81.0784 385.842 76.2891 385.842 70.3812V33.1595H393.061V69.4812C393.061 71.8911 395.015 73.8447 397.425 73.8447V73.8447C399.835 73.8447 401.788 71.8911 401.788 69.4812V33.0802H409.008V70.3008C409.008 76.2221 404.231 81.0345 398.31 81.0784V81.0784H396.539Z" fill="#49728B"> <path d="M359.312 81.0842V33.086H366.531V40.3849V53.4754V60.7743V73.7853H379.86V81.0842H359.312Z" fill="#49728B">
</svg>
<p class="text-lg font-normal text-gray-700 leading-relaxed">
Turn your engineering standards into automated guardrails that provide feedback directly in pull requests, with 100+ guardrails included out of the box and support for the tools and CI/CD systems you already have.
</p>
</div>
<div class="mt-4">
<p><a class="btn-gradient" href="https://earthly.dev/" target="_blank"> Learn More </a></p>
</div>
</div>
