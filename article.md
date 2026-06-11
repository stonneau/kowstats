# How to choose a scoring system system for your tournament?
### A data-driven comparison of Northern Kings, Black Jack and their variants

---

## Introduction

<div style="text-align: justify">
What makes a tournament experience successful? There are many aspects to these questions: the venue, the organisation, the tables, food etc.
I would like to tackle the question from the perspective of the actual games. As a Tournament Organiser (TO), what should you prioritise when designing a pairing and scoring system? Do you want a system that maximises the chances that the best player wins the event? Or would you rather have a system that keeps games as balanced and enjoyable as possible for players of all skill levels? And for that matter, what does it even mean to be "the best player"?

In this article, I try to define and quantify a number of tournament criteria. I then compare two scoring systems, Northern Kings and Black Jack, to see how they perform against these criteria. I also study how small variations of these systems can affect the overall tournament experience.

The goal is not to find the one perfect scoring system. Different tournaments have different objectives. Instead, the aim is to provide TOs with some data and insights that can help them choose the system that best matches the type of event they want to run.

To do this, I use Monte Carlo simulations — which is a fancy way of saying that I let a computer play out thousands of tournaments and record the results. This is equivalent to throwing a lot of dice, which seems appropriate for evaluating a kings of war pairing system!

The results suggest that, for the criteria considered here, there is little reason to use the Black Jack system, as it tends to perform worse in most situations. The Northern Kings system appears fairly robust, although no scoring system proves capable of consistently identifying and ranking the strongest players perfectly.
</div>

---

## I. How the simulation works

The core idea is simple: generate a group of fictional players with different skill levels, simulate a 32-player, 5-round Swiss tournament under a given scoring system, and record who ends up where. Then repeat 1,000 times and average the results. By running enough simulations, the patterns we see are reliable rather than just lucky.

**Modelling player skill: the ELO system.**
Player skill is modelled using the [ELO rating system](https://en.wikipedia.org/wiki/Elo_rating_system), the same system used in chess and many other competitive games. ELO is a simple but powerful way to express the probability that one player will beat another. For example, if Player A has an ELO of 1800 and Player B has an ELO of 1400, Player A will win roughly 9 games in 10 — not all of them, because anything can happen on the day.

**Player distribution.**
Players are drawn from a realistic synthetic distribution: a few beginners around ELO 1300, a large cluster of average players around 1400, and a small number of experienced players up to 1900. This is designed to resemble a typical regional or national event. An ELO of 1000 would be a complete beginner, your local club champion would be around 1800–2000, and a national master around 2200.

**From ELO to game outcomes.**
The ELO probability tells us who wins or loses, but a Kings of War game has more to it than that: draws, scenario points, kill points. An empirical lookup table converts the ELO probability into a win, draw, or loss result and a normalised "margin of victory" score, which each scoring system then interprets in its own way. Two equally-matched players (ELO 1400 vs 1400) have roughly a 40% chance of a win, 20% chance of a draw, and 40% chance of a loss — which seems reasonable as a baseline.

**An important note on fairness.**
Crucially, all five scoring systems are evaluated on exactly the same set of pre-generated game results. The only variable is how those results are translated into scores and rankings. This makes the comparison as fair as possible.

---

## II. Scoring and pairing systems

### Northern Kings (NK)

The Northern Kings scoring system awards **15 points for a win, 10 for a draw, 5 for a loss**, plus scenario points (which vary by mission, typically 1–7 for the winner) and kill points (0–5 based on casualties inflicted). The cumulative total determines both the pairing for each round and the final ranking.

### Black Jack (BJ)

In the Black Jack system, both players' scores are calculated **relative to each other**: the winner earns a base of 14 points plus bonuses based on how large the scenario and kill point margins were; the loser earns a base of 7 minus those same margins. Both players' final scores therefore depend heavily on the margin of victory, not just the result. Like NK, the cumulative total determines round-by-round pairing and the final ranking.

### A hybrid approach: using Strength of Schedule

A key insight is that the system used **during** a tournament — for pairing players against each other each round — can be different from the system used to determine the **final standings**. A TO can keep the pairing process familiar while applying a fairer tiebreaker at the end.

The tiebreaker used in the three hybrid variants tested here is **Strength of Schedule (SOS)**, borrowed from chess. Once two players have the same number of wins, the one who faced tougher opponents (measured by their opponents' overall win records) ranks higher. This rewards players who earned their record against harder competition.

The three variants are:

- **NK Hybrid** — NK scoring and pairing during the event, but the **final ranking** is determined by: most wins first → most draws → strongest schedule (SOS).
- **BJ Hybrid** — BJ scoring and pairing during the event, same SOS-based final ranking as NK Hybrid.
- **Wins+SOS** — wins first → draws → SOS used for **both pairing and final ranking** throughout the event, with equal weight given to each round.

> *Pool-based formats (3 rounds of round-robin within small groups, followed by 2 Swiss rounds) were also explored. They are not covered in this article, as they introduce meaningful extra organisational overhead for the TO and their advantages on accuracy do not outweigh the disadvantages on game balance.*

---

## III. What are we measuring?

All values in the tables below run from **0 to 1, where lower is always better**. A score of 0 is perfect; a score of 1 is as bad as possible. Think of each score as "how often does this system get it wrong" — 0.00 means never, 0.50 means half the time.

### Fairness criteria

These measure whether the tournament treats players equitably — regardless of their final placement.

| Criterion | What it measures |
|-----------|-----------------|
| **Wins rank higher** | If Player A has more wins than Player B, does A always rank higher? A score of 0 means yes, always. A higher score means players with fewer wins are sometimes ranked above players with more wins. |
| **No submariner effect** | Could a player benefit by deliberately losing their first game, to get easier opponents for the rest of the event and rack up big point margins? A low score means the system discourages this. |
| **Balanced games** | Are players mostly playing opponents of similar strength throughout the event? A low score means games are well-matched. |
| **Tough schedule rewarded** | Among players with the same win/draw record, does the one who faced harder opponents rank higher? |
| **No weak-schedule boost** | Among players with the same win count, is having faced weaker opponents a disadvantage rather than a boost? |

### Accuracy criteria

These measure whether the tournament reliably identifies and ranks the strongest players.

| Criterion | What it measures |
|-----------|-----------------|
| **Champion wins the event** | How often does the strongest player (highest ELO) finish 1st? Lower = they win more reliably. |
| **Champion in the top 3** | How often is the strongest player somewhere in the top 3 at the end? Lower = they place highly more reliably. |
| **Overall ranking quality** | How well does the full final ranking reflect player strength from top to bottom? |
| **Top 10 ranking quality** | Same as above, but looking only at the top 10 positions. |

### An open question: should bigger wins mean a better rank?

| Criterion | What it measures |
|-----------|-----------------|
| **Bigger win rewarded** | Among players with the same win count, does the one who won more dominantly rank higher? |

This criterion deserves a note. There are reasonable arguments both ways. Some feel that **a win is a win**, regardless of margin, and that rewarding larger margins may unfairly penalise armies that naturally score fewer kill points or scenario points. Others argue that the **margin of victory is a genuine signal of player skill** and should count for something when wins are equal. The results below are presented without a recommendation on this point — it is ultimately a design choice for the TO.

---

## IV. Results

### Summary scorecard

The table below shows how each system performs across all ten criteria. Read each column top-to-bottom to get a feel for a system's strengths and weaknesses.

> 🟢 best &nbsp; 🟡 good &nbsp; 🟠 mixed &nbsp; 🔴 poor

| Criterion | Black Jack | Northern Kings | Wins+SOS | NK Hybrid | BJ Hybrid |
|-----------|:----------:|:--------------:|:--------:|:---------:|:---------:|
| **Wins rank higher** | 🔴 0.32 | 🟡 0.10 | 🟢 0.00 | 🟢 0.00 | 🟢 0.00 |
| **No submariner effect** | 🔴 0.33 | 🟠 0.12 | 🟢 0.02 | 🟢 0.02 | 🟢 0.03 |
| **Balanced games** | 🟡 0.25 | 🟢 0.24 | 🟡 0.26 | 🟢 0.24 | 🟡 0.25 |
| **Tough schedule rewarded** | 🔴 0.34 | 🔴 0.37 | 🟢 0.00 | 🟢 0.00 | 🟢 0.00 |
| **No weak-schedule boost** | 🟡 0.31 | 🔴 0.39 | 🟢 0.27 | 🟡 0.32 | 🟡 0.28 |
| **Champion wins the event** | 🟡 0.74 | 🟢 0.73 | 🔴 0.81 | 🔴 0.81 | 🔴 0.80 |
| **Champion in the top 3** | 🔴 0.56 | 🔴 0.53 | 🟠 0.43 | 🟢 0.38 | 🟠 0.41 |
| **Overall ranking quality** | 🟢 0.21 | 🟢 0.21 | 🟠 0.27 | 🟠 0.28 | 🟠 0.30 |
| **Top 10 ranking quality** | 🟢 0.33 | 🟡 0.34 | 🟠 0.36 | 🟠 0.37 | 🔴 0.39 |
| **Bigger win rewarded** *(see note)* | 🟡 0.25 | 🟢 0.16 | 🔴 0.41 | 🟠 0.34 | 🟠 0.34 |

---

### Does the player with the most wins rank highest?

This is the most fundamental fairness question a scoring system has to answer. **Wins+SOS, NK Hybrid, and BJ Hybrid all score a perfect 0.00** — by design, the player with more wins always ranks above the one with fewer. Northern Kings comes close (0.10), meaning roughly 1 in 10 comparisons produces an "inverted" ranking where a player with fewer wins sits above a player with more. **Black Jack scores 0.32**: in almost one third of pairwise comparisons, the player with fewer wins ranks higher. For any event where players expect "winning more games = finishing higher", BJ is the wrong system.

---

### The submariner problem

Could a player deliberately lose their first game in order to face weaker opponents for rounds 2 to 5 and accumulate large point margins? **In BJ, the answer is clearly yes (0.33).** A player who tanks round 1 will spend the rest of the event beating players well below their level for maximum points. NK has a noticeable but smaller version of the same problem (0.12). All three SOS-based systems virtually eliminate the incentive (0.02–0.03), because a loss in round 1 directly drops your rank based on win count and no amount of subsequent large margins can compensate. For any competitive event, BJ's submariner problem should be taken seriously.

---

### Are the games well-matched?

This is where all five systems are closest to each other. **NK and NK Hybrid share the best result (0.24)**, with BJ and BJ Hybrid just behind (0.25) and Wins+SOS slightly further (0.26). The differences are small enough that no system has a decisive advantage here. All five do a reasonable job of matching players against opponents of similar strength from round 2 onwards — the first round is always random, which limits how well any Swiss format can do on this criterion.

---

### Does facing tough opponents pay off?

These two criteria go together: if you happened to face stronger opponents, should your ranking reflect that?

For **tough schedule rewarded**: Wins+SOS, NK Hybrid, and BJ Hybrid achieve a perfect score (0.00) by construction — SOS is their explicit tiebreaker, so a harder schedule always helps within the same win count. BJ (0.34) and NK (0.37) both completely ignore schedule strength in their ranking formula; within any win-count group, the difficulty of your opponents is irrelevant.

For **no weak-schedule boost**: Wins+SOS (0.27) and BJ Hybrid (0.28) are the best. **NK is notably the weakest here (0.39)** — NK scoring actively rewards players who faced weaker opposition, because bigger wins against weaker players still produce large point totals that boost the final ranking.

---

### Does the strongest player win the event?

This is arguably the headline question. The honest answer across all five systems is sobering: **even the best system correctly identifies the champion barely one tournament in four**.

| System | % of events where the strongest player finishes 1st |
|--------|-------------------------------------------------------|
| Northern Kings | **27.5%** |
| Black Jack | 26.1% |
| BJ Hybrid | 19.6% |
| Wins+SOS | 18.8% |
| NK Hybrid | 18.8% |

NK and BJ are the best here. The SOS variants pay a real cost — switching to a WDL+SOS final ranking drops the success rate from ~27% to ~19%. This is the core trade-off: fairness and accuracy pull in opposite directions.

It is worth stressing that even the best result (27.5% for NK) is low in absolute terms. **This is not a failure of the scoring system — it is a fundamental property of a 5-round Swiss tournament with 32 players.** With 5 rounds, a single bad game can derail the strongest player's event, regardless of how scores are counted.

---

### Is the strongest player at least in the top 3?

This is where the results take a striking turn. **The systems that are worst at finding the exact champion are the best at keeping the strongest player somewhere in the top 3.**

| System | % of events where the strongest player is in the top 3 |
|--------|-------------------------------------------------------|
| NK Hybrid | **61.9%** |
| BJ Hybrid | 59.0% |
| Wins+SOS | 57.1% |
| Northern Kings | 46.8% |
| Black Jack | 44.1% |

NK Hybrid keeps the best player in the top 3 almost two events in three, compared to less than half the time for NK or BJ. The reason: when a strong player has one bad game, a WDL-priority system keeps them near the top based on their win count and schedule quality — they lose the chance of being #1, but they remain visible at the top of the table. In a score-based system, one bad game can push a strong player well below a cluster of players with similar scores but weaker records.

For many TOs, this is a more meaningful criterion than "does the best player finish exactly first" — a strong result is still a strong result if the best player finishes 2nd or 3rd.

---

### Overall ranking quality

For the full-field ranking, **BJ and NK are tied best (0.21)**, with the SOS variants notably worse (0.27–0.30). For the top 10 specifically, BJ (0.33) and NK (0.34) again lead. The differences in this range are small — none of the five systems can accurately rank the top of the field because 5 rounds simply isn't enough data. Adding SOS to the final ranking makes this slightly worse, which is the price of the fairness gains.

---

### Bigger wins, better rank?

NK is the strongest here (0.16), which makes sense: scenario points and kill points directly reflect how dominant a performance was, and NK scores both into the cumulative total. BJ (0.25) also captures margin of victory, though less strongly. The three SOS variants score between 0.34 and 0.41, reflecting the fact that SOS ranking within win-count groups ignores actual point margins entirely. Whether this matters is, as noted, a question of TO philosophy.

---

## V. Conclusion

There is no perfect scoring system. But the data does allow some clear conclusions.

**If your primary goal is a fair event where wins always matter**, use **NK Hybrid** (or Wins+SOS). Both guarantee that the player with more wins always ranks higher, virtually eliminate the submariner incentive, and ensure that facing a harder schedule is rewarded. NK Hybrid also gives the strongest chance of having the best player finish in the top 3 (61.9%). The trade-off is a lower chance of the exact champion finishing first (18.8% vs 27.5% for NK).

**If your primary goal is to crown the strongest player**, use **Northern Kings**. It is the best of the five Swiss systems at identifying the winner, and its in-tournament pairing produces the most balanced games. Be aware that it still only succeeds about one event in four, and that it has a real submariner problem (12% of the time, losing early pays off) and does not reward facing a harder schedule.

**There is no good reason to use Black Jack.** BJ is the worst system on every fairness criterion — wins ranking, the submariner effect, and schedule strength — and is not better than NK on any accuracy criterion. If you currently use BJ and want to keep familiar pairing dynamics, **BJ Hybrid** preserves the BJ pairing experience while completely fixing all three fairness problems. But NK Hybrid offers the same fairness guarantees with better game balance and is the cleaner choice.

**The fundamental trade-off cannot be engineered away.** Any system that prioritises fairness will spread the final ranking more evenly, which reduces the chance of the strongest player finishing exactly first. With 32 players and 5 rounds of Swiss, the format simply cannot separate skill from luck completely — the choice of scoring system shapes *how* results are distributed, not whether luck matters. For shorter, more competitive events, that may be the honest message to share with your players.

---

*Based on 1,000 Monte Carlo simulations of 32-player, 5-round Swiss tournaments. All five scoring systems were evaluated on identical pre-generated game outcomes. Source code and full results available in the accompanying notebook.*
