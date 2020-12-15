---
title: "New Stuff in Vowpal Wabbit 8.9.0"
date: 2020-12-14T09:57:29-06:00
draft: false
---

# New Stuff in Vowpal Wabbit 8.9.0

Vowpal Wabbit 8.9.0 was [released a few weeks ago](https://vowpalwabbit.org/blog/vowpalwabbit-8.9.0.html) and includes a *ton* of interesting new features.
I think it's fair to say that it's largest new release in my memory having used and followed the project now since 2014.
This release shows excellent progress apparently due at least in part to Microsoft's increased investment and reliance on the project.

This release seems to focus primarily on algorithm support and offline ease-of-use as opposed to in-production-ease-of-use. This may be because the production niceties are often handled by [Azure Personalizer](https://docs.microsoft.com/en-us/azure/cognitive-services/personalizer/) and so it likely makes more sense for the vowpal team to shift focus away from things like model management, monitoring, delayed/buffered reward joining (aka the "join server"). In short: reinforcement learning in production requires a lot of robust data pipeline components and very capable engineering beyond just the algorithms themselves and Microsoft seems to be focusing on monetizing that portion of the work but still allowing the core ML work to be fully open and usable by anyone.

The page linked above does a good job summarizing the new stuff but I'll recap here in brief:
- [Easy Python installation via wheels](https://github.com/VowpalWabbit/vowpal_wabbit/wiki/Python#support)
- [Slates (CB)](https://vowpalwabbit.org/blog/vowpalwabbit-8.9.0.html#slates)
- [Probabilistic Label Tree](https://vowpalwabbit.org/blog/vowpalwabbit-8.9.0.html#probabilistic-label-tree)
- [Continuous Actions](https://vowpalwabbit.org/blog/vowpalwabbit-8.9.0.html#continuous-actions)
- [SquareCB](https://github.com/VowpalWabbit/vowpal_wabbit/wiki/Contextual-Bandit-Exploration-with-SquareCB) Exploration
- [Early Pandas support](https://vowpalwabbit.org/blog/vowpalwabbit-8.9.0.html#initial-pandas-support-in-python)

### Python Support
As mentioned above vw can now easily be installed via `pip` where previously installation was often challenging and in my experience occasionally would completely break
existing conda environments. With installation proceeding via pre-built wheels there is no need to manually install dependencies (like boost), deal with build errors or to make yourself a cup of coffee while vowpal builds.

Vowpal now has early but useful Pandas support. Taken together these two things definitely indicate Vowpal's increased focus on the Python ecosystem as
opposed to the historical focus on the command line `vw` executable. The command line is still the "main" interface I'd say but Python support has come a long way and is obviously now a first-class citizen in Vowpal world.
I've used a ton of Pandas but in general I'm ambivalent about it due to its sometimes extreme memory requirements with respect to the source data and what I perceive to be inconsistency in the API. I'm very glad it exists as it filled a real need in the Python community, but I'm hopeful for better tools in the future.

### Slates
For ranking a "slate" of items with a single per-slate reward (referred to as "whole-page metrics" in the paper) and typically for rankings over relatively few items.
I tend to think of this in the context of a webpage where a click **anywhere** on the page is valuable, but that we are not interested in per-module or per-unit feedback on the page in the manner of a traditional learning-to-rank problem.
The Vowpal folks don't seem to be publicizing it much yet but the super-prolific [Jack Gerrits](https://github.com/jackgerrits) has created this [slates-experiments](https://github.com/VowpalWabbit/slates-experiments) repo with a few notebooks demonstrating usage and testing things.
The [paper](https://arxiv.org/abs/1605.04812) also provides much more detail of course, a [repo of its own](https://github.com/adith387/slates_semisynth_expts) 
and shares some compelling results on real data in comparison to LambdaMART among others.

### Probabilistic Label Tree
Great addition here from [Marek Wydmuch](https://github.com/mwydmuch) useful for "extreme classification" problems with very large numbers of labels
Wydmuch had done some extreme classification work previously in some forked repos ([extremeText](https://github.com/mwydmuch/extremeText), [napkinXC](https://github.com/mwydmuch/napkinXC))
For more on these "extreme multilabel learning" or "extreme classification" problems see [Manik Varma's page](http://manikvarma.org/downloads/XC/XMLRepository.html)

### Continuous Actions
These are pretty much what they sound like. "Standard" bandits often model a choice among discrete options whereas continuous armed bandits ("cats" in vw-speak) extend this to the continuous setting. Example use cases here might be choosing the amount of a discount to offer a shopper, how much of a drug to prescribe to a patient or how many minutes of training an athlete should perform to get the largest gains.

## SquareCB
Lots of [docs](https://github.com/VowpalWabbit/vowpal_wabbit/wiki/Contextual-Bandit-Exploration-with-SquareCB) on this one and encouraging evidence from the so-called ["bake-off paper"](https://arxiv.org/abs/1802.04064)
I have yet to try SquareCB but plan to compare it to other approaches using the CB examples in my [Ocaml bindings repo](https://github.com/travisbrady/ocaml-vw/tree/master/examples)

## Also
Vowpal now also has a pretty active [Gitter room](https://gitter.im/VowpalWabbit/community?source=orgpage) which seems to have picked up helpful discussion since the
demise of the old vw Yahoo group. Definitely worth a look if you're actively engaged in the project.

It also seems worth checking out [this talk from NeurIPS 2020 Expo Day](https://slideslive.com/38942331/vowpal-wabbit) I recently spotted on Twitter.
