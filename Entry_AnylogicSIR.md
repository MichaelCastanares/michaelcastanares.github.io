---
layout: default
title: Blog
---

[Home](/) | [Research Blog](/blog)

---
### "Anylogic: Contagion model"
*7 May 2025*

audience: anylogic practitioners, researchers, and prospective employers who are looking to apply systems thinking


Systems thinking emphasizes the importance of understanding complex systems.
Modelling allows us to explore the properties of the system and try to match it with the observed reality.
The SEIR model is a good example to demostrate the spread of disease. 

I take inspiration from the work of Rahmandad & Sterman (2008).


**Q1:** How does network structure affect the spread of disease?;

**Q2:** How could intervention policies such as contact tracing remedy the cost.

In this blog, I explore the effect of network structure with the spread of disease. I use the DE-based Contagion model as a baseline/control model. Then I build an agent based model with small world and XX characteristic and compare how exposure rate and infection change with varied network characteristics. 

My goal is to share some insights to these questions based on the simulation model I built using AnyLogic software.

### Platform
All simulations were built and run using AnyLogic 8 Personal Learning Edition 8.9.8.

### A. Theoretical Foundations

**A.1 SEIR model**. A common example of the contagion model is the Susceptible Exposed Infected Recovery (SEIR) model. It is a compartmental model that is used to simulate the spread of disease [Wikipedia].

The population is divided into four states: Susceptible, Exposed, Infected, and Recovery. 

- Susceptible are agents who are vulnerable to disease
- Exposed are agents who are infected but are in an incubation phase and are not yet infectious. It takes an `incubation period` for the agent to develop symptoms of the disease.
- Infected are agents who have the disease and are able to transmit the disease to susceptible agents
- Recovered are agents who have recovered from the disesase and have developed immunity.

**A.1 DE model**.
The system dynamics of the SEIR model is described by the following rates [https://en.wikipedia.org/wiki/Compartmental_models_(epidemiology)]

$$
\frac{dS}{dt} = - \frac{\beta}{N}*IS
$$
$$
\frac{dE}{dt} = \frac{dS}{dt} - \frac{E}{T_{incubation}}
$$
$$
\frac{dI}{dt} = \frac{dE}{dt} - \frac{I}{T_{illness}}
$$

Also, it is assumed that the system is closed and there is no leak such as the total population remains constant at any point in time.

$$
\frac{dS}{dt} + \frac{dE}{dt} + \frac{dI}{dt} + \frac{dR}{dt} = 0
$$

$$
S(t) + E(t) + I(t) + R(t) = N
$$

**A.2 Agent-based model**.


**A.4 Network Structure**. 
The DE model assumes perfect mixing, i.e., infectious individuals can meet a susceptible individual with equal probability [Rahmandad]. However, real networks are sparse and clustered, i.e., individual tend to likely meet with people who they know.

#why this matters


fully connected, random (Erdos and
Renyi 1960)

small world (Watts and Strogatz 1998),
- six degree of separation


scale-free (Barabasi and Albert 1999),
- power-law distribution


### B. Application


### Final thoughts

However this example can be translated to transmission of other object such as information, viral social media content, news, recommendations that are useful in businesses.

Codes used to generate the figures may be found here: [View Code Repository on GitHub](https://github.com/MichaelCastanares/Github/tree/main/Anylogic_Market)

Disclaimer of AI use: Claude Haiku was used to improve the flow of the discussion.


### Reference:

Rahmandad, H., & Sterman, J. (2008). Heterogeneity and network structure in the dynamics of diffusion: Comparing agent-based and differential equation models. *Management Science*, 54(5), 998–1014. https://doi.org/10.1287/mnsc.1070.0787


