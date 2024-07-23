---
title: "Publications"
draft: false
---

{{< publication
    title="Decoding Multilingual Moral Preferences: Unveiling LLM's Biases Through the Moral Machine Experiment"
    authors="[K. Vida](https://www.bwl.uni-hamburg.de/en/ds/team/vida.html)\*, **[F. Damken](https://fabian.damken.net/)**\*, [A. Lauscher](https://anne-lauscher.de/)"
    venue_name="AIES 2024"
    venue_url="https://www.aies-conference.com/2024/"
    paper="/publications/vida2024decoding.pdf"
    code="https://github.com/fdamken/decoding_multilingual_moral_preferences" >}}
Large language models (LLMs) increasingly find their way into the most diverse areas of our everyday lives. They indirectly influence people's decisions or opinions through their daily use. Therefore, understanding how and which moral judgements these LLMs make is crucial. However, morality is not universal and depends on the cultural background. This raises the question of  whether these cultural preferences are also reflected in LLMs when prompted in different languages or whether moral decision-making is consistent across different languages. So far, most research has focused on investigating the inherent values of LLMs in English. While a few works conduct multilingual analyses of moral bias in LLMs in a multilingual setting, these analyses do not go beyond atomic actions. To the best of our knowledge, a multilingual analysis of moral bias in dilemmas has not yet been conducted.

To address this, our paper builds on the moral machine experiment (MME) to investigate the moral preferences of five LLMs, Falcon, Gemini, Llama, GPT, and MPT, in a multilingual setting and compares them with the preferences collected from humans belonging to different cultures. To accomplish this, we generate 6500 scenarios of the MME and prompt the models in ten languages on which action to take. Our analysis reveals that all LLMs inhibit different moral biases to some degree and that they not only differ from the human preferences but also across multiple languages within the models themselves. Moreover, we find that almost all models, particularly Llama 3, divert greatly from human values and, for instance, prefer saving fewer people over saving more.
{{< /publication >}}

---

{{< publication
    title="STAMP: Differentiable Task and Motion Planning via Stein Variational Gradient Descent"
    authors="[Y. Lee](https://yewon-lee.github.io/), [P. Huang](https://philip-huang.github.io/), [K. M. Jatavallabhula](https://krrish94.github.io/), [A. Li](https://andrewzl.github.io/), **[F. Damken](https://fabian.damken.net/)**, [E. Heiden](https://eric-heiden.com/), [K. Smith](https://www.mit.edu/~k2smith/), [D. Nowrouzezahrai](http://www.cim.mcgill.ca/~derek/), [F. Ramos](https://fabioramos.github.io/), [F. Shkurti](https://www.cs.toronto.edu/~florian/)"
    venue_name="CoRL 2023 -- LEAP Workshop"
    venue_url="https://leap-workshop.github.io/leap2023.html"
    arxiv="2310.01775"
    openreview="jtxPRTTgx1" >}}
Planning for many manipulation tasks, such as using tools or assembling parts, often requires both symbolic and geometric reasoning. Task and Motion Planning (TAMP) algorithms typically solve these problems by conducting a tree search over high-level task sequences while checking for kinematic and dynamic feasibility. This can be inefficient as the width of the tree can grow exponentially with the number of possible actions and objects. In this paper, we propose a novel approach to TAMP that relaxes discrete-and-continuous TAMP problems into inference problems on a continuous domain. Our method, Stein Task and Motion Planning (STAMP) subsequently solves this new problem using a gradient-based variational inference algorithm called Stein Variational Gradient Descent, by obtaining gradients from a parallelized differentiable physics simulator. By introducing relaxations to the discrete variables, leveraging parallelization, and approaching TAMP as an Bayesian inference problem, our method is able to efficiently find multiple diverse plans in a single optimization run. We demonstrate our method on two TAMP problems and benchmark them against existing TAMP baselines.
{{< /publication >}}
