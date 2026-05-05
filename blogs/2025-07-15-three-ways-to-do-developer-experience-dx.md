---
title: "Three Ways to Do Developer Experience (DX)"
url: "https://earthly.dev/blog/dx-three-ways/"
date: "2025-07-15T00:00:00-04:00"
author: "Adam Gordon Bell"
feed_url: "https://earthly.dev/blog/feed.xml"
---
<p>Think of Developer Experience, or DX, as user experience but for developers. Instead of making things easier for the everyday user, DX is about making a developer’s life easier when working with tools, libraries, and platforms.</p>
<h2 id="who-should-care-about-developer-experience">Who Should Care About Developer Experience?</h2>
<p>Okay, we’ve got a definition. But who cares about DX? Why does it matter? Let’s skip the jargon and consider three scenarios where DX is crucial.</p>
<div class="align-right">
<figure>
<img alt="" src="https://earthly.dev/.netlify/images?url=/blog/assets/images/dx-three-ways/9740.png" /><figcaption>An important moment in DX.</figcaption>
</figure>
</div>
<p>Three types of people might care about developer experience. Their jobs are different, so their views on DX might vary. Let’s meet Alice, Bob, and Carlos.</p>
<h2 id="dx-awakening">DX Awakening</h2>
<h3 id="alice---product-based-developer-experience">Alice - Product-Based Developer Experience</h3>
<div class="align-left">
<img alt="Alice - Product Manager" height="200" src="https://earthly.dev/.netlify/images?url=/blog/assets/images/dx-three-ways/0590.png" width="200" />
<figcaption>
Alice - Product Manager
</figcaption>
</div>
<p>Alice is a Product Manager at Request Express, a developer tool for API development. Developer experience is critical for her because Request Express’s customers are all developers.</p>
<p>To her, everything about Developer Experience leads back to Stripe. Stripe, a billion-dollar success, was built on a simple observation: the developer experience for payment processing was horrible, and they could do better.</p>
<p>Alice can’t stop talking about Stripe. She loves their clear instructions, reusable code, and easy start-up. Stripe showed everyone the value of making things easy for developers.</p>
<p>Alice took a page from Stripe’s book, modeling Request Express’s new features after their developer-centric approach. She and her team created interactive documentation with embedded code samples inspired by Stripe’s docs. And she led a redesign of Request Express’s onboarding flow to simplify the initial integration steps that had been pain points for developers.</p>
<h3 id="bob---internal-platform-developer-experience">Bob - Internal Platform Developer Experience</h3>
<div class="align-right">
<img alt="Bob - Internal Tools Lead" height="200" src="https://earthly.dev/.netlify/images?url=/blog/assets/images/dx-three-ways/0970.png" width="200" />
<figcaption>
Bob - Internal Tools Lead
</figcaption>
</div>
<p>Bob is a staff software engineer at Shop-O-Rama. He works on internal tools and platforms used by Shop-o-rama’s engineering teams. His job: make their work easier and more productive.</p>
<p>Bob’s wake-up call? Failure. His team built this dashboard system at Shop-o-rama called ‘Dash-forge’. Bob thought it was powerful, a game changer. But no one used it. Not without a fight.</p>
<p>He could have forced it. He’d seen it before. Top-down mandates, standardizing internal tools, causing friction. Developers forced to use tools they hated. He knew that wasn’t the way. So he changed his approach. Started acting like a product manager. Treating internal tools and APIs as a product. Those other teams were his customers.</p>
<p>His product solved a genuine problem, but no one could use it. Or at least the usability was terrible enough to outweigh any potential benefits.</p>
<p>For Bob, DX is about being selective. He doesn’t have the resources of a developer tools company. But he can make sure he’s building with his users in mind. Now, things like documentation, user testing, and support are part of the product development process.</p>
<h3 id="carlos---organizational-developer-experience">Carlos - Organizational Developer Experience</h3>
<div class="align-left">
<img alt="Carlos - Director of Engineering" height="200" src="https://earthly.dev/.netlify/images?url=/blog/assets/images/dx-three-ways/1020.png" width="200" />
<figcaption>
Carlos - Director of Engineering
</figcaption>
</div>
<p>Meet Carlos. He’s the Director of Engineering at a fast-growing ML startup. But he’s got a problem. Carlos faces onboarding and team productivity challenges as the engineering team has grown from 10 to 100 developers.</p>
<p>Quick hiring means training new developers is tricky. Getting them the right environment, tools, and documentation to start contributing was even tougher. Just when things need to speed up, they’re slowing down.</p>
<p>The ballooning team size has also introduced friction into development workflows. More developers, more confusion. Work’s getting duplicated. Carlos sees it. He knows they need a team focused on smoothing things out if this startup wants to keep growing.</p>
<h2 id="dx-metrics">DX Metrics</h2>
<p>So for Alice, Bob, and Carlos, the tactics employed to improve the developer experience will vary. They’re all about improving how developers interact with code, tools, and resources. Every interaction matters. But what Alice, Bob, and Carlos focus on? That’s where they differ.</p>
<p>For Alice, DX might focus on these key elements of her company’s API and CLI tool:</p>
<ul>
<li><strong>Intuitive, well-documented APIs</strong>. Easy discovery of API contracts.</li>
<li><strong>Helper libraries</strong> and sample code accelerate building.</li>
<li><strong>Extensive and intuitive documentation</strong></li>
<li><strong>Excellent technical support</strong> resources like chat and issue tracking, community management, and support.</li>
<li><strong>Dashboards</strong> to provide visibility into API usage, performance, and errors.</li>
<li><strong>Release notes</strong>, deprecation schedules, and migration guides help developers stay current with the product.</li>
</ul>
<p>For Alice, key metrics to watch might include:</p>
<ul>
<li><strong>Onboarding Duration</strong> - How long it takes new developers to use her product successfully.</li>
<li><strong>Documentation Hit Rate / Findability</strong>: This is how developers find and access documentation.</li>
<li><strong>Support Ticket Frequency</strong>: How often do developers need to contact you for help?</li>
</ul>
<p>Carlos doesn’t have the luxury of focusing on just one tool - he has to think of the whole experience of developers at his company. Key elements of DX for him include:</p>
<ul>
<li><strong>Standardizing tools and technologies</strong> to reduce complexity. This minimizes the learning burden as developers learn new systems.</li>
<li><strong>Good collaboration practices</strong> via knowledge-sharing platforms and open communication to prevent duplicate efforts.</li>
<li><strong>Documentation</strong> of key procedures and processes to help with onboarding</li>
<li><strong>Continuous delivery pipelines</strong> and test automation so developers can ship faster with confidence.</li>
</ul>
<p>For Carlos, key metrics might include:</p>
<ul>
<li><strong>Onboarding Duration</strong> - How long it takes new developers to make their first successful code contribution.</li>
<li><strong>Time To First Commit</strong> - Time from cloning repo to having a local commit ready. Includes time for getting dependencies, setting up the environment, and making a superficial change.</li>
<li><strong>Build Time</strong> - The time required to complete a code build in CI. Includes build queue wait time, if any.</li>
<li><strong>PR Turn Around Time</strong>: The total duration from submitting a PR until it’s finally approved.</li>
</ul>
<p>Bob’s worries are a mix. He’s got Carlos’ concerns about developers in his Org. And he’s got Alice’s concerns about the tools he owns.</p>
<p>Regardless of the use case, though, there is no perfect metric for measuring DX improvements. Instead, whether your situation is closer to Alice, Bob, or Carlos, you should center your efforts around developer satisfaction and frustration. The least scalable but highest payoff way to do this is field testing.</p>
<h2 id="field-testing">Field Testing</h2>
<p>Field testing is observing developers using your tools, libraries, APIs, or frameworks in their natural working environment. You want to see how they handle real-world scenarios, what problems they hit, and how they get around them.</p>
<p>Alice, at Request Express, has the most rigorous field testing process, but even so, the process is relatively simple. She recruits developers, ones who’ve never used her product before.</p>
<p>( She started with just a few friends from a former company. As time went on, she moved on to friends of colleagues. Lately, she’s even reached out to a local coding bootcamp graduating class. )</p>
<p>Each volunteer gets on a video call with Alice and is given a task to complete using their chosen development environment. The task is always some variation of working through Request Express’s onboarding tutorial.</p>
<h2 id="field-testing-analysis">Field Testing Analysis</h2>
<p>The first field test Alice did is hard to forget. The user was confused and lost at step one of the tutorial. He would have never even made it to step two without a nudge from her. That testing led to some tutorial changes and error message cleanup, and then field testing flowed more smoothly.</p>
<p>For Alice, analysis of the field testing results is a breeze. Every new volunteer finds something. A confusion point, a missing usage pattern, or just a rough edge. The hundred-dollar gift cards she hands out at the end are the best money her company has ever spent.</p>
<h2 id="internal-field-testing">Internal Field Testing</h2>
<p>Bob’s approach to field testing has been different. He temporarily joined a team looking to use Dash-forge and did the integration himself. It went badly, and for every papercut or roadblock he hit, he documented it and got his team to prioritize a resolution.</p>
<p>After that integration, he paired with the dev. He took a backseat, but still spotted limitations. Now, several quarters later, teams are using dash-forge with ease.</p>
<h2 id="aggregate-feedback">Aggregate Feedback</h2>
<p>Carlos did things differently. He started with anonymous surveys. What was preventing you from getting your job done? What’s frustrating you? New hires made daily lists of problems. Carlos took this data, cleaned it up, summarized it, and took it to a focus group of trusted devs.</p>
<p>He came out of this with a list. Improvements the organization needed to prioritize. Build speed had to go up. Red tape had to go. Cross-team collaboration had to be strongly encouraged. Then there was the implementation work: A new docs system based on markdown, a backstage implementation, and a new role, all about onboarding and training improvements.</p>
<p>Six months later, the anonymous developer survey looked a lot better. Another six months, and the engineering org was moving faster than ever.</p>
<h2 id="conclusion">Conclusion</h2>
<p>So there you go. Developer Experience is not just a trendy new term but a fundamental pillar of success in modern software development. Alice, Carlos, and Bob underscore its wide-ranging impact.</p>
<ul>
<li>For <strong>Alice</strong>, embracing DX, focusing on clear instructions and easy start-up, transformed her product. It became more user-friendly and popular.</li>
<li><strong>Bob</strong> really embraced DX in his tool building. He turned a tool that was barely used into something everyone loved by listening to what his users needed.</li>
<li>Meanwhile, <strong>Carlos</strong> used DX improvements handle fast growth. He listened to feedback, made changes, and sped up work.</li>
</ul>
<p>From public-facing APIs to internal tools and across entire organizations, DX means asking how easy our tools are to use. Testing these tools, getting feedback, that’s how we find problems and fix them. It’s how we keep developers happy and successful. It’s how we drive adoption, nurture loyalty, and fosters success.</p>
<p>Are there tools or apps you use that could be improved?</p>
<p>DX can turn a tool from ignored to essential, boost a struggling product, and make a growing team run smoothly. Whether you’re an Alice, a Bob, or a Carlos, improving DX is key. It ensures developer satisfaction and your organization’s success. And if you’re looking to improve your Developer Experience, check out <a href="https://earthly.dev/earthfile/">Earthly</a>. It’s a tool designed to simplify and speed up builds and accelerate development workflows.</p>
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
