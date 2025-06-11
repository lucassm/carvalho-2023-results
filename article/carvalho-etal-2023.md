---
type: article
title: "Optimization-Based Operation of Distribution Grids With Residential Battery Storage: Assessing Utility and Customer Benefits"
---

# Optimization-Based Operation of Distribution Grids With Residential Battery Storage: Assessing Utility and Customer Benefits 

- Wilhiam C. de Carvalho ,
- Elizabeth L. Ratnam, Senior Member, IEEE,
- Lachlan Blackhall, Senior Member, IEEE, and
- Alexandra von Meier, Senior Member, IEEE

## Abstract

Increasing levels of distributed solar photovoltaic (PV) generation has created significant technical challenges in distribution networks, particularly regarding voltage regulation. **Small-scale behind-the-meter battery storage is a key element** in effectively overcoming such challenges, while offering financial benefits for customers. In this paper, **we propose an optimization-based approach for dispatching power from residential-scale battery storage for grid support and customer savings**, considering only local (behind-the-meter) measurements. The proposed approach takes into account the physics of the grid and both real and reactive power (coupled) for voltage regulation and grid loss reduction. The optimization-based approach, termed **Local-Quadratic Program (L-QP)**, is formulated based on the linear power flow equations (**LinDistFlow**). The proposed L-QP is benchmarked against an approach in which real power is used to maximize the customer benefit, while reactive power is dedicated for voltage regulation. Numerical simulations with the IEEE 13 and IEEE 123 Node Test Feeders, which include realistic time-varying data for residential load and PV generation, demonstrate the technical advantages of the proposed approach.

Index Terms-Battery storage, distribution network, grid power losses, solar photovoltaic, voltage regulation.

## Introduction

The dramatic increase of solar photovoltaic (PV) penetration in recent years has caused significant challenges for distribution network operators. High rooftop PV generation combined with low power demand can result in reverse power flow along line segments and an unacceptably high grid voltage. Significant voltage rise can limit customer-owned solar PV generation and, in turn, potentially reduces financial saving that a PV customer accrues [1]. Among different measures to mitigate voltage issues posed by distributed PV, including [^0] grid reinforcement or the installation of on-load tap changing transformers, are increasingly affordable battery storage solutions. Residential-scale battery storage that charges when solar generation is in excess, potentially reduces grid over-voltage conditions at the source of the problem [2].

> [!important]
> Approaches to charge and discharge residential-scale battery storage are typically designed to provide financial benefits to the battery owner [3]. However, the overwhelming majority of economic-based methods do not consider the local impact on the grid voltage [4].

Alternatively, to improve distribution grid voltages, **it is possible to inject/absorb inverter-based reactive power from residential battery systems [5]**. However, using reactive power alone can lead to unsatisfactory voltage regulation with excessive power losses in the distribution network [6].

> Decoupling real power for customer economic-benefit and reactive power for voltage regulation, while sensible in transmission networks, has fundamental limitations in distribution grids [6]. Specifically, the higher resistance over reactance ( $\mathrm{R} / \mathrm{X}$ ) ratio of lines in the distribution grid couples both real and reactive power flows to over-voltage or under-voltage conditions, limiting the long-term applicability of the aforementioned decoupled approaches [6].

> [!note]
> Esse ponto em que a autora do trabalho faz uma comparação entre as diferenças nos efeitos das variações de potência ativa e reativa na rede elétrica dos sistemas de transmissão e distribuição é muito importante de ser compreendido, sendo necessário inclusive uma investigação mais profunda sobre o tema, tando na literatura, geral e indicada pela autora, quanto no desenvolvimento de demonstrações práticas por meio de experimentos computacionais.

Several papers in the literature have proposed new approaches for dispatching real and reactive power of residential battery systems for both grid and customer benefit. An optimization-based approach is proposed in [7] to use **real power from the battery for customer financial benefit**, while promoting charging during the peak PV generation period. Nevertheless, when the grid voltage exceeds a threshold, **both real and reactive power from the residential battery system are dispatched** to drive the grid voltage closer to the nominal voltage. In [8] the **reactive power is constantly dispatched for voltage regulation**, while **real power from the battery system is reserved for correcting voltage excursions beyond a nominal threshold**. The authors in [9] propose a method to **dispatch real power from the battery** to maximize customer financial savings, while **reactive power is reserved for power factor correction** of the residential system. A variety of **rule-based approaches for real and reactive power dispatch have been proposed and compared in [10]** to provide customer benefit and grid voltage regulation services.

> [!important]
> Due to **the limited efficacy of reactive power for voltage regulation in distribution networks**, other studies [11]-[16] have focused only on dispatching real power, i.e. charging/discharging battery storage.

Several behind-the-meter optimization-based approaches have been proposed in [11], [12] to **reduce real power imports/exports from/to the grid** while considering customer savings. The authors in [13], [14] propose to **use the real power of the battery to improve grid voltages** alongside customer benefit. However, in [13] the proposed optimization-based approach includes an additional cost when real power exports exceeds a threshold, whereas in [14] a time-based approach is proposed to prevent overvoltage by charging the battery proportional to the amount of PV generation. Moreover, in [15], [16] **real power is dispatched for grid voltage regulation, disregarding the benefits provided for the battery owner**.

> [!important]
> Although reactive power for voltage regulation in the distribution grid is not as effective as in the transmission network, it can still contribute to improve grid voltages and reduce grid power losses. Ultimately, **it is the grid impedance characteristic that determines how effective real and reactive power is to regulate grid voltage** and the impact on grid power losses.

It follows that the authors in [17]-[23] have proposed **centralized and distributed approaches to dispatch real and reactive power from residential energy systems**, which incorporate network models that capture the relationship of grid impedance to grid voltages and power losses.

However, a key challenge that exists is:

> [!important]
> To capture such a relationship with a formulation that considers **only local (behind-the-meter) measurements**, which are:
>
> - fast-acting to system variability,
> - robust to communication failures, and
> - privacy preserving [20].

> [!note]
> Essa é a motivação explícita do trabalho:
> 
> This motivates us to consider more directly the impedance characteristic of the electrical network in the formulation of a *local optimization-based approach to dispatch real and reactive power from a residential energy system, that improves supply voltages and reduces power losses throughout the electrical network*.

In this paper, we propose: **a local optimization-based approach for dispatching real and reactive power of behind-themeter residential-scale battery storage**.

The optimization problem incorporates both real and reactive power (coupled) for both grid voltage regulation and grid power loss reduction.

The formulation is based on the impedance characteristics of the network, which fundamentally dictates the relation of real and reactive power with grid voltages.

Specifically, the proposed optimization-based approach, labelled **Local-Quadratic Program (L-QP), incorporates a linearized model of the distribution grid power flow equations (i.e., LinDistFlow) together with behind-the-meter (local) voltage and power flow measurements**.

Our objective is **to increase the customer financial benefits for operating residential battery storage, while improving grid voltages and power losses**.

The contributions of this paper are:

- (i) the derivation of an equation with both real and reactive power coupled for **voltage regulation** considering only behind-the-meter variables;
- (ii) the derivation of mathematical terms to express **grid resistive power losses** using only behind-the-meter variables; and
- (iii) the formulation of a local optimization-based approach for behindthe-meter battery storage operation that seeks to **minimize grid voltage deviations, grid resistive losses and customer electricity billing costs**.

Importantly, the derivation of (i) and (ii) culminate in the proposed local optimization-based approach (iii). 

> [!important]
> It is worth mentioning that (i) and (ii) can underpin other applications, including the design of new tariff structures for individual customers.

This paper focuses on deriving and incorporating the networkcognizant equations in a local (fully decentralized) optimizationbased approach and investigating their effectiveness when adverse interactions between inverters do not impact overall performance.

We benchmark our proposed L-QP algorithm against an alternative approach that also ingresses local measurements, however, separates real power for maximizing customer savings and reactive power for voltage regulation. Numerical simulations are carried out with challenging distribution test feeders and with actual time-varying data for residential load and PV generation [24].

This paper is organized as follows:

- The LinDistFlow equations together with the residential system are introduced in Section II.
- We derive grid voltage and resistive loss equations, and formulate the L-QP approach in Section III.
- Numerical simulations follow in Section IV.

## Preliminaries

We consider a single-phase radial distribution network modelled as a connected graph as in Fig. 1. 

The set of nodes is denoted by $\mathcal{N}_{o}=\{0,1, \ldots, N\}$, where 0 is the source node, also referred as slack node or substation bus, and $N$ is the total number of nodes downstream of node 0 (i.e. $\left|\mathcal{N}_{o}\right|=N+1$ ). The set of edges is denoted by $\mathcal{E} \subseteq \mathcal{N}_{o} \times \mathcal{N}_{o}$, where edge $(m, n) \in \mathcal{E}$ represents a line segment from node $m$ to node $n$. The distribution network can then be represented by the graph $\mathcal{G}=\left(\mathcal{N}_{o}, \mathcal{E}\right)$. We often refer to the set of nodes downstream of node 0, denoted by $\mathcal{N}=\mathcal{N}_{o} \backslash\{0\}$.

![](https://cdn.mathpix.com/cropped/2024_08_27_654167e472f5bf5a26b5g-02.jpg?height=211&width=721&top_left_y=217&top_left_x=1114)

Fig. 1. Distribution network modelled as a connected graph. Node 0 is the source node, also referred as slack or substation bus, and $l, m, n$ are indices used to represent nodes and line segments.

In Fig. 2 we present our distribution network and residential system notation.

Line segments represent the low-voltage (LV) distribution network, and it is straightforward to extend the notation to represent line segments in the medium-voltage (MV) network. 

Specifically, we consider a set of customers $\mathcal{C}_{m}=$ $\left\{1, \ldots, c, \ldots, C_{m}\right\}$ connected to each node $m \in \mathcal{N}$. The voltage magnitude at node $m$ is denoted by $V_{m}$ and the impedance of the edge $(m, n) \in \mathcal{E}$ is represented by $r_{m n}+j x_{m n}$, where $r_{m n}$ is the resistance and $x_{m n}$ is the reactance of the line segment.

Variable $P_{m n}$ is the real power and $Q_{m n}$ is the reactive power flow in the edge $(m, n)$.

Whereas $P_{m}$ and $Q_{m}$ is the aggregate real and reactive power consumption, respectively, at node $m$, **consistent with the positive load convention**.

> For a customer $c$ connected to node $m$, $p_{m}^{c}$ denotes the real power and $q_{m}^{c}$ denotes the reactive power consumption, **with positive load convention**.

![](https://cdn.mathpix.com/cropped/2024_08_27_654167e472f5bf5a26b5g-03.jpg?height=769&width=863&top_left_y=217&top_left_x=149)

Fig. 2. Distribution network serving residential systems. Arrows indicate the positive direction of power flow. Zoom A depicts the disaggregation of load $P_{m}, Q_{m}$, consisting of the load drawn by each customer in the set $\left\{1, \ldots, c, \ldots, C_{m}\right\}$, e.g., customer $c$ draws load $p_{m}^{c}, q_{m}^{c}$. Zoom B depicts a residential system for customer $c$ connected to node $m$.

> All customers prescribe to a time-of-use (TOU) pricing tariff with the net-metering policy.

> [!note]
> Essas definições são importantes para o entendimento dos cálculos que serão realizados em seguida. É importante compreender que, de acordo com a modelagem realizada pela autora, conectados ao nó m existem m consumidores, cada um com possibilidade de possuir um sistema com geração solar, bateria e carga.
> Outro dado importante que foi mencionado pelos autores é que o esquema tarifário é TOU combinado com política de net-metering, ou seja, existe uma tarifa de energia elétrica variável no tempo e o consumidor é cobrado/remunerado de acordo com a variação no seu consumo/produção.

The relationship of aggregate power consumption to customer power consumption is given by:

$$
P_{m}=\sum_{c \in \mathcal{C}_{m}} p_{m}^{c}, \quad Q_{m}=\sum_{c \in \mathcal{C}_{m}} q_{m}^{c}
$$

for all $m \in \mathcal{N}$. 

Throughout, $V_{m}^{2}$ is referred to as voltage magnitude squared.

> [!important] Definição Importante
> Further, we refer to the **deviation of the voltage magnitude squared relative to node 0**, denoted by:
>
> $E_{m}=$ $V_{0}^{2}-V_{m}^{2}$ by simply voltage deviation. 
>
> Note that: **a positive voltage deviation $\left(E_{m}>0\right)$ represents a voltage drop between the nodes, whilst a negative voltage deviation $\left(E_{m}<0\right)$ represents voltage rise between the nodes**.

Next we consider the **linear power flow equations** developed in [25] for distribution networks. 

> Specifically, we are motivated to consider the *LinDistFlow* equations as **they support the development of convex optimization problem formulations**.

The *LinDistFlow* equations assume negligible power losses in line segments, yet are able to model power networks with satisfactory accuracy as reported in [21]-[23], [26]. 

A single-phase representation of the *LinDistFlow* equations is expressed by:

$$
\begin{array}{r}
P_{l m}=P_{m}+\sum_{n:(m, n) \in \mathcal{E}} P_{m n}, \quad \forall m \in \mathcal{N} \\
Q_{l m}=Q_{m}+\sum_{n:(m, n) \in \mathcal{E}} Q_{m n}, \quad \forall m \in \mathcal{N} \\
V_{m}^{2}=V_{n}^{2}+2 r_{m n} P_{m n}+2 x_{m n} Q_{m n}, \quad \forall(m, n) \in \mathcal{E}
\end{array}
$$

As in [25], [26], **we define a path $\mathcal{L}_{m} \subseteq \mathcal{E}$ as the set of edges (or otherwise line segments) on the unique path from node 0 to node $m$**. We also define matrices $\boldsymbol{R}, \boldsymbol{X} \in \mathbb{R}^{\mathrm{N} \times \mathrm{N}}$, such that elements in the matrices can be computed as:

$$
R_{h k}=\sum_{(m, n) \in \mathcal{L}_{h} \cap \mathcal{L}_{k}} r_{m n}, \quad X_{h k}=\sum_{(m, n) \in \mathcal{L}_{h} \cap \mathcal{L}_{k}} x_{m n}
$$

where $h, k \in \mathcal{N}$ represent the row and column index, respectively, of the matrices.

> Conceptually, the elements in the matrices $\boldsymbol{R}, \boldsymbol{X}$ represent the total resistance and reactance, respectively, of the path that is common for both nodes $h$ and $k$.

Importantly, when $h=k, R_{h h}$ is the summation of the resistance of each line segment along the unique path from node 0 to node $h$. Likewise, $X_{h h}$ is the summation of the reactance of each line segment along the unique path from node 0 to node $h$.

> [!important]
> The LinDistFlow equations are then written in compact form [26] as follows:
>
> $$
> \boldsymbol{E} = 2 \boldsymbol{R} \boldsymbol{P} + 2 \boldsymbol{X} \boldsymbol{Q}
> $$
>
> Where $\quad \boldsymbol{E}=\left[E_{1}, \ldots, E_{N}\right]^{\top}, \quad \boldsymbol{P}=\left[P_{1}, \ldots, P_{N}\right]^{\top}, \quad \boldsymbol{Q}=$ $\left[Q_{1}, \ldots, Q_{N}\right]^{\top}$.
>
> Note that all elements in $\boldsymbol{E}$ are voltage squared deviations relative to node 0 (e.g. $E_{N}=V_{0}^{2}-V_{N}^{2}$ ).
> It is worth mentioning that (6) is formulated with nodal aggregate power, instead of line power flows as in (4).

> [!note] Nota de Implementação
> Nesse ponto é importante firmar que se faz necessário a implementação da obtenção das matrizes $\mathbf{R}, \mathbf{X}, \mathbf{P}, \mathbf{Q}$, para que a matriz $\mathbf{E}$ também possa ser obtida. Isso será realizado no pluto notebook presente nesse repositório.

## A. Residential System

Fig. 2 depicts a residential system connected to node $m$ for a customer $c \in \mathcal{C}_{m}$. The residential system includes a load, solar PV, and battery storage. The battery storage represents a dispatchable resource, whereas load and PV generation are considered uncontrollable resources. Although PV inverters are usually able to dispatch reactive power, in this study, for simplicity, the dispatchable reactive power $\left(v_{m}^{c}\right)$ is provided by the battery inverter only. We introduce a set denoted by $\mathcal{K}=\{1, \ldots, k, \ldots, K\}$, where $k$ denotes a time index and $K$ is the total number of time indices. We denote by $\Delta$ the length of one time interval (i.e., $((k-1) \Delta, k \Delta)$ ), and we define a time horizon $T=K \Delta$, where $[0, T]$ is a time window.

In Fig. 2, $p_{m}^{c}(k), d_{m}^{c}(k), g_{m}^{c}(k)$ and $u_{m}^{c}(k)$ represent average real power flows (in kW ) across time interval $((k-1) \Delta, k \Delta$. Similarly, $q_{m}^{c}(k), e_{m}^{c}(k)$ and $v_{m}^{c}(k)$ denote average reactive power flows (in kvar) across time interval $((k-1) \Delta, k \Delta)$. The real and reactive power consumed by the entire residential system is represented by $p_{m}^{c}(k)$ and $q_{m}^{c}(k)$, respectively. The power flows from the grid to the residence are positive, whereas power flows from the residence exported to the grid are negative. We represent real and reactive residential load by $d_{m}^{c}(k), e_{m}^{c}(k) \in \mathbb{R}_{\geq 0}, \forall k \in \mathcal{K}$, respectively, and $g_{m}^{c}(k) \in \mathbb{R}_{\leq 0}$, $\forall k \in \mathcal{K}$, represents the solar PV real power. The real and reactive battery power is denoted by $u_{m}^{c}(k)$ and $v_{m}^{c}(k)$, respectively, where positive power flows represent the battery absorbing power and negative power flows represent the battery generating power. The real and reactive power balance equations for the residential system, corresponding to Fig. 2, are:

$$
\begin{array}{r}
p_{m}^{c}(k)=d_{m}^{c}(k)+g_{m}^{c}(k)+u_{m}^{c}(k) \\
q_{m}^{c}(k)=e_{m}^{c}(k)+v_{m}^{c}(k)
\end{array}
$$

for all $k \in \mathcal{K}$. Next we consider a battery with charging and discharging constraints (in kW ) given by

$$
-\underline{u} \leq u_{m}^{c}(k) \leq \bar{u}, \quad \forall k \in \mathcal{K}
$$

where $\underline{u}$ is the maximum discharging constraint and $\bar{u}$ is the maximum charging constraint. The battery charge level $s_{m}^{c}(k)$ (in kWh ) at time $k \Delta$ is given by:

$$
s_{m}^{c}(k)=s_{0}+\sum_{i=1}^{k} u_{m}^{c}(i) \Delta, \quad \forall k \in \mathcal{K}
$$

where $s_{0}$ is the initial charge level. The battery charge level is limited by the energy capacity $\bar{s}$ (in kWh ) as:

$$
0 \leq s_{m}^{c}(k) \leq \bar{s}, \quad \forall k \in \mathcal{K}
$$

We also restrict the charge level of the battery at the end of $[0, T]$ by

$$
s_{m}^{c}(K)=s_{f}
$$

where $s_{f}$ is the final charge level (in kWh ). Furthermore, the dispatchable reactive power $v_{m}^{c}$ is constrained independently from the dispatchable real power $u_{m}^{c}$. In practice, this can be achieved by over-sizing the battery inverter or requesting reactive power from the PV system [13]. That is, $v_{m}^{c}$ can represent the dispatchable reactive power from one or more inverter in a residential system. The dispatchable reactive resource is limited by

$$
-\underline{v} \leq v_{m}^{c}(k) \leq \bar{v}, \quad \forall k \in \mathcal{K}
$$

where $\underline{v}$ is the maximum supply and $\bar{v}$ is the maximum absorption of reactive power (in kvar). Extensions to incorporate dispatchable real and reactive power from both a solar PV inverter and flexible loads are straightforward.

Next, the customer of the residential system subscribes to the financial policy of net-metering, where the customer is billed for energy consumption at the same rate as it is compensated for exported energy to the grid. With a time-of-use (TOU) pricing tariff $\eta$ (in $\$ / \mathrm{kWh}$ ), supported by the net-metering policy, the cost of energy consumption (in $\$$ ) across time interval $((k-$ 1) $\Delta, k \Delta$ ) is defined by

$$
\Psi_{m}^{c}(k):=\eta(k) p_{m}^{c}(k) \Delta
$$

With the net-metering policy, the corresponding financial savings provided by the battery across $[0, T]$ are shown in [27] to be simply

$$
\Gamma_{m}^{c}=-\sum_{k \in \mathcal{K}} \eta(k) u_{m}^{c}(k) \Delta
$$

That is, we consider the net-metering policy as in [9], [27], however, extensions to other policies and tariff structures are possible.

## PRoblem Formulation

In this section we propose a local optimization-based approach for dispatching real and reactive power from a residential battery system. Our proposed L-QP approach is designed to enhance voltage regulation and reduce grid resistive losses, while increasing financial savings that accrue to a customer. Our proposed L-QP approach incorporates physics-based models of the grid, and relies on measurements collected at the customers premise (i.e., within the residential system as per Fig. 2). In what follows we derive voltage deviation and power loss equations, which support the formulation of the L-QP optimization problem. To reduce notational overhead, we omit the time index $(k)$ in the following equations.

## A. Voltage Deviation Equations

Following on from (6), the voltage deviation at node $m$ relative to node 0 can be written as:

$$
E_{m}=2 \sum_{n \in \mathcal{N}}\left(R_{m n} P_{n}+X_{m n} Q_{n}\right)
$$

where $R_{m n}$ and $X_{m n}$ are defined in (5). Next expand (16),

$$
\begin{aligned}
& E_{m}=2\left(R_{m m} p_{m}^{c}+X_{m m} q_{m}^{c}\right) \\
& +2 \sum_{\substack{i \in \mathcal{C}_{m} \\
i \neq c}}\left(R_{m m} p_{m}^{i}+X_{m m} q_{m}^{i}\right)+2 \sum_{\substack{n \in \mathcal{N} \\
n \neq m}}\left(R_{m n} P_{n}+X_{m n} Q_{n}\right)
\end{aligned}
$$

and rewrite (16) as follows

$$
E_{m}=E_{m}^{c}+E_{m}^{C}+E_{m}^{N}
$$

where

$$
\begin{aligned}
& E_{m}^{c}=2\left(R_{m m} p_{m}^{c}+X_{m m} q_{m}^{c}\right) \\
& E_{m}^{C}=2 \sum_{\substack{i \in \mathcal{C}_{m} \\
i \neq c}} R_{m m} p_{m}^{i}+X_{m m} q_{m}^{i} \\
& E_{m}^{N}=2 \sum_{\substack{n \in \mathcal{N} \\
n \neq m}} R_{m n} P_{n}+X_{m n} Q_{n}
\end{aligned}
$$

Here $E_{m}^{c}$ represents the voltage deviation attributed to customer $c, E_{m}^{C}$ represents the voltage deviation attributed to other customers connected to node $m$, and $E_{m}^{N}$ represents the voltage deviation attributed to other nodes along the circuit.

Next we denote by $\widetilde{E}_{m}^{c}$ the extended voltage deviation, which is defined by

$$
\widetilde{E}_{m}^{c}:=E_{m}^{c}+\rho_{m}^{c}\left(E_{m}^{C}+E_{m}^{N}\right)
$$

where $\rho_{m}^{c} \geq 0$ is a parameter termed the extension coefficient. If $\rho_{m}^{c}=1$, equation (18) is identical to (17). If $\rho_{m}^{c}=0$ the extended voltage deviation, $\widetilde{E}_{m}^{c}$, is representative of voltage deviation stemming from residential system $c$ itself. It is worth mentioning that in distribution grids with many nodes and customers, voltage deviation caused by a single customer is much smaller than the combined voltage deviation associated with all other customers and nodes. Consequently, we approximate from (17) that

$$
E_{m} \approx E_{m}^{C}+E_{m}^{N}
$$

We then approximate the extended voltage deviation, $\widetilde{E}_{m}^{c}$, by

$$
\widetilde{E}_{m}^{c} \approx E_{m}^{c}+\rho_{m}^{c}\left(E_{m}\right)
$$

We then expand (20) as follows

$$
\widetilde{E}_{m}^{c} \approx 2\left(R_{m m} p_{m}^{c}+X_{m m} q_{m}^{c}\right)+\rho_{m}^{c}\left(V_{0}^{2}-V_{m}^{2}\right)
$$

Assuming the voltage at the substation, $V_{0}$, is fixed and known, and the impedance of the path, $R_{m m}$ and $X_{m m}$, is also fixed and known, the extended voltage deviation $\widetilde{E}_{m}^{c}$ in (21) can be computed from measurements within the residential system $c$ (i.e., from the measurement of $p_{m}^{c}, q_{m}^{c}$, and $V_{m}$ ) as per Fig. 2. Or otherwise, $V_{0}$ in (21) represents the nominal voltage magnitude of the network.

The voltage deviation $\left(V_{0}^{2}-V_{m}^{2}\right)$ in (21) encapsulates the impact of other customers, from everywhere in the network, on node $m$. In practice, such deviation can be much larger than the voltage regulation capacity of the residential battery system. In such cases, a large extension coefficient $\rho_{m}^{c}$ (e.g. $\rho_{m}^{c}=1$ ) might result in voltage deviations beyond the battery capacity for voltage regulation, whereas a small extension coefficient (e.g. $\rho_{m}^{c}=0$ ) might result in insufficient voltage regulation from the battery system. As such, we design the extension coefficient $\rho_{m}^{c}$ to scale voltage deviation to an appropriate size in the context of the regulation capacity of the residential battery system.

In what follows, we present our approach to designing the extension coefficient $\rho_{m}^{c}$. First, we define the voltage regulation capacity $\left(\bar{E}_{m}^{c}\right)$ of a customer by

$$
\bar{E}_{m}^{c}:=2\left(R_{m m} \bar{u}+X_{m m} \bar{v}\right)
$$

Here $\bar{E}_{m}^{c}$ represents the extent that the battery is able to reduce the voltage (i.e. reduce voltage rise). In (22), we include the maximum real and reactive power limits of the battery, $\bar{u}$ and $\bar{v}$, respectively, and the network impedances $R_{m m}$ and $X_{m m}$. Importantly, it is straightforward to represent the capacity of the battery to raise the voltage (e.g. in cases of steady-state voltage drop), by replacing $\bar{u}$ and $\bar{v}$ with $\underline{u}$ and $\underline{v}$, respectively, in (22). Next we define a voltage deviation threshold denoted by $E_{t}$,

$$
E_{t}:=V_{r}^{2}-V_{t}^{2}
$$

where $V_{r}$ is the nominal voltage magnitude of the distribution circuit and $V_{t}$ is the voltage magnitude threshold. Specifically, the voltage magnitude threshold, $V_{t}$, represents either the maximum or the minimum voltage magnitude limit for the network, e.g., 1.10 or 0.90 p.u. Next we compute the parameter $\rho_{m}^{c}$,

$$
\rho_{m}^{c}=\left|\frac{\bar{E}_{m}^{c}}{E_{t}}\right|
$$

Computing the extension coefficient as in (24) enables the battery to regulate the local grid voltage in accordance with its capacity $\bar{E}_{m}^{c}$.

## B. Grid Resistive Power Loss Equations

Here we derive power loss expressions for a distribution circuit that can be computed by a customer using behind-the-meter measurements. It's worth mentioning that even though power losses are neglected in the LinDistFlow equations, it is still possible to approximate power losses with the linear equations as in [28].
Let's consider the path $\mathcal{L}_{m} \subseteq \mathcal{E}$ connecting the substation bus to node $m$, where customer $c$ is connected. The resistive power loss in the path $\mathcal{L}_{m} \subseteq \mathcal{E}$ can be calculated as

$$
L_{m}=\sum_{(h, k) \in \mathcal{L}_{m}} r_{h k} I_{h k}^{2}
$$

where $I_{h k}$ is the current magnitude flowing in the line segment $(h, k)$. The current magnitude can be written in terms of power and voltage as in [28],

$$
L_{m} \approx \sum_{(h, k) \in \mathcal{L}_{m}} r_{h k} \frac{\left(P_{h k}^{2}+Q_{h k}^{2}\right)}{V_{h}^{2}}
$$

We further approximate the resistive losses by assuming the voltage $V_{h}^{2}$ is approximately equal to the nominal $\left(V_{h}^{2} \approx V_{r}^{2}\right)$ [28], yielding:

$$
L_{m} \approx \sum_{(h, k) \in \mathcal{L}_{m}} \frac{r_{h k}}{V_{r}^{2}}\left(P_{h k}^{2}+Q_{h k}^{2}\right)
$$

The power flow in line segment $(h, k) \in \mathcal{L}_{m}$ that is not delivered to customer $c$ is given by

$$
\widetilde{P}_{h k}=\sum_{\substack{i \in \mathcal{C}_{m} \\ i \neq c}} p_{m}^{i}+\sum_{\substack{n \in \mathcal{N}: \mathcal{L}_{n} \supseteq(h, k) \\ n \neq m}} P_{n}
$$

and similar for the reactive power $\left(\widetilde{Q}_{h k}\right)$. We now rewrite (27) as follows

$$
L_{m} \approx \sum_{(h, k) \in \mathcal{L}_{m}} \frac{r_{h k}}{V_{r}^{2}}\left(\left(p_{m}^{c}+\widetilde{P}_{h k}\right)^{2}+\left(q_{m}^{c}+\widetilde{Q}_{h k}\right)^{2}\right)
$$

Next, expand and simplify (29), and rewrite the resistive power loss in the path $\mathcal{L}_{m}$ by

$$
L_{m} \approx L_{m}^{c}+L_{m}^{b}+L_{m}^{x}
$$

where

$$
\begin{gathered}
L_{m}^{c}=\frac{R_{m m}}{V_{r}^{2}}\left(\left(p_{m}^{c}\right)^{2}+\left(q_{m}^{c}\right)^{2}\right) \\
L_{m}^{b}=\frac{2}{V_{r}^{2}} \sum_{(h, k) \in \mathcal{L}_{m}} r_{h k}\left(p_{m}^{c} \widetilde{P}_{h k}+q_{m}^{c} \widetilde{Q}_{h k}\right) \\
L_{m}^{x}=\frac{1}{V_{r}^{2}} \sum_{(h, k) \in \mathcal{L}_{m}} r_{h k}\left(\widetilde{P}_{h k}^{2}+\widetilde{Q}_{h k}^{2}\right)
\end{gathered}
$$

Importantly, $L_{m}^{c}$ is the resistive power loss related only to residential system $c$, whereas $L_{m}^{b}$ and $L_{m}^{x}$ incorporate the external customers and nodes. Assuming that $R_{m m}$ and $V_{r}$ are fixed and known, $L_{m}^{c}$ in (31) can be computed by customer $c$ using behind-the-meter measurements (see Fig. 2).

## L-QP: Local Optimization-Based Approach

To dispatch real and reactive power from the battery system we propose an optimization-based approach termed L-QP. Our L-QP objectives are threefold: (i) reduce energy consumption cost for the customer; (ii) reduce grid voltage deviations; and
(iii) reduce power losses across the electric grid. The optimization problem is formulated to reduce these three terms across the entire time window $[0, T]$. Specifically, we formulate the optimization problem by

$$
\begin{aligned}
\min _{\substack{u_{m}^{c}, p_{c}^{c} \\
v_{m}^{c}, q_{m}^{c}, \tilde{E}_{m}^{c}}} & \sum_{k \in \mathcal{K}} \Psi_{m}^{c}(k)+\sigma(k)\left(\widetilde{E}_{m}^{c}(k)\right)^{2} \Delta+\zeta(k) L_{m}^{c}(k) \Delta \\
\text { s.t. } & (7),(8),(9),(10),(11),(12),(13),(21)
\end{aligned}
$$

where $\Psi_{m}^{c}(k)$ is as in (14), $\widetilde{E}_{m}^{c}(k)$ is as in (21), $L_{m}^{c}(k)$ is as in (31), and $\sigma(k), \zeta(k)$ are design parameters.

In more detail, $L_{m}^{c} \Delta$ represents the energy loss (in kWh ) along the path $\mathcal{L}_{m}$ and $\Psi_{m}^{c}$ is the cost of energy consumption for customer $c$ at node $m$. Design parameters $\sigma(k), \zeta(k)$ are selected to balance reductions in energy consumption cost against improvements in voltage regulation and reductions in grid power losses. Specifically, reductions in the Euclidean distance of the voltage deviation in either direction (e.g., voltage rise or drop) are regulated by the design of $\sigma(k)$, and reductions in grid power losses are regulated by the design of $\zeta(k)$. It is worth mentioning that careful selection of design parameters $\sigma(k)$, $\zeta(k)$ will support both reductions to voltage deviations and power losses without significantly reducing the financial savings accrued by the customer. Extensions to include a method for selecting $\sigma(k)$ and $\zeta(k)$ are possible. Since the loss term in (32) is an energy value representing the losses in the grid associated only with customer $c$, parameter $\zeta(k)$ can be computed based on the energy price. Similarly, in a scenario in which customers are compensated for their contribution on voltage, parameter $\sigma(k)$ can represent the price for voltage regulation.

The constraints in (32) include battery constraints, the power balance equation, and the proposed extended voltage deviation equation based on the LinDistFlow model. In the process of solving (32), we obtain the real $\left(u_{m}^{c}\right)$ and reactive $\left(v_{m}^{c}\right)$ battery power to be dispatched across time window $[0, T]$. The optimization problem (32) is solved by a residential customer, with knowledge of network impedances, and informed by their (local) behind-the-meter measurements (see Fig. 2). Importantly, the optimization problem in (32) can be cast as a quadratic program (QP) for which there are many commercially available solvers.
In cases where the network topology in a distribution grid changes, updates to $R_{m m}$ and $X_{m m}$ are potentially required for customers connected to nodes along the path $\mathcal{L}_{m}$. In such cases, customers along the path $\mathcal{L}_{m}$ will still operate inverters according to the $\mathrm{L}-\mathrm{QP}$ formulation, to drive measured supply voltages towards the nominal ahead of updates to $R_{m m}$ and $X_{m m}$.

## Benchmark Approach With Droop-Based Volt-Var Control

We introduce an important benchmark approach to assess the effectiveness of our proposed L-QP algorithm. Here, the real power of the battery storage is dedicated to maximize financial savings for the customer, whereas the reactive power is dedicated to voltage regulation. We consider an optimization problem equivalent to [9], [27] for charging/discharging the battery across

![](https://cdn.mathpix.com/cropped/2024_08_27_654167e472f5bf5a26b5g-06.jpg?height=380&width=871&top_left_y=213&top_left_x=1044)

Fig. 3. Droop-based volt-var function, with reactive power as a percentage of the nameplate apparent power rating for an inverter [29].
$[0, T]$. Specifically, the optimization problem is

$$
\begin{aligned}
\min _{u_{m}^{c}, p_{m}^{c}} & \sum_{k \in \mathcal{K}} \Psi_{m}^{c}(k) \\
\text { s.t. } & (7),(9),(10),(11),(12)
\end{aligned}
$$

The optimization (33) minimizes the energy consumption costs for the customer, subject to battery constraints and the power balance equation. In the process of solving (33) we obtain the battery schedule for real power dispatch $\left(u_{m}^{c}\right)$ across $[0, T]$.

Next, to dispatch reactive power of the battery system, we consider the volt-var droop curve in accordance with the IEEE Standard 1547 [29]. Droop-based volt-var control has been considered in [5], [8], [17] and is also a mandatory control requirement for new connections of battery storage in several real-world distribution networks [30], [31]. Fig. 3 illustrates the droop-based volt-var function that we incorporate in the benchmark approach for dispatching reactive power. In this paper, we adopt the default volt-var droop function for distribution networks with a high penetration of distributed resources as per [29]. The maximum reactive power is $44 \%$ of the apparent power rating of the inverter as per the standard in [29]. Note that volt-var droop functions that have a steeper slope, and a smaller dead-band, potentially provide enhanced voltage regulation and reduce network losses

It is worth mentioning that locally regulating the grid voltage, without coordinating the response of customers along a feeder, as in both volt-var and our proposed L-QP approach, potentially creates adverse interactions between controllers as reported in [17], [29], [32]-[38]. Adverse interactions between controllers is underpinned by a number of factors, including the network impedance and the location of inverters in the network, the operating state of the system, and the number and size of inverters along a feeder [17], [29], [32]-[36]. Approaches proposed in the literature to avoid potential controller interactions include: (i) increasing or decreasing inverter response times to avoid potential interactions [32], [33], [35]; (ii) the careful placement of inverters along a feeder so as to critically dampen or avoid adverse inverter interactions [36]; and (iii) the careful design of control parameters for local controllers located along a feeder so as to reduce the potential occurrence of adverse interactions [17], [29], [34], [37], [38].

![](https://cdn.mathpix.com/cropped/2024_08_27_654167e472f5bf5a26b5g-07.jpg?height=404&width=871&top_left_y=217&top_left_x=145)

Fig. 4. The IEEE 13 Node Test Feeder, where boxes represent the number of residential customers connected to the phases of each node.

## NUMERICAL SIMULATIONS

In Fig. 4 a single line diagram of the IEEE 13 Node Test Feeder (IEEE 13NF), a three-phase distribution network, is depicted. In our numerical simulations the IEEE 13 NF is selected for the voltage regulation challenges it presents - stemming from being highly loaded, unbalanced, and its inclusion of mutual line impedances [23], [39]. We assign slack bus 650 as node 0 , with a fixed and nominal voltage magnitude $V_{0}=V_{r}=1$ p.u. The nominal line-to-ground voltage is 2.4 kV , and the voltage threshold, $V_{t}$, is 1.10 p.u. The IEEE 13NF includes a transformer between nodes 633 and 634, allowing for an analysis across both the primary and secondary side of the transformer.

We modify the IEEE 13NF by removing the voltage regulator transformer and the capacitors, and in this way we exacerbate underlying over-voltage and under-voltage conditions that the residential battery systems are designed to regulate. In the modified IEEE 13NF we connect 1,503 residential systems, where each residential system is connected to a phase at each of the nodes, as illustrated in Fig. 4.

Each residential system includes real time-varying load and PV generation data obtained from one of the 100 de-identified customers [24], with average power values reported in 5-min intervals. Specifically, we replace the fixed load in the IEEE 13NF with time-varying load and PV generation data, where the substitution of aggregate customer load data at each node is approximately equal to the original fixed load values (with respect to the peak load conditions). Each customer is connected to a single-phase and we use the constant power load characteristic. Reactive loads are obtained by using the original IEEE 13NF power factor for each phase at each node.

In our numerical simulations, we also consider the more extensive IEEE 123 Node Test Feeder (IEEE 123NF). For the IEEE 123 NF , we apply the same methodology described to populate the IEEE 13NF with real time-varying data, which corresponds to the inclusion of 1,145 residential systems.

It's worth mentioning that customers connected to different phases of the same node measure the voltage magnitude for the respective phase. The residential battery is thus dispatched according to the voltage measurements for the respective phase. Accordingly, $R_{m m}$ and $X_{m m}$ is composed of the self-resistance and self-reactance, respectively, of the line segments of the respective phase. For the IEEE 13 NF , the R/X ratio of paths range from 0.32 to 0.58 , and for the IEEE 123 NF the $\mathrm{R} / \mathrm{X}$ ratio of paths range from 0.42 to 0.86 . As per the IEEE test feeder documentation [39], the power factor for all residential loads connected to the IEEE 13 NF range from 0.75 to 0.93 , with a mean load power factor of 0.86 . The loads on the IEEE 123NF have a power factor ranging from 0.80 to 0.91 , with a mean load power factor of 0.87

In what follows, we assume each customer has a solar PV system, and $30 \%$ of customers have a battery storage system. In our numerical simulations, we focus on the distinctive impact of the battery operation on the network and assume the PV inverters do not operate according to a volt-var control strategy. Customers with a battery storage system schedule their battery power flows for the day-ahead, i.e., $T=24 \mathrm{~h}$. We consider a $5 \mathrm{~kW}, 10 \mathrm{kWh}$ residential battery $(\underline{u}=\bar{u}=5 \mathrm{~kW}$ and $\bar{s}=10 \mathrm{kWh})$ and a 6 kVA inverter. The dispatchable reactive power limit is 3.3 kvar $(\underline{v}=\bar{v}=3.3$ kvar). We set the battery charge level at the end of the day equal to the charge level at the beginning of the day, i.e., $s_{0}=s_{f}=2 \mathrm{kWh}$.

The distributor serving the 100 de-identified customers reported in the dataset (described more fully in [24]) has published a TOU tariff $\eta$ [40] which we use in our simulations. Specifically, $\eta(k)=0.032$ from midnight to 7 am and from 10 pm to midnight, $\eta(k)=0.065$ from 9 am to 5 pm and from 8 pm to 10 pm and $\eta(k)=0.144$ from 7 am to 9 am and 5 pm to 8 pm . We assume each day begins at midnight, and the day-ahead load, PV generation and voltage forecasts (with uncertainty) are computed using the procedure described in [11]. Note that we use a three-phase, non-linear, full power flow model based on the current injection method [41] to simulate the respective IEEE test feeders, enabling a comprehensive analysis and benchmark for the L-QP approach. That is, the L-QP approach incorporates a linear approximation of the power flow equations, and in the numerical simulations we assess our results against the full non-linear power flow equations for the respective test feeders.

In our numerical simulations, the simulation time step is 5 minutes (i.e., $\Delta=5 / 60 \mathrm{~h}$ and $K=288$ ). Using an Intel Core i7-8700 CPU @ 3.20 GHz , it takes approximately 2 seconds to solve the L-QP with the MATLAB solver quadprog.

Next, we carefully select our design parameters $\sigma$ and $\zeta$. Specifically, we select $\zeta(k)$ to reflect the energy price in $\$ / \mathrm{kWh}$, i.e., $\zeta(k)=\eta(k), \forall k \in \mathcal{K}$. To prioritize earnings for customers, let $\sigma(k)=0.01, \forall k \in \mathcal{K}$. For the IEEE 13NF, coefficient $\rho_{m}^{c}$ ranges from 0.003 to 0.011 , and for the IEEE $123 \mathrm{NF}, \rho_{m}^{c}$ ranges from 0.0007 to 0.014 . In what follows, we consider the L-QP approach and the benchmark approach, in the context of network voltages, network losses, and customer daily operational savings.

## A. Assessing Utility and Customers Benefits

In Fig. 5 we present real and reactive power of load, PV and battery storage for a residential system connected to node 675 in the IEEE 13NF. In Fig. 5(a,b) we present real and reactive power, respectively, according to our benchmark approach. In Fig. 5(c,d) we present real and reactive power, respectively, according to our proposed L-QP approach.

![](https://cdn.mathpix.com/cropped/2024_08_27_654167e472f5bf5a26b5g-08.jpg?height=777&width=1725&top_left_y=202&top_left_x=150)

Fig. 5. Real and reactive power of load, solar PV and battery storage in a residential system connected at node 675 phase C along the IEEE 13NF. (a) Real and (b) reactive power for the benchmark approach. (c) Real and (d) reactive power for the proposed L-QP approach.

![](https://cdn.mathpix.com/cropped/2024_08_27_654167e472f5bf5a26b5g-08.jpg?height=348&width=872&top_left_y=1118&top_left_x=125)

Fig. 6. Voltage magnitude envelopes for the entire IEEE 13NF. The baseline voltage envelope represents the case where no customer installs a battery.

In Fig. 5(a) we observe that our benchmark approach results in real power of the battery that is solely determined by the TOU tariff, whereas in Fig. 5(b) we observe that the battery reactive power is essentially proportional to the local voltage. In Fig. 5(c) we observe that the L-QP approach results in battery real power that is also influenced by the TOU tariff, as we prioritized savings for customer in (32). We further observe that the battery charges when PV generation peaks, resulting in reduce real power exports from the customer which potentially reduces grid resistive losses. In Fig. 5(d), we observe reactive power is dispatched to support voltage regulation but it is not solely a function of the local voltage, since real and reactive power are coupled for voltage regulation as in (21).
In Fig. 6 we present voltages envelopes for the IEEE 13NF considering all phases of all nodes across the feeder - excluding node 650 (the slack bus). Each envelope represents the range between the maximum and the minimum voltage magnitude across the network at each time step. In Fig. 6 the baseline envelope represents the case where no customer along the feeder has a battery (i.e., $\bar{s}=\underline{v}=\bar{v}=0$ for all customers). In Fig. 6 we observe that the baseline envelope encompasses two significant voltage drops at 08:00 and again at 20:00, which coincides

![](https://cdn.mathpix.com/cropped/2024_08_27_654167e472f5bf5a26b5g-08.jpg?height=342&width=871&top_left_y=1134&top_left_x=1044)

Fig. 7. Grid resistive power losses across a day for the entire IEEE 13NF. Our baseline represents the case where no customer installs a battery.
with peak demand across the feeder. Furthermore, we observe voltage rise occurs at 12:00, which is also coincident with peak PV production across the feeder. In contrast, the proposed L-QP approach significantly reduces voltage deviations from the nominal in comparison with both the baseline and the benchmark approach.

In Fig. 7 we present the grid resistive power losses across the day, where the baseline approach represents the situation where no customer has installed a battery. We observe that in all three approaches, Baseline, Benchmark and L-QP, the most significant losses occur during the middle of the day when PV generation peaks. During peak PV generation, large quantities of real power $\left(P_{m n}\right)$ flow back along line segments resulting in significant power losses across the network, in accordance with (26). We also observe that the proposed L-QP approach offers a greater reduction in peak power losses, a result of charging of batteries during peak PV generation.

In Table I we present a summary of numerical simulations that were carefully curated to be representative of summer and winter days, considering sunny and cloudy conditions - where the load and PV generation profiles vary considerably. More specifically, the selected days were carefully curated to be representative of

TABLE I
FinANCIAL SAVINGS, ENERGY LOSSES AND VOLTAGE ENVELoPES FOR THE IEEE 13NF

| Day | Baseline | Benchmark | L-QP (Set 1) |
| :---: | :---: | :---: | :---: |
| Summer | N/A | $\$ 1.912$ | $\$ 1.890$ |
|  | 1609 kWh | 1348 kWh | 1261 kWh |
|  | $1.07-0.90 \mathrm{p.u}$. | $1.04-0.94 \mathrm{p.u}$. | $1.01-0.96 \mathrm{p.u}$. |
| Summer | N/A | $\$ 1.912$ | $\$ 1.904$ |
| Cloudy Day | 968 kWh | 847 kWh | 768 kWh |
|  | $1.06-0.91 \mathrm{p.u}$. | $1.04-0.94 \mathrm{p.u}$. | $1.01-0.96 \mathrm{p} . \mathrm{u}$. |
| Winter | N/A | $\$ 1.912$ | $\$ 1.843$ |
|  | 1565 kWh | 1045 kWh | 810 kWh |
|  | $1.02-0.81 \mathrm{p.u}$. | $1.01-0.88 \mathrm{p.u}$. | $1.02-0.91 \mathrm{p} . \mathrm{u}$. |
| Winter | N/A | $\$ 1.912$ | $\$ 1.829$ |
|  | 1569 kWh | 1184 kWh | 979 kWh |
|  | $1.00-0.83 \mathrm{p} . \mathrm{u}$. | $1.00-0.90$ p.u. | $1.01-0.91 \mathrm{p} . \mathrm{u}$. |

TABLE II
FinANCIAL SAVINGS, ENERGY LOSSES AND VOLTAGE ENVELOPES FOR THE IEEE 123NF

| Day | Baseline | Benchmark | L-QP (Set 1) |
| :---: | :---: | :---: | :---: |
| Summer | N/A | $\$ 1.912$ | $\$ 1.889$ |
|  | 713 kWh | 689 kWh | 669 kWh |
|  | $1.04-0.94$ p.u. | $1.03-0.95 \mathrm{p} . \mathrm{u}$. | $1.02-0.97$ p.u. |
| Winter | N/A | $\$ 1.912$ | $\$ 1.822$ |
|  | 943 kWh | 779 kWh | 571 kWh |
|  | $1.01-0.89$ p.u. | $1.00-0.93$ p.u. | $1.00-0.95$ p.u. |

extreme cases, where large voltage deviations and power losses are prevalent throughout the network. Note that the first selected day (Summer Sunny Day) summarizes the results previously presented in Figs. 5-7.

In Table I we present the maximum and minimum voltage magnitude and the total energy loss across the IEEE 13NF, in addition to the average savings per customer provided by batteries on that day. The average savings are calculated as the average of $\Gamma_{m}^{c}$ in (15) for all customers with battery storage. We observe that both the benchmark and the L-QP approaches provide savings for customers and reduce the grid losses from the reported baseline. The benchmark approach provided a maximum savings of $\$ 1.912$ on all selected days, whereas the proposed L-QP approach reduced grid power losses and provided significant voltage improvement at a marginal cost to the customer (e.g., savings reduced from $\$ 1.912$ to $\$ 1.829$ on the Winter Cloudy Day).

In Table II, we present a summary of the numerical simulations completed with the IEEE 123NF. Specifically, we carefully consider the two most extreme days, and we observe that in this larger-scale distribution network the L-QP approach reduces voltage deviations and resistive losses when compared to the baseline and the benchmark. The numerical simulation for the L-QP approach are completed within 2 seconds, for each customer, consistent with the reported simulation time for the IEEE 13 NF .

In Fig. 8 we present voltage envelopes for the Summer Sunny Day for the IEEE 13NF, considering the L-QP approach with three different sets of weights as reported in Table III. Note that Set 1 is consistent with our previous numerical simulations, whereas Set 2 considers a larger weight for grid losses $(\zeta)$ and Set 3 considers a larger weight for both grid voltage $(\sigma)$ and grid losses $(\zeta)$. That is, we carefully select our three sets of

![](https://cdn.mathpix.com/cropped/2024_08_27_654167e472f5bf5a26b5g-09.jpg?height=337&width=882&top_left_y=213&top_left_x=1052)

Fig. 8. Voltage magnitude envelopes for the IEEE 13NF with three sets of L-QP weights.

TABLE III
INTRODUCING THREE SETS: L-QP DESIGN PARAMETERS

|  | Set 1 | Set 2 | Set 3 |
| :---: | :---: | :---: | :---: |
| Design parameters: $\sigma, \zeta$ | $0.01, \eta$ | $0.01,10^{3}$ | $1,10^{3}$ |
| Average savings | $\$ 1.890$ | $\$ 0.492$ | $\$ 0.511$ |
| Total energy losses | 1261 kWh | 1082 kWh | 1090 kWh |

weights for our simulations, with extension to systematic tuning possible. In Fig. 8 and Table III we observe that, according to the change in priority, Set 2 considerably reduced grid energy loss compared to Set 1, while decreasing savings and voltage regulation performance. Set 3 resulted in improved grid voltage and losses compared to Set 1 , while providing lower savings. In Table III we also observe that by including the loss term in the L-QP approach we reduce power losses across the network. That is, by removing the loss term from the L-QP optimization in (32), i.e. $\zeta(k)=0$, the energy losses across the network increase to 1411 kWh .

Prioritizing voltage and loss terms in (32), as with Set 3, shifts the battery real power flows from a trajectory guided by the TOU tariff to a trajectory that directly reduces both grid voltage deviation from the nominal and feeder losses. We observed that the coupled action of real and reactive power intensifies voltage regulation performance with the L-QP approach, however, the average savings per customer fell to around $\$ 0.50$ per day. In this context, financially compensating customers for their grid voltage regulation services and for reducing feeder losses could potentially create greater benefits for both the customer and utility.

## B. Interaction Between Inverters

This section presents numerical simulations to illustrate the effect of coefficient $\rho_{m}^{c}$ on the grid voltage stability due to interactions between inverters. Analogous to the gain in a proportional controller or the droop slope in the volt-var control, coefficient $\rho_{m}^{c}$ has direct influence on stability, convergence rate and steady-state voltage deviation of the system. We consider a single-phase two-node network with two batteries alternately updating their output for grid voltage regulation with the L-QP approach. In this simulation, customers have enough resources to fully minimize the voltage regulation term $\left(\widetilde{E}_{m}^{c}\right)^{2}$ in (32).

Fig. 9 depicts the grid voltage deviation behavior for different values of coefficient $\rho_{m}^{c}$. In Fig. 9(a) we observe that $\rho_{m}^{c}>1$ resulted in ever-increasing voltage deviation (unstable system);
![](https://cdn.mathpix.com/cropped/2024_08_27_654167e472f5bf5a26b5g-10.jpg?height=388&width=871&top_left_y=214&top_left_x=126)
(b)

Fig. 9. Grid voltage deviation for different values of the extension coefficient $\rho_{m}^{c}$. Effect of the coefficient $\rho_{m}^{c}$ on (a) voltage stability and (b) on convergence rate and steady-state voltage deviation.
$\rho_{m}^{c}=1$ resulted in a sustained interaction between inverters (marginally stable system); and $\rho_{m}^{c}<1$ resulted in a convergent grid voltage (stable system). In Fig. 9(b) we observe that smaller coefficient values reduce interactions between inverters, whereas larger values reduce steady-state voltage deviation.

Analogous to other local (fully decentralized) approaches [37], [38], coefficient $\rho_{m}^{c}$ can be adjusted to balance convergence rate and steady-state voltage deviation. In (24) coefficient $\rho_{m}^{c}$ is computed according to the voltage regulation capacity of the battery storage. However, in case of significant interactions between local controllers, there can be a tuning-down factor in (24) that reduces $\rho_{m}^{c}$ proportionally to the battery regulation capacity. A similar strategy is proposed in [37] to adaptively adjust the coefficients of the local volt-var control. Alternatively, analytical investigation of coefficient $\rho_{m}^{c}$ can provide further insights on its relation with convergence and steady-state voltage deviation. Such a strategy is undertaken in [38], where a convex optimization problem is formulated to obtain the coefficients of a fully decentralized approach to minimize voltage deviation while ensuring system stability.

## CONCLUSION

Approaches separating real power for economic purposes and reactive power for voltage regulation have their fundamental limitations in distribution networks. In this paper, we proposed a local optimization-based approach, L-QP, that enables both real and reactive power coupled for grid voltage regulation and loss reduction, while considering the financial savings for the battery owner. With a small reduction in the financial savings that accrue to customers, our proposed approach has shown higher technical performance in simulation in terms of grid voltage regulation and reduced power losses across a feeder. By carefully selecting the design parameters for enhanced voltage regulation and further feeder loss reduction, we observed in simulation residential batteries operated according to the proposed L-QP approach offered significant opportunities for improved grid operations. Future work to consider a comprehensive assessment of battery degradation, the systematic tuning of $\sigma$ and $\zeta$, and a detailed investigation into interaction between local controllers, is possible.

## ACKNOWLEDGMENT

The authors would like to thank Jaimie Swartz for her insightful comments.

## REFERENCES

- [1] B. Palmintier, "On the path to sunshot: Emerging issues and challenges in integrating solar with the distribution system," Nat. Renewable Energy Lab. (NREL), Golden, CO, Tech. Rep. NREL/TP-5D00-65331, May 2016
- [2] "Renewable integration study stage 1 appendix A: High penetrations of distributed solar PV," Australian Energy Market Operator (AEMO), Tech. Rep., Apr. 2020.
- [3] K. Petrou et al., "Limitations of residential storage in PV-rich distribution networks: An Australian case study," in Proc. IEEE Power Energy Soc. Gen. Meeting, 2018, pp. 1-5.
- [4] A. T. Procopiou, M. Z. Liu, W. Nacmanson, and L. Ochoa, "Advanced planning of PV-rich distribution networks - deliverable 4 Non-traditional solutions," The Univ. Melbourne, Tech. Rep., Aug. 2020
- [5] J. W. Smith, W. Sunderman, R. Dugan, and B. Seal, "Smart inverter volt/var control functions for high penetration of PV on distribution systems," in Proc. IEEE/PES Power Syst. Conf. Expo., 2011, pp. 1-6.
- [6] A. von Meier, E. L. Ratnam, K. Brady, K. Moffat, and J. Swartz, "Phasor based control for scalable integration of variable energy resources," Energies, vol. 13, no. 1, pp. 1-14, 2020
- [7] I. Ranaweera, O.-M. Midtgåard, and M. Korpåas, "Distributed contro scheme for residential battery energy storage units coupled with PV systems," Renewable Energy, vol. 113, pp. 1099-1110, 2017
- [8] S. Hashemi and J. Østergaard, "Efficient control of energy storage for increasing the PV hosting capacity of LV grids," IEEE Trans. Smart Grid, vol. 9, no. 3, pp. 2295-2303, May 2018
- [9] M. U. Hashmi, D. Deka, A. Bušić, L. Pereira, and S. Backhaus, "Arbitrage with power factor correction using energy storage," IEEE Trans. Power Syst., vol. 35, no. 4, pp. 2693-2703, Jul. 2020
- [10] J. von Appen, T. Stetz, M. Braun, and A. Schmiegel, "Local voltage control strategies for PV storage systems in distribution grids," IEEE Trans. Smart Grid, vol. 5, no. 2, pp. 1002-1009, Mar. 2014.
- [11] E. L. Ratnam, S. R. Weller, and C. M. Kellett, "Central versus localized optimization-based approaches to power management in distribution networks with residential battery storage," Int. J. Electr. Power Energy Syst., vol. 80, pp. 396-406, 2016.
- [12] W. C. de Carvalho, E. L. Ratnam, L. Blackhall, A. von Meier, and A. Murray, "Over-voltage disconnection of DER inverters: Assessing customer savings," IFAC-PapersOnLine 21st IFAC World Congr., vol. 53, no. 2, pp. 13230-13235, 2020
- [13] E. Yao, P. Samadi, V. W. S. Wong, and R. Schober, "Residential demand side management under high penetration of rooftop photovoltaic units," IEEE Trans. Smart Grid, vol. 7, no. 3, pp. 1597-1608, May 2016.
- [14] A. T. Procopiou, K. Petrou, L. F. Ochoa, T. Langstaff, and J. Theunissen, "Adaptive decentralized control of residential storage in PV-rich MVLV networks," IEEE Trans. Power Syst., vol. 34, no. 3, pp. 2378-2389 May 2019
- [15] Y. Wang, K. T. Tan, X. Y. Peng, and P. L. So, "Coordinated control of distributed energy-storage systems for voltage regulation in distribution networks," IEEE Trans. Power Del., vol. 31, no. 3, pp. 1132-1141, Jun. 2016.
- [16] M. Zeraati, M. E. Hamedani Golshan, and J. M. Guerrero, "Distributed control of battery energy storage systems for voltage regulation in distribution networks with high PV penetration," IEEE Trans. Smart Grid, vol. 9 no. 4, pp. 3582-3593, Jul. 2018
- [17] G. Cavraro and R. Carli, "Local and distributed voltage control algorithms in distribution networks," IEEE Trans. Power Syst., vol. 33, no. 2, pp. 1420-1430, Mar. 2018.
- [18] D. K. Molzahn et al., "A survey of distributed optimization and control algorithms for electric power systems," IEEE Trans. Smart Grid, vol. 8, no. 6, pp. 2941-2962, Nov. 2017.
- [19] J. Joo, M. Chava, M. Sankur, D. Arnold, and E. Stewart, "Model predictive control of flexible demand for voltage support in unbalanced distribution systems," in Proc. IEEE Power Energy Soc. Gen. Meeting, Chicago, IL, USA, 2017, pp. 1-5
- [20] K. E. Antoniadou-Plytaria, I. N. Kouveliotis-Lysikatos, P. S. Georgilakis, and N. D. Hatziargyriou, "Distributed and decentralized voltage control of smart distribution networks: Models, methods, and future research," IEEE Trans. Smart Grid, vol. 8, no. 6, pp. 2999-3008, Nov. 2017
- [21] M. D. Sankur, R. Dobbe, E. Stewart, D. S. Callaway, and D. B. Arnold, "A linearized power flow model for optimization in unbalanced distribution systems," pp. 1-6, Jun. 2016, arXiv:1606.04492.
- [22] M. D. Sankur, R. Dobbe, A. von Meier, E. M. Stewart, and D. B. Arnold, "Optimal voltage phasor regulation for switching actions in unbalanced distribution systems," pp. 1-11, Jun. 2019, arXiv:1804.02080.
- [23] D. B. Arnold, M. Sankur, R. Dobbe, K. Brady, D. S. Callaway, and A. von Meier, "Optimal dispatch of reactive power for voltage regulation and balancing in unbalanced distribution systems," in Proc. IEEE Power Energy Soc. Gen. Meeting, Boston, MA, USA, 2016, pp. 1-5.
- [24] M. Shaw, B. Sturmberg, L. Guo, X. Gao, E. Ratnam, and L. Blackhall, "The NextGen energy storage trial in the ACT, Australia," in Proc. 10th ACM Inter. Conf. Future Energy Syst., Phoenix, AZ, USA, 2019 pp. $439-442$.
- [25] M. Baran and F. F. Wu, "Optimal sizing of capacitors placed on a radial distribution system," IEEE Trans. Power Del., vol. 4, no. 1, pp. 735-743, Jan. 1989.
- [26] W. Lin and E. Bitar, "Decentralized stochastic control of distributed energy resources," IEEE Trans. Power Syst., vol. 33, no. 1, pp. 888-900, Jan 2018.
- [27] E. L. Ratnam, S. R. Weller, and C. M. Kellett, "Scheduling residential battery storage with solar PV: Assessing the benefits of net metering," Appl. Energy, vol. 155, pp. 881-891, 2015.
- [28] M.E. Baran and F.F. Wu, "Network reconfiguration in distribution systems for loss reduction and load balancing," IEEE Trans. Power Del., vol. 4 no. 2, pp. 1401-1407, Apr. 1989.
- [29] IEEE Standard for Interconnection and Interoperability of Distributed Energy Resources with Associated Electric Power Systems Interfaces, IEEE Standard 1547-2018 (Rev. of IEEE Standard 1547-2003), pp. 1-138, Apr. 2018, doi: 10.1109/IEEESTD.2018.8332112.
- [30] AusNet Services, "Model standing offer for basic connection services: Basic micro Embedded Generation (EG) - inverter energy system," pp. 120, Dec. 2019.
- [31] "Victorian distribution network service provider (DNSP) basic micro EG connections power quality response mode settings," p. 1, Dec. 2019
- [32] P. Jahangiri and D. C. Aliprantis, "Distributed Volt/VAr control by PV inverters," IEEE Trans. Power Syst., vol. 28, no. 3, pp. 3429-3439, Aug. 2013.
- [33] J. Schoene et al., "Investigation of oscillations caused by voltage control from smart PV on a secondary system," in Proc. IEEE Power Energy Soc. Gen. Meeting, 2017, pp. 1-5
- [34] S. Chakraborty, A. Hoke, and B. Lundstrom, "Evaluation of multiple inverter volt-VAR control interactions with realistic grid impedances," in Proc. IEEE Power Energy Soc. Gen. Meeting, Denver, CO, USA, 2015, pp. $1-5$
- [35] S. Abadi, M. Mahmoodi, P. Scott, L. Blackhall, and S. Thiebaux, "Active management of LV residential networks under high PV penetration," in Proc. IEEE Milan PowerTech, Milan, Italy, Jun. 2019, pp. 1-6.
- [36] J. Swartz, B. Wais, E. Ratnam, and A. von Meier, "Visual tool for assessing stability of DER configurations on three-phase radial networks," in Proc. IEEE Madrid PowerTech, Madrid, Spain, Jun. 2021, pp. 1-6.
- [37] A. Singhal, V. Ajjarapu, J. Fuller, and J. Hansen, "Real-time local Volt/Var control under external disturbances with high PV penetration," IEEE Trans. Smart Grid, vol. 10, no. 4, pp. 3849-3859, Jul. 2019
- [38] K. Baker, A. Bernstein, E. Dall'Anese, and C. Zhao, "Network-cognizant voltage droop control for distribution grids," IEEE Trans. Power Syst., vol. 33, no. 2, pp. 2098-2108, Mar. 2018.
- [39] W. H. Kersting, "Radial distribution test feeders," in Proc. IEEE Power Eng. Soc. Winter Meeting. Conf., Columbus, OH, USA, 2001, vol. 2, pp. $908-912$
- [40] Evoenergy, "Evoenergy electricity network prices," [Online]. Available: https://www.evoenergy.com.au/residents/pricing-and-tariffs/electricitynetwork-pricing
- [41] P. A. N. Garcia, J. L. R. Pereira, S. Carneiro, V. M. da Costa, and N. Martins, "Three-phase power flow calculations using the current injection method," IEEE Trans. Power Syst., vol. 15, no. 2, pp. 508-514, May 2000.


[^0]:    Manuscript received 9 June 2021; revised 20 October 2021 and 14 February 2022; accepted 26 March 2022. Date of publication 29 March 2022; date of current version 22 December 2022. Paper no. TPWRS-00920-2021. (Corresponding author: Wilhiam C. de Carvalho.)

Wilhiam C. de Carvalho, Elizabeth L. Ratnam, and Lachlan Blackhall are with the College of Engineering and Computer Science, Australian National University, Canberra, ACT 2601, Australia (e-mail: wilhiam.decarvalho@anu.edu.au elizabeth.ratnam@anu.edu.au; lachlan.blackhall@anu.edu.au)

Alexandra von Meier is with the Electrical Engineering and Computer Sci ence Department, University of California, Berkeley, CA 94720 USA (e-mail vonmeier@berkeley.edu).

Color versions of one or more figures in this article are available at https://doi.org/10.1109/TPWRS.2022.3163371.

Digital Object Identifier 10.1109/TPWRS.2022.3163371