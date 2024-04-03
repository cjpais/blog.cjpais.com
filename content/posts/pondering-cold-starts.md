---
title: "`Preemptively Warm` to Improve Cold Start Performance"
date: 2024-04-02T19:51:00-08:00
draft: false
tags:
    - ml
    - ai
    - cold-start
    - inference
keywords:
    - ml
    - ai
    - cold-start
    - inference
---

The cold start problem for LLM inference seems to be isolated to a company at small scale. They want to give the people using their product a wonderful experience, but they don't necessarily have the capital to keep GPU servers running all the time. Or perhaps that cost is just too high and they are unwilling to pay the fee. As an independent dev, I certainly get sticker shock when calculating out the cost to run a GPU 24/7 just so I can have inference start in under 200ms.

I tried tackling this problem in a few ways. My friends had been tossing the idea of running a mac mini network together for a while. I thought this might be a great application to put the network together. The core of the idea is to get some friends together and run our computers all the time, with the models loaded in them. This way the model's are ready to go, without the cost of paying for proper servers. Turns out, yeah, this works. But one problem is now everyone needs to be a sysadmin, or I have to be the sysadmin for everyone. I do see some opportunity to improve that as well. So this is really fun, and actually the solution for now. But my mind continued to think, "what about scale?".

I look to Modal, Inferless, and anyone offering serverless GPU's. Trying to think what could improve their ability to initialize models. I know [llama.cpp](https://github.com/ggerganov/llama.cpp) used memory mapping to improve loading performance of the models. Thinking a bit on this I wondered it maybe doing memory mapping at scale would be helpful, maybe by using using [RDMA](https://en.wikipedia.org/wiki/Remote_direct_memory_access) or something. Surely we can take advantage of those 400/800Gbps network fabrics. I am not really an infra guy, but this seems doable, perhaps expensive. But maybe much less expensive than running a GPU 24/7? Surely having a bunch of models in memory would be faster than loading them from disk. This is where my knowledge of systems ends and maybe it's not feasible at all. But I would be curious to talk to a network architect. If you are one, hit me up! 

After doing all this thinking, I questioned the premise. Do cold starts matter? Is this a problem that only exists at small scale? Am I just solving a problem that doesn't exist? Am I wasting my time thinking about this? Well, maybe. 

What makes the cold start problem go away? Have it be warm before anyone clicks anything. Sounds obvious, and in hindsight it is obvious. When the person loads the webpage or opens the app, ping the system to warm it up. Yeah. That's it. That 2 seconds it took to warm is now not even noticed by the time the person has clicked a button. This is a tiny pattern, but somehow I missed it for some time. It's so simple and obvious. The cold start doesn't really matter, just make sure the system is warm before the person does anything. My greedy, greedy technical brain says "give me the model now!", but maybe the solve doesn't need to be technical. Maybe it's just a matter of timing.