---
title: "One canary rule, three systems to reconcile"
url: "https://earthly.dev/blog/one-canary-rule-three-systems/"
date: "2026-09-29"
author: "Kate Gooch"
feed_url: "https://earthly.dev/blog/feed.xml"
---
An engineering standard only works at scale when it reaches every service it applies to, draws on the right evidence, and keeps working as those services change. Take the sample rule: “Every production release of a critical service must use a canary rollout.” A canary setting can pass inspection while the next release skips the canary. The application changes in one repo, rollout configuration lives in another, and the service’s criticality is recorded in a catalog.
