---
layout: post
title: Victoria - LiFePO4 and Solar
comments: true
---

The simplest solution to getting Victoria powered and moving without be use a sealed lead acid battery [like this](http://www.amazon.com/dp/B004DR09Z2/ref=pd_lpo_sbs_dp_ss_3?pf_rd_p=1944687702&pf_rd_s=lpo-top-stripe-1&pf_rd_t=201&pf_rd_i=B00BMUDOLE&pf_rd_m=ATVPDKIKX0DER&pf_rd_r=0YHC6QHNXW9G6TN2QNWT) and standard solar charger [like this](http://www.amazon.com/TRACER-3215RN-Solar-Charge-Controller/dp/B008KWPGAE). Unfortunately, those batteries are *heavy*, 60 freedom pounds to be exact, they do not last a large number of full cycles, and full cycles is a bit of a misnomer since you really should not discharge them more than 50% for the best longevity.

The best alternative I can find is to use LiFePO4 Batteries. They are much lighter (<10lbs for 100ah), can be discharged down to almost 10% without damage, and last a far larger number of full cycles. Unfortunately they are much more expensive, and using them with solar is fairly new. Additionally, the cells can be irreparably damaged if abused whereas a sealed lead acid battery can sometimes be partially repaired after abuse.

In order to save cost, I will build the 100ah battery myself out of prismatic cells. Thankfully, Bioenno Power has a MPPT solar charger that will work with LiFePO4 [link](https://www.bioennopower.com/products/12v-24v-20a-mppt-solar-charge-controller-for-lifepo4-batteries-sc-122420wm?variant=9849056901). Couple that with a battery protection circuit such as [this one](http://www.bestechpower.com/128v4spcmbmspcbforlifepo4batterypack/PCM-D175.html) and a cell balancing circuit like [this](http://www.bestechpower.com/balanceboard/HCX-D136.html) and hopefully Victoria will be OK long-term in the power department. The charge controller has a reset button though and that makes me very leery since no one can push the button, but so far I have yet to find a decent charge controller alternative without a button.