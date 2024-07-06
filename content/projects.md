---
title: "Projects"
draft: false
---

## Present
### Learning Admissible and Monotone Heuristics for A*
- Type: Master's Thesis

In my Master's thesis, I work on methods for efficiently learning heuristics from data that can then be employed in algorithms such as A* and rapidly exploring random trees (RRTs). Crucially, distinctive from prior approaches, my goal is finding an approach that learns accurate and useful heuristics _without_ requiring prior knowledge of the value function.

As this is an ongoing project, I do not yet have final results. However, preliminary results, also on complex and high-dimensional environments, show that my method is effective and learns heuristics that can drastically decrease the number of vertices visited by A*.

## Past
### Random Fourier Series Features
- [Full Text PDF](/projects/rfsf.pdf)
- Type: Directed Research Project

While Gaussian process regression is extremely powerful and usually has great uncertainty calibration, it suffers from high computational complexity for large datasets. It is thus desirable to find _feature-based_ kernels that approximate kernels in a low-dimensional feature space. A well-known approach to this idea are _random Fourier features,_ which can efficiently approximate the RBF kernel. However, the RBF kernel is often too smooth in real-world applications as its bandwidth is stationary.

In this project we propose a novel feature-based kernel on top of random Fourier features: we extend them to random Fourier _series_ features by adding higher harmonics. This enriches the kernel's capacity by adding hyperparameters in the form of amplitudes and allows learning a kernel from data.

### Self-Paced Domain Randomization
- [Full Text](/projects/spdr.pdf)
- Type: Directed Research Project

In robot learning, a common problem is the _sim-to-real gap:_ as training on the real robot is costly and labor-intensive, the training algorithms are often executed and subsequently the policy is transferred to the robot. However, this transfer is nontrivial as simulators are imperfect and policies trained therein only work for that specific simulator. A common approach to bridging the sim-to-real gap is domain randomization. Instead of training in a fixed environment, some parameters, e.g., the friction coefficients, are randomized. However, this approach can be very time-consuming as training in random environments is inherently unstable.

In this project we propose a new approach to domain randomization called _self-paced domain randomization._ It is based on _self-paced reinforcement learning,_ a curriculum learning approach to reinforcement learning. Instead of randomizing all parameters uniformly and from the start with the same variance, we start off with sampling domain parameters from distributions with small variance. Over time, once the agent learns a policy that reaches the goal, we increase the variance to enhance the policy's robustness. Once a predefined target variance is reached, we terminate.

### Variational Autoencoders for Koopman Dynamical Systems
- [Full Text](/projects/vae4koopman.pdf)
- Type: Bachelor's Thesis

While control theory for linear systems is well understood and efficient methods exist to control a system as desired, nonlinear systems are still a great challenge. We thus often fall back to approximating a nonlinear system linearly, e.g., by Taylor-expanding it around a stationary point. However, these approximations only hold locally, requiring repeated updates of the approximation.

In my Bachelor's thesis, I propose _Koopman inference,_ an algorithm that combined inference in linear Gaussian dynamical systems with Koopman theory. Koopman theory states that, for a sufficiently large latent space, there exists a lifting from the original space into this latent space such that the nonlinear system dynamics evolve linearly therein. However, finding this lifting and the linear dynamics is hard. My approach, _Koopman inference,_ is an approximate expectation-maximization algorithm that jointly learns the latent dynamics and a function approximator for the mapping from latent space into the original space.

### Policy Presentation: Policy Summarization and Interactive Learning
- [Full Text PDF](/projects/pp.pdf)
- [Poster](/projects/pp-poster.pdf)
- Type: Seminar

In this seminar, I conducted an in-depth literature review on the topics of policy summarization and interactive learning. _Policy summarization_ is concerned with presenting a human the core behavior of a policy and trying to gauge why a policy behaves as it does. _Interactive learning,_ on the other hand, is concerned with how a user may interact with the learning process to guide the learning, e.g., by manually assigning rewards to actions. Interestingly, these two fields have so far been explored separately, although an integration seems reasonable: a human might be able to give better feedback to the algorithm if they understand why something happens.
