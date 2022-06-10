# Scrum Poker Online

This literally takes 10 seconds to set up. As far as I know, it's the fastest way to play Scrum Poker for free without setting up an account. It's also mobile friendly and there's a QR code. Check out [scrumpoker-online.org](https://www.scrumpoker-online.org/).

## User Story

* As a Scrum user, I want each team member to submit an honest Story Point estimate.
* Each user's Story Point estimate should be completely independent. This means we have to avoid the influence of [anchoring](https://en.wikipedia.org/wiki/Anchoring_(cognitive_bias)).

  > The anchoring effect is a cognitive bias whereby an individual's decisions are influenced by a particular reference point or 'anchor'. Both numeric and non-numeric anchoring have been reported in research. In numeric anchoring, **once the value of the anchor is set, subsequent arguments, estimates, etc. made by an individual may change from what they would have otherwise been without the anchor**.

## Solution

* Team members' estimates stay hidden and are all revealed at the same time. This avoids the effects of **anchoring**.

## Improvements

As of 2022 06 10, the Scrum Poker site allows **any** team member to reveal all the estimates at **any** time. This can lead to a problem:

* A team member can prematurely reveal the estimates, even before all submissions are received. Any submissions received after the reveal might be affected by **anchoring**.

I can currently think of 2 potential solutions.

* Estimates can only be reavealed if every member submitted one (and optionally indicates their estimate is final).
  * A potential issue with this is if a member is away or refuses to submit an estimate. An admin of the Scrum Poker session could exclude them from the current round and reveal the available estimates.
  * People might revise their estimates after they submitted them but before they were revealed. To ensure only `final` estiamtes are revealed, there could be an option to 'lock in' an estimate and indicate that it's ready to reveal. This seems a bit cumbersome.
* Only an admin of the Scrum Poker session can reveal estimates. An admin role can be assigned to the first person to join the Scrum Poker session, with an option to pass admin privileges to another team member.
