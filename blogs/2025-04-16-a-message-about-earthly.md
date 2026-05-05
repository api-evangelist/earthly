---
title: "A message about Earthly"
url: "https://earthly.dev/blog/shutting-down-earthfiles-cloud/"
date: "2025-04-16T00:00:00-04:00"
author: "Vlad A. Ionescu"
feed_url: "https://earthly.dev/blog/feed.xml"
---
<!-- vale HouseStyle.Spacing = NO -->
<div class="notice--info">
<p><strong>TL;DR</strong></p>
<ul>
<li>In the next three months, we will be phasing out our Earthly Satellite commercial services, including the Earthly Cloud Satellites, Self-Hosted Satellites, and BYOC Satellites, together with their respective free tiers. We are also phasing out Earthly Cloud Secrets and Logs.</li>
<li>We are also ending active maintenance of the Earthly open-source project.</li>
<li>We are supporting the community’s efforts to self-organize a fork, and we encourage those interested to get involved.</li>
</ul>
</div>
<!-- vale HouseStyle.Spacing = YES -->
<p>Dear Earthly Community,</p>
<p>I’ll start by saying thank you for being here and for helping shape what Earthly is today. Without early adopters like you, there would be no innovation in the world. Our hearts go out to all our community members for believing in us, helping with contributions big or small along the way, and championing Earthly within your organizations.</p>
<p>Today marks the 5-year anniversary of Earthly. Since the launch, we’ve built a vibrant community of developers who share our vision for a better CI/CD experience. Earthly has been adopted by thousands of teams worldwide, with numerous integrations into diverse CI/CD environments.</p>
<p>From container-centric dev experiences to cache optimization strategies, we’ve demonstrated tangible improvements in CI speed and efficiency — providing up to a 10x ROI in compute cost savings and developer productivity. This success is a testament to the creativity and hard work of our community.</p>
<p>With that said, we have encountered some significant challenges when attempting to commercialize Earthly in its current form, and unfortunately, without commercial success, we are no longer able to sustain our development efforts towards the project.</p>
<h2 id="challenge-1-difficulty-of-adoption">Challenge #1: Difficulty of adoption</h2>
<p>Adopting new open-source technology is a slow process. Even the most successful infrastructure companies, like Docker, took nearly a decade to become mainstream. Despite their technical brilliance, finding a commercialization path was challenging.</p>
<p>In the past, venture-backed companies could rely on open-source traction alone. Hashicorp, for example, sustained itself up to Series C — six years after inception — on open-source projects like Vagrant, Packer, and Consul that weren’t even commercialized.</p>
<p>Today, the economic landscape has shifted. Many infrastructure investors have pivoted toward AI, and there is less appetite for pure-play open-source moonshots, making early monetization a necessity.</p>
<p>For Earthly, the need to monetize quickly became a do-or-die situation. While Earthly has seen widespread adoption, translating that adoption into revenue has been much harder than we anticipated. Large organizations, despite initial interest, are reluctant to commit to adopting Earthly widely throughout their infrastructure. Despite many conversations, we couldn’t secure any company-wide top-down deployments - only slow, organic bottom-up motions.</p>
<h2 id="challenge-2-open-source-cannibalization">Challenge #2: Open-source cannibalization</h2>
<p>Our open-source strategy is simple: open-source the syntax and the developer experience to encourage adoption and ecosystem growth, then monetize on dev efficiencies (e.g. faster CI) via Satellites, our build runners.</p>
<p>To this end, we architected Earthly to allow the developer to experience the full power of Earthly locally - including the full speed benefit - while offering Earthly Satellites as a means to reuse cache between runs in CI primarily. But this meant that for some CI environments, the user could run Earthly just like they would run it locally and still get the same speed benefits. And while managing this type of installation isn’t necessarily trivial, in an economy that sees massive layoffs and infrastructure budgets cut significantly, when the leadership isn’t approving any new budgets, the ICs figure out a way to get the value via DIY.</p>
<p>So, even if the user’s CI environment might have been ephemeral initially, they would switch to using a non-ephemeral environment in order to gain the Earthly speed. In short, our users were gravitating toward strategies that avoided our commercial offering (and hey, I get it, I would have done the same if I were in their shoes).</p>
<p>This meant that when adoption did take place bottom-up in big enough companies, we were stuck against comparing the value of Earthly to our own free, open-source offering instead of comparing it to a traditional CI/CD experience. We could no longer claim the 10x value unlock.</p>
<h2 id="what-then">What then?</h2>
<p>There were <a href="https://earthly.dev/blog/shutting-down-earthly-ci/">a few variations</a> of our solution that we attempted to commercialize, but ultimately, we believe that the barrier to entry in the space of builds &amp; CI/CD is extremely high due to pre-existing diverse dev infrastructure that requires adaptation. At the same time, the monetization potential is significantly reduced due to CI compute being viewed as a commodity, and the developer efficiency gains are heavily discounted due to OSS canibalization, together with budget cuts across the tech industry.</p>
<p>And so, after exhausting several options of how to build a business around our initial product, we came to the realization that we needed a significant pivot.</p>
<p>As a result, we are announcing today that, unfortunately, we will no longer be able to offer Earthly Satellites as a commercial offering. All forms of Cloud Satellites, Self-hosted Satellites, and BYOC Satellites, together with all Earthly Cloud features (cloud secrets, logs, etc), will stop working in the coming months.</p>
<p>At the same time, we are also announcing that we will no longer be contributing actively to the <a href="https://github.com/earthly/earthly">Earthly open-source project</a> other than critical bug fixes. Unfortunately, this also means that we are no longer accepting PRs since there is a significant amount of effort needed to vet them.</p>
<p>We understand this news is disappointing, especially for those of you who have invested time, effort, and passion into building with Earthly. Your contributions have been invaluable, and we want to ensure you have the clarity and support needed to navigate this transition.</p>
<h2 id="community-fork">Community fork</h2>
<p>In order to help the Earthly community move forward, we are looking to bring together everyone who would be willing to help maintain a community fork of Earthly. To this end, <a href="https://forms.gle/CMda8gNFUvmPc4Eu8">we have put together a form where you can register interest</a>. If you would be willing to provide some amount of your time weekly to help drive the community fork forward, please fill it out by <strong>April 30th, 2025</strong>.</p>
<p>The only thing that we ask of the community is to change the name and logo of the project, as well as the name of the CLI command when forking, as we want to retain trademark rights - we will continue using “Earthly” and the distinctive logo in our company’s name and in future products.</p>
<h2 id="earthly-cloud-shutdown">Earthly Cloud shutdown</h2>
<p>Earthly Cloud, including Satellites, will stop working on <strong>July 16th, 2025</strong>. If you rely on Satellite functionality and would like to continue getting similar benefits, you can roll out your own <a href="https://docs.earthly.dev/ci-integration/remote-buildkit">remote Buildkit</a>. Our documentation page on <a href="https://docs.earthly.dev/docs/remote-runners">Remote runners</a> explains how they work. Please note that cloud features such as Satellite auto-sleep, Satellite automatic mTLS, shared logs, and cloud secrets will no longer be available.</p>
<h2 id="alternative-dagger">Alternative: Dagger</h2>
<p>Aside from the ongoing community fork, we have arranged with our friends at Dagger to offer a migration path to current Earthly users and customers. Although Dagger is not a drop-in replacement for Earthfiles, there are similarities in the goals of the two projects. In fact, both Earthly and Dagger happen to share Buildkit as an underlying technology.</p>
<p>Dagger has offered to organize a workshop for Earthly users to help evaluate Dagger more easily. Earthly customers also get 1 year for free on Dagger Cloud Team. <a href="https://dagger.io/blog/earthly-to-dagger-migration?utm_campaign=Earthly-Migration&amp;utm_medium=blog&amp;utm_source=earthly-blog">More details in Dagger’s announcement</a>.</p>
<h2 id="whats-next-for-earthly-technologies">What’s next for Earthly Technologies?</h2>
<p>Earthly is our first product. Just like Vagrant didn’t create commercialization potential for Hashicorp despite being wildly successful as an open-source project, Earthly doesn’t have to bring us commercial success all on its own. We are moving forward with developing new products to add to our line. <a href="https://earthly.dev/blog/lunar-launch">We are announcing one such product today</a>.</p>
<p>We know this is not the news you were hoping to hear. For many of you, Earthly has been more than just a tool - it’s been a part of your workflow, your creativity, and your successes. We deeply value every bug report, contribution, feature request, and piece of feedback you’ve shared with us. Without your support, Earthly would not be what it is today.</p>
<p>We hope that this information will help you to plan accordingly. If you have additional questions, please reach out to us at <a href="mailto:support@earthly.dev">support@earthly.dev</a>.</p>
<p>While this chapter of Earthly is coming to a close, we are committed to moving forward and building tools that solve real problems. Thank you for being part of our journey and for continuing to support us through both successes and setbacks.</p>
