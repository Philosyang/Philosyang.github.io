---
title: "Ditching a self-hosted RSS Stack"
date: 2026-03-31
tags: ["slice-of-life"]
---

My X timeline eventually became an endless scroll of illustrations. I was following 2,000+ accounts and the signal-to-noise ratio has completely collapsed. I also wanted to automate checking on paypayfleamarket and mercari query results for some rare albums (hi kairiki bear).

Obviously, I need to spend hours building a self-hosted RSS aggregator on my rasp pi instead of unfollowing people.

---

The stack I landed on was FreshRSS + Nitter, all in docker. The idea was that I could subscribe to accounts like RSS feeds; curated, algorithm-free, served over wg to my devices.

It mostly worked. FreshRSS was very easy to set up. I don't recall any hiccups; Nitter was harder.

Nitter needs a real X session to function. The session creation script gets blocked by X's bot detection at the very last step - dying at "Completing login flow" with a 401. I tried two accounts, both 401'd. X even emailed me to say there was a new login from "ChromeDesktop on Mac", which means the login _worked_, X just refuses to let me extract the session token afterwards.

Ultimately I had to log in through a real browser, manually copy the tokens and auths, and write the session json by hand. This worked, but this will also expire, which means the "maintenance-free" RSS reader now needs maintenance.

---

Youtube's RSS endpoint is obsolete and so unstable that it's completely hit or miss as a coin toss.

For paypayfleamarket, there is no RSS nor API. They use next.js that needs client-side rendering. Yahoo Auctions had native RSS (`&out=rss`) until they removed it years ago.

It was at this step that I'm thinking of giving up this whole RSS thing.

---

I ended up utilizing my second X account and only followed the ones I absolutely need to (so that I don't miss the info - e.g. kaf_info, isekai_info). This works better when integrating a browser-end add-on that can filter out RTs and replies. As for paypayfleamarket and mercari, I might make some scraping scripts or maybe convert the thing into a standalone system (input: item name, process: sqlite + cron job-likes to monitor results changes across major sites, output: endpoints such as telegram bots for notifications); or just check every day.

The RSS concept is nice, but it's too nice that it's hindering businesses.

Not that my blog has RSS support either.
