---
title: "We Interviewed 100 Eng Teams. The Problem With Modern Engineering Isn’t Speed. It’s Chaos."
url: "https://earthly.dev/blog/engineering-chaos/"
date: "2025-04-16T00:00:00-04:00"
author: "Vlad A. Ionescu"
feed_url: "https://earthly.dev/blog/feed.xml"
---
<p>Last year, our team spent a lot of time interviewing fellow Platform, DevOps, DevEx, CI/CD, and SRE engineers, as well as engineering leaders, in order to better understand their day-to-day challenges. We began this effort to see how <a href="https://earthly.dev/earthfile">Earthfiles</a>, one of our products, could serve engineering teams at scale. But as we spoke to more and more people, we realized that platform engineering as an industry is on a collision course with something far more painful and visceral than just <a href="https://earthly.dev/blog/the-roi-of-fast/">build speed</a>.</p>
<p>It was the summer of 2024, and we needed to turn open-source success into commercial success for Earthfiles. Eleven thousand GitHub stars. How hard could it be to monetize that traction?</p>
<p>To make venture-scale money, we needed to go up-market and figure out what makes mid-size companies and enterprises tick and how our product might be able to help them. So we started interviewing platform and engineering leaders across the industry. DocuSign, Affirm, Roblox, Palo Alto Networks, Twilio, LinkedIn, Box, Morgan Stanley, BNY, and many more. We spoke to over 100 of these.</p>
<p>We started with a simple question:</p>
<blockquote>
<p>What are the top issues that you’re struggling with in your day-to-day work?</p>
</blockquote>
<p>We were hoping to get validation that developer productivity is a top concern and then be able to further narrow down how CI/CD speed would be able to unlock developer efficiency. But of all these interviews, only one mentioned build speed as a top issue, and it was largely biased by a recent production incident where they couldn’t get the fix out quickly enough due to a slow end-to-end CI/CD process.</p>
<p>In fact, the top issues they typically mentioned had nothing to do with productivity - not on the surface, anyway. It had to do more with how to best manage the engineering chaos that becomes inevitable at scale. You see, in the era of containers and microservices, there has been a general trend for companies to give more and more freedom to individual dev teams. It’s a container - if it slots in nicely in production, there’s less of a concern about what’s <strong>inside</strong> the container. <a class="footnote-ref" href="https://earthly.dev/blog/engineering-chaos/#fn1" id="fnref1"><sup>1</sup></a></p>
<p>The increased freedom results in an <strong>explosion of diversity</strong> at the dev infrastructure layer. Within any given company, you’ll find a mix of programming languages, CI technologies, build scripts, packaging constructs, in-house scripts, adapters - you name it. Every team’s setup is a unique snowflake. Even within the same programming language ecosystem, different teams will set up their dev process completely differently. Completely different build, test, packaging logic. Completely different runtime versions. Completely different eng culture. So on and so forth. This craziness is now the norm. <a class="footnote-ref" href="https://earthly.dev/blog/engineering-chaos/#fn2" id="fnref2"><sup>2</sup></a></p>
<h2 id="explosion-of-diversity">“Explosion of diversity”</h2>
<p>This core problem of tech stack diversity is what we heard more commonly in our interviews. The interesting aspect of it is that different companies explained it differently to us, and different personas in the organizations were impacted by different consequences.</p>
<p>Platform teams complained about the constant firefighting required to support every app team’s unique needs. App teams on the other hand are focused on shipping features quickly - they complained about having to reinvent the wheel over and over again, about being slowed down by rigid deployment blockers, and about being given production readiness requirements very late in the process. Security teams complained about not having any visibility into the chaos. Engineering leadership complained about not being able to enforce high-quality engineering standards and not being able to understand the level of maturity of each app.</p>
<p>Everybody complained in their own way about the same fundamental core issue: <strong>extreme tech diversity is impossible to govern efficiently.</strong></p>
<h2 id="the-goal-isnt-total-standardization">The goal isn’t total standardization</h2>
<p>The other thing we heard loud and clear is that going back to the pre-microservice era of more standardized tech stacks isn’t a solution. Freedom is useful and necessary. It enables innovation. And hey, for many orgs, even if they suddenly thought that freedom is a bad thing, it would be impossible to go back and rewrite all the existing functionality to make the tech stack consistent. It’s just too much work.</p>
<p>We took it all in.</p>
<p>The industry is seemingly facing a catch-22. You can’t have strong innovation without freedom. You can’t have high-quality engineering and security without standardization.</p>
<p>We became obsessed with this problem: <strong>How do you preserve freedom, but still enforce the right standards at scale?</strong></p>
<h2 id="how-organizations-deal-with-this-today">How organizations deal with this today</h2>
<p>After speaking to over 100 engineering leaders, we identified a handful of common strategies for dealing with engineering chaos. Each has its strengths but also major weaknesses.</p>
<table>
<colgroup>
<col style="width: 50%;" />
<col style="width: 50%;" />
</colgroup>
<thead>
<tr class="header">
<th>Approach</th>
<th>Issues</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1. <strong>Common CI/CD Templates</strong> – Centralizing workflows via reusable templates works well for companies that adopted them early. But in mature orgs, adoption is rarely 100%, and maintaining consistency is a losing battle.</td>
<td>Rigid, difficult to retrofit, and often resented by app teams.</td>
</tr>
<tr class="even">
<td>2. <strong>Manual Checklists</strong> – Reviews per PR or before launches. Cheap and flexible, but prone to human error and rubber-stamping.</td>
<td>Inefficient, inconsistent, and lacks ongoing visibility.</td>
</tr>
<tr class="odd">
<td>3. <strong>Scorecards (IDPs)</strong> – Great for accountability and high-level visibility. But they’re shallow, with limited CI/CD support and no shift-left feedback.</td>
<td>Issues are discovered too late, and enforcement is manual and inconsistent.</td>
</tr>
<tr class="even">
<td>4. <strong>Individual Vendor Tools</strong> – Best for depth in specific areas like code scanning, testing, or licensing. But without unification, coverage remains inconsistent and fragmented.</td>
<td>Too many dashboards, poor integration, no centralized control plane.</td>
</tr>
<tr class="odd">
<td>5. <strong>DIY Solutions</strong> – Custom internal systems provide deep insights but are costly and hard to maintain.</td>
<td>Scalability issues, limited shift-left feedback, and incomplete enforcement.</td>
</tr>
<tr class="even">
<td>6. <strong>Doing Nothing</strong> – Policies without enforcement. It’s compliance theater: the intention is there, the tools exist, but there’s no way to track or govern what’s actually happening across teams.</td>
<td>Inconsistent enforcement, lack of visibility, massive risk.</td>
</tr>
</tbody>
</table>
<p>Each approach tackles part of the problem in some way but none solves it entirely.</p>
<h2 id="what-now">What now?</h2>
<p>The more we listened, the more we realized our mission had to grow beyond what we first imagined.</p>
<p>We started out Earthly with the goal of helping teams tame CI/CD complexity in today’s world of diverse tech stacks. One way to do that is to empower teams managing CI/CD (both platform and app teams) to be more effective in how they develop and run CI scripts. Consistent and fast CI scripts means that collaboration barriers are greatly reduced between these diverse ecosystems, and engineering teams as a whole are more productive. Certainly, that is the mission of Earthfiles.</p>
<p>But, another way to look at it is to step back and address the bigger problem. Enterprises are struggling to tame not just CI/CD complexity, but SDLC complexity as a whole, because it’s riddled with the same diversity, but also entangled with the difficulties of managing people at scale and giving every team the freedom to innovate with the right tools for the job, but to do so safely, within guardrails that aren’t slowing them down.</p>
<h2 id="earthly-lunar-monitoring-for-the-sdlc">Earthly Lunar: Monitoring for the SDLC</h2>
<p>After over a hundred interviews, one insight became impossible to ignore: <strong>a significant chunk of production incidents originate from issues that could have been caught earlier in the software development lifecycle.</strong> And yet, while we’ve built a whole industry around monitoring and securing production systems, we treat everything before production like the Wild West.</p>
<p>This is why we are building <strong><a href="https://earthly.dev/">Earthly Lunar</a></strong>.</p>
<figure>
<img alt="" src="https://earthly.dev/.netlify/images?url=/blog/assets/images/engineering-chaos/initiatives.png" /><figcaption>Global visibility over engineering practices without the need to integrate in every team’s messy CI/CD pipeline</figcaption>
</figure>
<p><strong>Lunar is a platform for monitoring engineering practices at scale. It’s like production monitoring, except it targets everything that happens before production.</strong> It gives Platform, DevEx, Security, QA, and Compliance teams real-time visibility into how applications are being developed, together with the power to gradually enforce specific practices — across every project, in every PR and in every deployment.</p>
<p>Lunar works by instrumenting your existing CI/CD pipelines (no YAML changes needed) and source code repositories to collect structured metadata about how code is built, tested, scanned, and deployed. This metadata is then continuously evaluated against policies that you define — policies that are flexible, testable, and expressive enough to reflect your real-world engineering standards.</p>
<figure>
<img alt="" src="https://earthly.dev/.netlify/images?url=/blog/assets/images/engineering-chaos/pr.png" /><figcaption>Continuous compliance enables application developers to understand what’s wrong in context, right in their PR</figcaption>
</figure>
<p>Want to block deployments that would violate compliance rules, like using unapproved licenses or bypassing required security scans? Or fail a PR if it introduces stale dependencies or vulnerable CI plugins? Or ensure that security-sensitive services are collecting SBOMs, running code scans, and deploying frequently enough to avoid operational drift? Lunar makes all of that possible — without requiring a wholesale rewrite of every team’s CI pipeline, and without sacrificing developer velocity.</p>
<p>And crucially, <strong>Lunar is designed to work with the messy reality of modern engineering.</strong> It’s not a one-size-fits-all template, and it doesn’t require rewriting every CI pipeline. Its instrumentation is flexible and centralized — meaning platform teams stay in control, app teams stay autonomous, and standards actually get enforced.</p>
<h2 id="finally">Finally</h2>
<p>Engineering at scale is messy. You’ve got hundreds of services, dozens of teams, and a sprawling ecosystem of tools — each doing one part of the job. But stitching that all together into a coherent, reliable, and compliant software delivery process? That’s the hard part. And that’s what Earthly Lunar is here to solve.</p>
<p>If this sounds like a problem you’re facing, we’d love to show you how Lunar works in practice.</p>
<p>👉 <a href="https://earthly.dev/">Visit the Lunar homepage</a></p>
<p>👉 <a href="https://earthly.dev/book-demo/">Book a demo</a></p>
<section class="footnotes">
<hr />
<ol>
<li id="fn1"><p>Whereas previously, writing a component in the wrong language would simply be incompatible with production altogether. Remember the Java servlet days?<a class="footnote-back" href="https://earthly.dev/blog/engineering-chaos/#fnref1">↩︎</a></p></li>
<li id="fn2"><p>There are several exceptions still, of course, like the Google’s and Facebook’s of the world. Companies born before the era of containers, and more generally, companies who have invested heavily in common CI/CD infrastructure for one reason or another. But most enterprises aren’t like that.<a class="footnote-back" href="https://earthly.dev/blog/engineering-chaos/#fnref2">↩︎</a></p></li>
</ol>
</section>
