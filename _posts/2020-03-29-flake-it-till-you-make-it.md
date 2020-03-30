---
layout: post
title: Flake it till you make it
subtitle: Excerpt from Soulshaping by Jeff Brown
bigimg: /img/path.jpg
tags: [books, test]
---

Modeling natural images with latent variable models whose continuous latent variables represent locations on the manifold can be a useful approach that is also discussed here. As in part 1, a model with one latent variable $\mathbf{t}_i$ per observation $\mathbf{x}_i$ is used but now the latent variables are continuous rather than discrete variables. Therefore, summations over latent variable states are now replaced by integrals and these are often intractable for more complex models. 

Observations i.e. images $$\mathbf{X} = \left\{ \mathbf{x}_1, \ldots, \mathbf{x}_N \right\}$$ are again described with a probabilistic model $p(\mathbf{x} \lvert \boldsymbol{\theta})$. Goal is to maximize the data likelihood $p(\mathbf{X} \lvert \boldsymbol{\theta})$ w.r.t. $\boldsymbol{\theta}$ and to obtain approximate posterior distributions over continuous latent variables. The joint distribution over an observed variable $\mathbf{x}$ and a latent variable $\mathbf{t}$ is defined as the product of the conditional distribution over $\mathbf{x}$ given $\mathbf{t}$ and the prior distribution over $\mathbf{t}$.

$$
p(\mathbf{x}, \mathbf{t} \lvert \boldsymbol{\theta}) = p(\mathbf{x} \lvert \mathbf{t}, \boldsymbol{\theta}) p(\mathbf{t} \lvert \boldsymbol{\theta})
\tag{1}
$$

We obtain the marginal distribution over x by integrating over t.

$$
p(\mathbf{x} \lvert \boldsymbol{\theta}) = \int p(\mathbf{x} \lvert \mathbf{t}, \boldsymbol{\theta}) p(\mathbf{t} \lvert \boldsymbol{\theta}) d\mathbf{t}
\tag{2}
$$

This integral is usually intractable for even moderately complex conditional probabilities $p(\mathbf{x} \lvert \mathbf{t}, \boldsymbol{\theta})$ and consequently also the true posterior.

$$
p(\mathbf{t} \lvert \mathbf{x}, \boldsymbol{\theta}) = {p(\mathbf{x} \lvert \mathbf{t}, \boldsymbol{\theta}) p(\mathbf{t} \lvert \boldsymbol{\theta}) \over p(\mathbf{x} \lvert \boldsymbol{\theta})}
\tag{3}
$$

This means that the E-step of the EM algorithm becomes intractable. Recall from part 1 that the lower bound of the log marginal likelihood is given by 

$$
\mathcal{L}(\boldsymbol{\theta}, q) = \log p(\mathbf{X} \lvert \boldsymbol{\theta}) - \mathrm{KL}(q(\mathbf{T} \lvert \mathbf{X}) \mid\mid p(\mathbf{T} \lvert \mathbf{X}, \boldsymbol{\theta}))
\tag{4}
$$

In the E-step, the lower bound is maximized w.r.t. $q$ and $\boldsymbol{\theta}$ is held fixed. If the true posterior is tractable, we can set $q$ to the true posterior so that the KL divergence becomes $0$ which maximizes the lower bound for the current value of $\boldsymbol{\theta}$. If the true posterior is intractable approximations must be used. 
