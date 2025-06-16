Title: Starting the Fight – Scraping UFC Data and Launching Optimal Kombat
Date: 2025-06-12
Category: MMA Analytics
Tags: scraping, UFC, MMA
Slug: starting-the-fight
Author: Oscar Kelly
Summary: Intro to Optimal Kombat and scraping workflow.
Status: published

---
Welcome to Optimal Kombat – where we use data to decode the fight game.

This first post is a quick overview of why I started this project, what kind of analysis I'm building, and how you can help shape it.

---

### Who am I?
My name is Oscar, a trading analyst who uses Python in my job and has a passion for sports. I played as a prop in rugby throughout school and uni, but decided that I was done standing around in the rain on a pitch in the middle of winter and wanted to move to a different sport. One I could do year-round and inside, with a lower incidence of injury perhaps... Which is why I picked Brazilian Jiu Jitsu (BJJ)!

While there is still the small but non-zero chance of some pretty devastating injuries, I was immediately hooked onto BJJ after being tapped 8 times in a single 5-minute round by someone half my size - I love learning new things, and there are plenty of techniques and facets to the sport, both in the gi and in no gi.

It also opened me up to the world of martial arts, and exposed me to MMA. Whilst I had heard of and seen MMA before, I had rather naively seen it as, "boxing but more violent and with grappling" up to this point - now, I had a new appreciation for the grappling aspect of the sport: the contrast between the overt violent melee, and the subtle techniques, tactics and strategy creates a fantastic spectator sport.

### What This Blog Is About
I remember watching baseball with my brother one holiday when we were kids, and seeing all of these acronyms: we had no idea what OBP or RBI meant, or why they were worth showing on screen as batters stepped up to the plate. To me, American sports have always had more of a focus on the statistical side of sports, both at a team and a player level, than other sports.

This made me wonder: why *aren't* there stats in other sports?

MMA seems like a good candidate for investigating this: the UFC is a huge promotion, and dominates the MMA sport (some people use the terms "UFC" and "MMA" interchangably when talking about watching the sport!). They collect a vast array of different data during the course of a fight: number of strikes landed vs thrown, takedown attempts, significant strikes landed to the opponent's body, significant strikes landed from the clinch position,... Not to mention, this data is collected at the fight level and at the round level: so, a 5-round fight generates a huge amount of data, and with several fights every event, there are thousands of data points generated every month!

Maybe it's just my ignorance, but I think that this data gets generated, collected,... and largely ignored. What are the implications of this data? Could we look at an incoming fighter and judge how they will perform against a particular opponent? Can we use some of this data to predict if a fight will go the distance or finish early, and how might it finish? Is there a way to evaluate fighters before a fight, to see if one is severely over- or undervalued in terms of betting odds?

### The Purpose of This Blog
Miyamoto Musashi, a Japanese swordsman, strategist and writer, wrote: "When you know the way broadly, you see it in all things". Starting BJJ has made me look at other aspects of my life differently, particularly when looking at learning new things.

I have learned how to code only in the last few years, and already I feel comfortable using it to automate a lot of my work on a day-to-day basis. However, I feel like I have rushed past some things, and neglected to practice other things that I learned, didn't require at the time, and so have forgotten about.

One of the aims of this blog is to help give me a reason to practice these skills, and learn new ones along the way, as well as to put myself out there and try to do something new, no matter how I feel about my chances of succeeding. I'm sure there will be flaws in the analysis I do to begin with, and as time goes on, I may revisit previous articles with better methods and a greater understanding. But this is all part of an effort to improve what I can do, expand my skillset, and apply myself to an area I find exciting.

My overall goal is to use Python to break down fight data, uncover trends, and model fight outcomes and aspects of a fight. This blog will track my journey as I build analytics tools, test predictive models, and explore fighter performance from a data-driven lens.

### What’s Coming
This project is exploratory in nature, so currently there is no defined direction, but here are a few ideas I'm excited to dive into:

- Time series evolution of fighters’ stats - who learns from their mistakes, and who gets left behind
- Fighter style clustering - how does Bruce Buffer know how to describe fighters in his intros before a fight starts?
- Pace & fatigue analysis - do the young bucks have a significant advantage over the veterans?
- Pre-fight modeling & betting implications - can this data be used to shape how fans talk about this sport, shifting away from intangible qualities and towards data-driven insights?

### Give Me Feedback
This is probably premature and a little bit self-indulgent, but in case you do read this and comes back for the articles later on, I’d love to hear your thoughts! What kind of insights are you curious about? Do you want visual breakdowns of matchups? Deeper dives into performance analytics? Tutorials or code walkthroughs? Any ideas, thoughts, comments or feedback (however brutal) would be greatly appreciated!

Comment (coming soon), DM me, or message me [on GitHub](https://github.com/optimal-kombat).

Let’s find patterns in the chaos — together.