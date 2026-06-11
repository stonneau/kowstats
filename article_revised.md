# How to choose a scoring system for your tournament? (And why it should not be black jack)
### A data-driven comparison of Northern Kings, Black Jack and their variants

---

## Introduction

<div style="text-align: justify">
What makes a tournament experience successful? There are many aspects to these questions: the venue, the organisation, the tables, food etc.
I would like to tackle the question from the perspective of the actual games played. As a Tournament Organiser (TO), what should you prioritise when designing a pairing and scoring system? Do you want a system that maximises the chances that the best player wins the event? Or would you rather have a system that keeps games as balanced and enjoyable as possible for players of all skill levels? And for that matter, what does it even mean to be "the best player"?

In this article, I try to define and quantify a number of tournament criteria. I then compare several scoring systems built around Northern Kings and Black Jack, including Swiss, hybrid, and pool-based variants, to see how they perform against these criteria.

The goal is not to find the one perfect scoring system. Different tournaments have different objectives. Instead, the aim is to provide TOs with some data and insights that can help them choose the system that best matches the type of event they want to run.

To do this, I use Monte Carlo simulations — which is a fancy way of saying that I let a computer play out thousands of tournaments and record the results. This is equivalent to throwing a lot of dice, which seems appropriate for evaluating a Kings of War pairing system.

The results suggest that, for the criteria considered here, there is little reason to use the Black Jack system as a default. Northern Kings (NK) remains a strong and fairly robust Swiss baseline, especially if you care about giving players balanced games throughout the event, while a pool stage followed by NK is the strongest option if your main goal is raw ranking accuracy rather than balance and simplicity.

We also look at how these findings hold up at a much larger scale, using the Clash of Kings UK 2025 as a case study: 192 players, 6 rounds, with an ELO distribution built from real competitive data. In this case, we show that the Northern Kings scoring system is the most reliable.
</div>

---

## I. How the simulation works

The core idea is simple: generate a group of fictional players with different skill levels, simulate a 32-player, 5-round event under a given system, and record who ends up where. Then repeat that **1,000 times** and average the results. By doing this often enough, we can talk about reliable patterns rather than one lucky run.

**Modelling player skill: the ELO system.**
Player skill is modelled using the [ELO rating system](https://en.wikipedia.org/wiki/ELO_rating_system), the same system used in chess and many other competitive games. You do not need to think of ELO as a perfect truth. Here it is simply a hidden reference point: a way to say that some players are stronger than others before the tournament starts.

**Player distribution.**
Players are drawn from a synthetic but plausible distribution: many players are clustered around average level, some are clearly weaker, and a smaller tail of stronger players reaches up to 2200 ELO. The exact numbers matter less than the overall shape: most players are average, a few are beginners, and a few are much stronger than the pack.

**From ELO to game outcomes.**
An ELO gap does not directly give a Kings of War score. It only gives a rough win probability. The simulation then turns that into a realistic game result: win, draw, or loss, plus a game score that each scoring system interprets in its own way.

---

## II. Scoring and pairing systems

There are 9 tested systems in this comparison. To keep the article readable, it is easier to think of them as three families rather than as 9 completely separate ideas.

### 1. Score-first Swiss systems

These are the most traditional systems in the set.

- **Northern Kings (NK)** uses a score that combines result, scenario, and kill points. That score drives both pairings and final standings.
- **Black Jack (BJ)** also uses a running score, but it reacts more strongly to margin. Bigger wins and heavier losses matter more.

These are the most commonly used systems in the UK, and they both propose  game-specific means to evaluate the ranking of a player additionally to their number of wins, draws and losses. 

### 2. Fairness-first Swiss systems

These systems try to make one principle very clear: if you win more games, you should rank above players who won fewer games.

- **WDL+SOS** uses wins first, then draws, then Strength of Schedule (SOS), for both pairing and final ranking.
- **NK|WDL+SOS** keeps NK-style pairing during the event, but uses wins, draws, and SOS for the final standings.
- **BJ|WDL+SOS** does the same thing starting from BJ pairing.

These systems care less about the exact score of each win and more about simple competitive logic: wins first, then tiebreaks.

### 3. Pool-based systems

These systems change the structure of the event itself. Instead of five straight Swiss rounds, the event starts with three rounds of round-robin pool play in groups of four, then ends with two Swiss rounds.

- **Pool NK** and **Pool BJ** keep score-first standings.
- **Pool NK|WDL+SOS** and **Pool WDL+SOS** are the pool-based fairness-first versions.

Pool formats ask more from the TO, but they also sort the field earlier. As we will see, that extra early sorting can matter a lot.

---

## III. What are we measuring?

All the criteria listed below have been translated into a formula that computes a mark to the outcome of a tournament between **0 to 1, where lower is better**. In plain English, a score of 0.20 means the system gets that question wrong about one time in five.

To see the details of the formulas used, I invite the reader to refer to the notebook where we describe these measures in depth.

### Fairness criteria

- **Wins rank higher**: if Player A wins more games than Player B, does A finish above B?
- **No submariner effect**: is there any benefit to losing early on purpose in order to get easier pairings later?
- **Balanced games**: do players mostly face opponents of similar strength?
- **Tough schedule rewarded**: among players with the same record, does facing stronger opposition help your ranking?
- **No easy-schedule bonus**: among players with the same record, are you protected from being flattered by an easy schedule?

For many events, **Balanced games** may be just as important as identifying the strongest winner. Most players experience a tournament through the quality of the five rounds they actually play, not through the final fight for 1st place.

### Accuracy criteria

- **Champion wins the event**: how often does the strongest player actually finish first?
- **Champion in the top 3**: how often does the strongest player at least finish on the podium?
- **Overall ranking quality**: how well does the full final ranking match the hidden strength of the field?
- **Top 10 ranking quality**: same question, but only for the top end of the table.

The last two criteria use ELO as the hidden benchmark in the background, but you can read them simply as: does the final table look like a sensible ordering of player strength?

---

## IV. Results

### Full results table

The table below is dense. Think of it as a reference sheet: **lower is always better**, and the analysis just below explains the main patterns. One useful way to read it is to compare three priorities: top-table accuracy, fairness of standings, and the balance of games across the room.

To make it easier to scan, <span style="color:#137333; font-weight:600;">green</span> marks the best cluster in each row, while <span style="color:#b3261e; font-weight:600;">red</span> marks a clearly weaker cluster when the gap is large enough to matter.

| Criterion | BJ | NK | WDL+SOS | NK\|WDL+SOS | BJ\|WDL+SOS | Pool NK | Pool NK\|WDL+SOS | Pool BJ | Pool WDL+SOS |
|-----------|----|----|------------|-------------|-------------|---------|-------------------|---------|-----------------|
| Wins rank higher | <span style="color:#b3261e; font-weight:600;">0.295</span> | 0.089 | <span style="color:#137333; font-weight:600;">0.000</span> | <span style="color:#137333; font-weight:600;">0.000</span> | <span style="color:#137333; font-weight:600;">0.000</span> | 0.069 | <span style="color:#137333; font-weight:600;">0.000</span> | <span style="color:#b3261e; font-weight:600;">0.266</span> | <span style="color:#137333; font-weight:600;">0.000</span> |
| No submariner effect | <span style="color:#b3261e; font-weight:600;">0.300</span> | 0.115 | <span style="color:#137333; font-weight:600;">0.019</span> | <span style="color:#137333; font-weight:600;">0.023</span> | <span style="color:#137333; font-weight:600;">0.031</span> | 0.089 | <span style="color:#137333; font-weight:600;">0.028</span> | <span style="color:#b3261e; font-weight:600;">0.271</span> | <span style="color:#137333; font-weight:600;">0.024</span> |
| Balanced games | 0.230 | <span style="color:#137333; font-weight:600;">0.210</span> | 0.233 | <span style="color:#137333; font-weight:600;">0.210</span> | 0.230 | <span style="color:#b3261e; font-weight:600;">0.257</span> | <span style="color:#b3261e; font-weight:600;">0.257</span> | <span style="color:#b3261e; font-weight:600;">0.275</span> | <span style="color:#b3261e; font-weight:600;">0.266</span> |
| No easy-schedule bonus | 0.302 | 0.369 | <span style="color:#137333; font-weight:600;">0.240</span> | 0.294 | <span style="color:#137333; font-weight:600;">0.247</span> | <span style="color:#b3261e; font-weight:600;">0.485</span> | 0.363 | 0.389 | 0.328 |
| Tough schedule rewarded | 0.326 | 0.361 | <span style="color:#137333; font-weight:600;">0.000</span> | <span style="color:#137333; font-weight:600;">0.000</span> | <span style="color:#137333; font-weight:600;">0.000</span> | 0.373 | <span style="color:#137333; font-weight:600;">0.000</span> | 0.330 | <span style="color:#137333; font-weight:600;">0.000</span> |
| Champion wins the event | 0.632 | <span style="color:#137333; font-weight:600;">0.560</span> | 0.647 | 0.661 | <span style="color:#b3261e; font-weight:600;">0.701</span> | <span style="color:#137333; font-weight:600;">0.561</span> | 0.657 | <span style="color:#b3261e; font-weight:600;">0.707</span> | 0.629 |
| Champion in the top 3 | 0.294 | 0.278 | 0.388 | <span style="color:#b3261e; font-weight:600;">0.427</span> | <span style="color:#b3261e; font-weight:600;">0.434</span> | <span style="color:#137333; font-weight:600;">0.185</span> | 0.379 | 0.367 | 0.385 |
| Overall ranking quality | <span style="color:#137333; font-weight:600;">0.189</span> | <span style="color:#137333; font-weight:600;">0.189</span> | 0.239 | 0.253 | <span style="color:#b3261e; font-weight:600;">0.270</span> | <span style="color:#137333; font-weight:600;">0.176</span> | 0.226 | 0.206 | 0.228 |
| Top 10 ranking quality | <span style="color:#137333; font-weight:600;">0.295</span> | <span style="color:#137333; font-weight:600;">0.300</span> | 0.324 | <span style="color:#b3261e; font-weight:600;">0.341</span> | <span style="color:#b3261e; font-weight:600;">0.355</span> | <span style="color:#137333; font-weight:600;">0.286</span> | 0.337 | 0.314 | 0.322 |

### The short version

| If you mainly care about... | Best option | Why |
|-----------------------------|-------------|-----|
| Finding the strongest players as accurately as possible | **Pool NK** | Best full ranking, best top-10 ranking, best top-3 result for the strongest player |
| Giving most players close, enjoyable games | **NK** or **NK\|WDL+SOS** | Best game-balance score in the comparison |
| Keeping a clear wins-first Swiss logic | **WDL+SOS** or **NK|WDL+SOS** | Perfect on wins and SOS, almost no submariner problem |
| A strong default for a normal Swiss event | **NK** | Best simple no-pool baseline, combining top game balance with solid overall results |
| A system I would not recommend as a default | **BJ** | Too many trade-offs, without enough upside to justify them |

### 1. If your goal is to identify the strongest players

This is where **Pool NK** stands out the most clearly.

It has the best full ranking quality in the whole field (**0.176**), the best top-10 ranking quality (**0.286**), and the best top-3 result for the strongest player (**0.185** failure rate, which means the strongest player makes the podium about **81.5%** of the time).

One pattern stands out immediately from the table: the best podium systems are not the fairness-first systems. They are the more accuracy-oriented ones: **Pool NK** leading clearly, and **NK** close behind.

Even here, though, the format still has limits. **Pool NK** does not magically make the best player win every event. Its winner-accuracy cost is **0.561**, essentially tied with **NK** at **0.560**. In plain English, even the best systems only crown the strongest player about **44%** of the time. In a 32-player, 5-round event, luck still matters.

### 2. If your goal is to give most players balanced games

On that criterion, **NK** and **NK|WDL+SOS** are the best systems in the comparison, both at **0.210**. **WDL+SOS** remains reasonably close at **0.233**. The pool systems are clearly worse here: **Pool NK** and **Pool NK|WDL+SOS** both sit at **0.257**, **Pool WDL+SOS** at **0.266**, and **Pool BJ** is worst at **0.275**.

This is an important result, because the price paid by pool formats is not just an abstract statistical trade-off. It shows up directly in the round-by-round experience of the field. If your event is meant to give players a good day of gaming rather than just produce the sharpest possible top table, **NK** and **NK|WDL+SOS** deserve much more weight than a purely winner-focused reading would suggest.

Between the two, **NK** is the simpler recommendation. **NK|WDL+SOS** is the better choice if you want the same best-in-class game balance while also making the final standings more clearly wins-first.

### 3. If your goal is that wins should clearly drive the standings

If this is your top priority, the strongest Swiss answers are **WDL+SOS** and **NK|WDL+SOS**.

Both are perfect on **wins rank higher** and **strength of schedule**. Both almost eliminate the submariner problem, at **0.019** and **0.023**. Both are also much easier to explain to players: win more, rank higher; if records are equal, use schedule strength.

Between the two, **WDL+SOS** is the cleaner fairness package overall. It is better at protecting players from easy-schedule inflation (**0.240** vs **0.294**), slightly better on overall ranking quality (**0.239** vs **0.253**), and slightly better on winner and podium accuracy.

**NK|WDL+SOS** has one important strength, though: it keeps the best game-balance score among the fairness-first Swiss systems, tied with **NK** at **0.210**. So if you want cleaner final standings without losing the general feel of NK pairings during the event, it is the most natural adaptation.

### 4. What pool systems really add

The big upside of pools is faster sorting. After three rounds inside small groups, the event already knows much more about who belongs near the top. That is the main reason **Pool NK** is the best raw-accuracy package in the entire comparison.

The downside is equally clear. Pool systems create less balanced games overall. **Pool NK** scores **0.257** on game balance against **0.210** for **NK**, and **Pool BJ** is worst at **0.275**. **Pool NK** is also poor at avoiding an easy-schedule bonus (**0.485**) and weak on **strength of schedule** (**0.373**).

In plain English: pool formats help you sort the top of the field, but they do a worse job of making the whole event feel evenly paired and structurally fair. That is the trade-off at the heart of this comparison.

There is also the practical side. Pools mean more work for the TO. So **Pool NK** is not the universal answer. It is the answer if your event cares a lot about sharpening the top table and you are willing to pay the organisational cost.

### 5. Northern Kings remains the best simple Swiss baseline

Once pools are taken out of the picture, **NK** is still the most convincing all-round default.

It ties **BJ** on full ranking quality (**0.189**), but beats it clearly on the questions most players actually notice: **wins rank higher** (**0.089** vs **0.295**), **submariners** (**0.115** vs **0.300**), **games balance** (**0.210** vs **0.230**), **winner accuracy** (**0.560** vs **0.632**), and **top-3 accuracy** (**0.278** vs **0.294**).

In practice, that makes NK the safest recommendation for a normal Swiss event if you want strong pairings across the room and do not want either pool logistics or a full wins-first redesign.

### 6. Black Jack and the odd hybrids

**Black Jack** is not catastrophic at everything. It is a bit better than NK at avoiding easy-schedule inflation and slightly less bad on **strength of schedule**. But those are not enough to offset how much worse it is on wins logic, submariners, game balance, and champion-finding.

That is the recurring pattern in these results: BJ can look respectable on one or two secondary metrics, but it loses too often on the questions that most TOs and players care about first.

The BJ-based variants do not really rescue the picture. **Pool BJ** adds even worse pairing balance and does not lead any major criterion. **BJ|WDL+SOS** fixes the wins-first problem, but **WDL+SOS** and **NK|WDL+SOS** are cleaner fairness-first options.

### Three systems to consider as a conclusion

Three systems stand out when looking across all criteria together.

**I. Pool NK — best for accuracy**

The clearest leader on raw ranking quality. It has the best full ranking (**0.176**), the best top-10 (**0.286**), and the best chance of keeping the strongest player on the podium (**81.5%** top-3 success). The pool phase does the work early, and the Swiss rounds sharpen the top table further.

The price is real: worst game balance in the set (**0.257** vs **0.210** for NK), poor protection against easy-schedule inflation (**0.485**), and wins do not fully drive standings (**0.069**). Add to that the extra organisational work of running pool groups. Pool NK is the right answer if accuracy is your primary goal and you are willing to absorb those costs.

**II. NK — best all-round Swiss default**

The most convincing no-pool option. NK ties BJ on full ranking quality (**0.189**) but beats every other pure Swiss system on most of the questions players and TOs actually care about: best game balance (**0.210**), best winner accuracy among Swiss systems (**0.560**), and cleaner results on wins and submariners. It is also the simplest system to explain and run.

Its weaknesses are real but moderate: it does not guarantee wins drive standings (**0.089**), the submariner effect is present (**0.115**), and there is no structural tiebreak for schedule strength. For most events, those are acceptable trade-offs.

**I. NK|WDL+SOS — best for fairness**

The strongest option if you want the final standings to clearly reflect competitive results. Perfect on wins rank higher (**0.000**) and schedule strength (**0.000**), near-zero submariner effect (**0.023**), and tied with NK for best game balance (**0.210**). It keeps NK-style pairings during the event, so the feel in the room does not change — only the final tiebreak logic does.

The cost is accuracy: elo distance rises to **0.253** compared to **0.189** for NK, and the top-3 failure rate for the champion is notably higher (**0.427** vs **0.278**). If identifying the strongest players with precision is the main goal, NK|WDL+SOS is not the right tool.

*Worth knowing: if you want pool structure but fairness-first standings, **Pool NK|WDL+SOS** sits cleanly between these two worlds — better accuracy than NK|WDL+SOS (**0.226** elo distance), perfect on wins and schedule strength, and less damaging on easy-schedule inflation than Pool NK (**0.363** vs **0.485**). The game balance penalty of pool formats still applies, but it is the most balanced pool option in the set.*

---

## V. Clash of Kings: 192 players, 6 rounds - Nothern Kings wins by far!

The 32-player, 5-round baseline covers the most common tournament format. But some events are structurally different. The Clash of Kings UK is one of the largest Kings of War events in the world: the 2025 edition attracted 194 players across 6 rounds. At that scale, the same questions take on a different shape. 

**The scale problem.** With 192 (we rounded down to faciliate testing the pool configuration) players and 6 rounds, each player faces 6 opponents out of a possible 191 — about 3% of the field. Even the strongest player has very little room to demonstrate their edge. No scoring system can fully compensate for that: the champion wins the event less than 30% of the time under any system tested.

**Building the player pool.** Rather than a synthetic ELO distribution, we matched the 194 CoK UK 2025 participants against the European KoW ELO database published at *kingsofwarmasters.fr*. Players not found in the database were assigned estimated ratings. A kernel density estimate of the resulting distribution was used to resample 192-player fields for each simulation. The pool format was adjusted to 3+3: three pool rounds then three Swiss rounds, for a total of 6 — matching the Swiss format.

### What changes at 192 players

The overall structure of results is unchanged: fairness-first systems remain perfect on wins and schedule strength, score-first systems lead on ranking accuracy, BJ remains the worst choice for wins logic. Three differences stand out.

**Games balance improves everywhere.** With 192 players available at each score level, Swiss pairings become much more precise. NK drops from **0.210** to **0.165**, Pool NK from **0.257** to **0.185**. The gap between Swiss and pool formats also narrows significantly.

**Pool NK regains its full-ranking accuracy advantage** (**0.214** vs NK's **0.231**). The early sorting from the pool phase pays off across the whole field. However, Pool NK no longer leads on top-3 accuracy: NK is better here (**0.500** vs **0.554**). At this scale, three pool rounds are not enough additional information to guarantee the strongest player reaches the podium.

**Fairness-first systems become very costly.** At 32 players, NK|WDL+SOS had a top-3 failure rate of **0.427** — worse than NK but tolerable. At 192 players, it rises to **0.756**. WDL+SOS reaches **0.874** on winner accuracy: the strongest player wins the event only about **13%** of the time. If ranking accuracy matters at all in a large competitive event, the fairness-first accuracy cost is hard to justify.

### What to use for a large-format event

**NK is the clearest all-round recommendation.** Best podium accuracy (**0.500** top-3 failure rate), best game balance of any Swiss system (**0.165**), and solid full-ranking quality (**0.231**). Its simplicity is also an asset when managing 192 players over 6 rounds.

**Pool NK is worth considering if full-field ranking accuracy is the priority** and you have the infrastructure to run 48 pools. It leads on elo distance (**0.214**) but does not improve the podium question, and the organisational cost is significant.

**Fairness-first systems are a poor fit for large competitive events.** NK|WDL+SOS remains defensible if player trust in the standings is the priority — but WDL+SOS, BJ|WDL+SOS, and their pool equivalents carry accuracy costs at this scale that are hard to justify for a flagship event.

---

## VI. Conclusion

There is no perfect scoring system. But the current results do point to a clearer set of recommendations.

**If your main goal is to maximise the quality and balance of games across the room, start from NK or NK|WDL+SOS.** NK is the simpler choice. NK|WDL+SOS is the better option if you want that same strong pairing quality while making the final standings more explicitly wins-first.

**If your main goal is raw accuracy, use Pool NK.** It gives the best full ranking, the best top-10 ranking, and the best chance of keeping the strongest player on the podium. The price is real: rougher pairings, weaker fairness on schedule-related questions, and extra organisational work.

**If your main goal is that wins should clearly drive the standings, use WDL+SOS or NK|WDL+SOS.** WDL+SOS is the cleaner fairness model on paper. NK|WDL+SOS is the easier choice if you want to keep more of the NK feel during the event.

**There is still little reason to choose Black Jack as a default.** Its trade-offs are too often the wrong ones.

For very large formats such as Clash Of Kings, it seems that Northern Kings is the clear choice.

And one final point remains true whatever system you choose: **a 32-player, 5-round event cannot fully separate skill from variance**. The scoring system matters, but the limits of the format matter too.

---

*Sections I–IV based on 1,000 Monte Carlo simulations of 32-player, 5-round tournaments. Section V uses 500 simulations of 192-player, 6-round events (3+3 pool format) with an ELO distribution derived from the CoK UK 2025 player list.*
