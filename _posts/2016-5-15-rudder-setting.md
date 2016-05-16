---
layout: post
title: Victoria - Rudder Setting
---

One of the things I cannot count on is that Victoria will always know where rudder "zero" is. Maybe something jostles the rudder motor hard and the connections slip somewhere, maybe I'm being overly cautious.

The best way to combat that is to re-calculate the rudder zero every so often. Having the logic to do this also means I can be lazy and not have to set it up perfectly when building. I am lazy.

The idea is simple, have something that physically blocks the rudder from turning past a certain points in either direction. Move to the left until blocked and record that position. Move to the right until blocked and record that position. Set zero as the middle of those two positions.

The logic is [built](https://github.com/grossadamm/victoria/commit/ac72541ce2a3bec199850d74f7e65e2d9eb83c3a), now to figure out why comms is hanging too long... 