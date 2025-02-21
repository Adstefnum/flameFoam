# Research Article

# Numerical Simulation of the Deflagration-to-Detonation

# Transition in Inhomogeneous Mixtures

## Florian Ettner, Klaus G. Vollmer, and Thomas Sattelmayer

```
Lehrstuhl fur Thermodynamik, Technische Universit ̈ ̈at Munchen, 85748 Garching, Germany ̈
```
```
Correspondence should be addressed to Florian Ettner; florian.ettner@gmail.com
```
```
Received 16 February 2014; Accepted 4 April 2014; Published 19 May 2014
```
```
Academic Editor: Yiguang Ju
```
```
Copyright © 2014 Florian Ettner et al. This is an open access article distributed under the Creative Commons Attribution License,
which permits unrestricted use, distribution, and reproduction in any medium, provided the original work is properly cited.
```
```
In this study the hazardous potential of flammable hydrogen-air mixtures with vertical concentration gradients is investigated
numerically. The computational model is based on the formulation of a reaction progress variable and accounts for both deflagrative
flame propagation and autoignition. The model is able to simulate the deflagration-to-detonation transition (DDT) without
resolving all microscopic details of the flow. It works on relatively coarse grids and shows good agreement with experiments.
It is found that a mixture with a vertical concentration gradient can have a much higher tendency to undergo DDT than a
homogeneous mixture of the same hydrogen content. In addition, the pressure loads occurring can be much higher. However,
theoppositeeffectcanalsobeobserved,withthedecisivefactorbeingthegeometricboundaryconditions.Themodelgivesinsight
into different modes of DDT. Detonations occurring soon after ignition do not necessarily cause the highest pressure loads. In
mixtures with concentration gradient, the highest loads can occur in regions of very low hydrogen content. These new findings
should be considered in future safety studies.
```
## 1. Introduction

Due to its potentially catastrophic consequences, the acci-
dental release of hydrogen is a major concern in process
engineering [ 1 , 2 ], power generation [ 3 – 5 ],andfutureauto-
motive concepts [ 6 , 7 ]. A small heat source can be sufficient to
initiate a deflagration that causes a sudden temperature and
pressure rise. The severity of the consequences depends on
the propagation speed of the deflagration. In general it can be
expected that the flame accelerates due to a positive feedback
loop: the expansion of the combustion products induces
motion in the unburned gas which generates turbulence and
thereby increases the burning speed of the flame. This process
is further complicated through instabilities [ 8 – 10 ], formation
of shocks, and interaction with the surrounding structure.
Under certain circumstances the deflagration can undergo
a transition to a detonation. The hazardous potential of a
detonation(andespeciallythatoftheunsteadytransition
process) is considerably higher than that of a deflagration.
Therefore, the probability of the occurrence of a
deflagration-to-detonation transition (DDT) needs to

```
be considered in safety studies involving scenarios with
accidental hydrogen release. In the past, many researchers
have contributed impressive DDT simulation studies
by applying a very high grid resolution to observe all
microscopic flow details [ 11 – 15 ]. This approach has helped a
lottounderstandtheformationofDDTbutisonlyapplicable
to very small domains. When using simple reaction models
like one-step Arrhenius kinetics, many publications can be
found using a grid resolution of 8 or less computational cells
per half-reaction length. However, it is generally agreed that
when employing one-step Arrhenius kinetics, a resolution
of at least 20 computational cells per half-reaction length
is required in inviscid flow to sufficiently resolve the flow
structure and obtain correct results for heat release profile,
flame-shock interaction, detonation cell size, and so forth
[ 16 – 18 ]. This is already challenging to achieve in large
computational domains. Even though it is often argued that
diffusive effects are negligible when simulating established
detonations, they are of importance in fast deflagrations and
the onset of detonations. Mazaheri et al. [ 19 ]showedthat
the inclusion of diffusive terms increases the required spatial
```
Hindawi Publishing Corporation
Journal of Combustion
Volume 2014, Article ID 686347, 15 pages
[http://dx.doi.org/10.1155/2014/](http://dx.doi.org/10.1155/2014/)


2 Journal of Combustion

resolution to approximately 25 to 300 computational cells
(depending on the activation energy of the mixture) per
half-reaction length. Powers and Paolucci [ 20 ] demonstrated
that when using a detailed chemical mechanism instead
of simplified kinetics, the demand for spatial resolution
increases to an order of magnitude of approximately 103 cells
per half-reaction length. Due to the enormous computational
costs, such “direct” simulations of DDT (even when using
only simplified kinetics at 20 cells per half-reaction length)
cannot be applied to large scale engineering simulations and
are expected to remain impossible for years to come. Thus,
thecurrentstateoftheartoflargescaleaccidentsimulations
(e.g., in nuclear safety studies) is as follows [ 3 , 4 ].

```
(1) Determination of spatial hydrogen distribution.
(2) Usage of empirical criteria to determine whether
DDT can occur or not.
(3) Simulation of the combustion witheithera deflagra-
tionora detonation code.
```
Step1canbeperformedwithalumpedparametercode
[ 5 ]oraCFDcode[ 21 , 22 ]. Step 2 is performed by applying
empirical criteria [ 23 , 24 ]whichhavebeenobtainedfrom
experiments in explosion tubes [ 25 – 29 ]tothegeometry
enclosing the hydrogen cloud. This step can only be per-
formed with considerable uncertainty regarding not only the
different scale and geometry (explosion tube with regular,
periodic obstacles versus intricate three-dimensional build-
ing structure), but also the fact that virtually all criteria have
been gained from experiments with perfectly homogeneous
mixtures. In accident scenarios, however, mixtures are likely
to include strong concentration gradients [ 30 , 31 ]. Step 3 can
be performed with a variety of CFD codes. While slower
deflagrations can be simulated satisfactorily with commercial
codes, simulations of fast deflagrations (where gas dynamics
have a major influence) and especially simulations of deto-
nations are usually performed more accurately with in-house
codes that are generally not made available to the public.
In an OECD report prepared by a group of experts this
“significant lack of numerical tools available to safety ana-
lysts” [ 32 ] has been criticized and the following requirements
have been identified.

```
(1) Development of approximate but reliable methods for
simulating both flame acceleration and detonation in
such a fashion that the simulation can be run within
a single software framework.
(2) Development of reliable combustion models that can
be used to model DDT without the judgment and
intervention of the simulator.
```
As the current situation is very unsatisfying, the present
study was aimed at developing a CFD solver capable of
simulating both deflagrations and detonations and especially
the transition between both regimes. While the application
of 3D computations at full reactor scale remains a long-term
objective, this project goes a first step into this direction:
the development of a solver to show the technical feasibility
of simulating DDT experiments in explosion tubes in 2D

```
without resolving the microstructure of the flow in the CFD
grid. This forms an important prerequisite for the future
simulation of flame acceleration and DDT in large, three-
dimensional domains which will necessarily be performed on
underresolved grids.
Inasecondstep,thisnewsolverisusedtoinvestigate
the influence of concentration gradients on DDT forma-
tion. While many earlier studies considered a homogeneous
mixture a worst-case scenario and consequently neglected
the role of inhomogeneities, the influence of concentration
gradients has only recently come into the focus of research
[ 29 , 33 , 34 ].
Theresultsofthisprojectareshowninthispaper.
```
## 2. Model Description

```
As the direct initiation [ 35 ] of a detonation is very unlikely,
a detonation usually occurs after a turbulent flame (defla-
gration) has accelerated to a sufficiently high velocity [ 32 ].
This deflagration-to-detonation transition is a complex phe-
nomenon including flame instabilities, interaction with tur-
bulence, and gas dynamic phenomena. With all these effects
occurring at very high Reynolds numbers, it is virtually
impossible to resolve them completely in numerical compu-
tations. However, not all phenomena occurring on micro-
scopic scale are necessarily relevant for an accurate simu-
lation of macroscopic DDT events. Thomas [ 36 ]concluded
from a comparison of experimental and numerical results
that a reliable DDT model does not have to resolve all details
of the flow. Instead, only correct turbulent burning rates, local
density increase due to shocks and the capability of giving rise
to detonations as a result of blast waves have been identified
as necessary features of an accurate DDT model.
For the present work, the CFD codeOpenFOAM[ 37 ]
has been chosen as a basis for model development. One
reason for this choice was that (contrary to many proprietary
detonation codes)OpenFOAMhas the built-in capability
of dealing with unstructured grids—a clear advantage in
view of the intended future application to sophisticated
geometries. Another reason for the usage ofOpenFOAM
was that the code is free and open source and thus also the
model developed in this project can be made available to the
scientific community at no cost.
The density-based code developed underOpenFOAM
solves the unsteady, compressible Navier-Stokes equations.
All convective fluxes are determined using the HLLC scheme
[ 38 ] with multidimensional slope limiters (“cellMDLimited”
[ 37 , 39 ]). This scheme is very suitable for the simulation of
high Mach number compressible flow as it leads to much
better shock capturing than the standard schemes used in
most pressure-based codes like the PISO scheme [ 40 ]. As
an example, the results of a 1D shock-tube calculation are
compared in Figures 1 and 2 .Theinitialdataforthisshock-
tubeproblemisanidealgaswithmolecularweight𝑀=
28.85kg/kmol and specific heat ratio𝛾 = 1.4at𝑝=10bar,
𝑇 = 800K,𝑢=0m/sfor𝑥≤0and𝑝=1bar,𝑇 = 300K,
𝑢=0m/sfor𝑥>0.Theresultsshownhavebeenobtained
on an equidistant grid with1.0mm spacing. For comparison,
```

Journal of Combustion 3

the analytical solution is displayed as a light gray line. It can
be seen fromFigure 1that the PISO scheme not only predicts
a wrong shock location (i.e., wrong propagation speed), but
also is in general very dissipative and displays overshoots at
discontinuities. This can be attributed to the nonconservative
formulation of the Navier-Stokes equations which is inherent
to the pressure-based scheme. With regard to the intended
application to transonic reactive flow (including autoignition
caused by shocks) this has to be regarded as a very critical
issue. It can be concluded that standard pressure-based
solvers are not suitable for the simulation of fast deflagrations
and detonations.
Density-based solvers, especially Riemann solvers like the
HLLC scheme employed inFigure 2,showamuchbetter
performance, producing accurate shock propagation speeds
and far less dissipation at discontinuities. Thus it was decided
to use the HLLC scheme as a basis for the DDT solver
developed in this work. The only disadvantage of the scheme
is that it does not work in very low Mach number flow.
Therefore, the PISO scheme is also implemented and can be
used to start computations in stagnant flow and then switch
totheHLLCschemeonceacombustion-inducedflowhas
developed (seeSection 3).
Realistic material properties for the reacting hydrogen-
air mixture are obtained from theChemkindatabase [ 41 ]
and molecular transport coefficients are determined using the
Sutherland correlation [ 42 ].
Combustion is described via a reaction progress variable
𝑐[ 43 ].𝑐=0corresponds to an unburned mixture, 𝑐=
1 to a completely burned mixture. Within the context of
Favre-averaging [ 44 , 45 ],̃𝑐(𝑥,𝑡)⃗ can be interpreted as the
density-weighted probability of encountering burned gas at a
particular instance of space and time. The transport equation
of the reaction progress variable reads

### 𝜕

### 𝜕𝑡

### (𝜌̃𝑐)+

### 𝜕

### 𝜕𝑥𝑗

### (𝜌̃𝑐𝑢̃𝑗)=

### 𝜕

### 𝜕𝑥𝑗

```
(𝜌𝐷eff
```
### 𝜕̃𝑐

### 𝜕𝑥𝑗

```
)+𝜔𝑐,def+𝜔𝑐,ign,
```
```
(1)
```
where the overbar denotes Reynolds-averaging and the tilde
denotes Favre-averaging. The equation contains two source
terms that account for deflagrative and detonative combus-
tion, respectively. This concept is related to the simulation of
autoignition in gas turbines or internal combustion engines
as proposed by [ 46 – 48 ].
The deflagrative source term𝜔𝑐,def is modelled using
the RANS version of the Weller combustion model [ 49 ],
extended by a factor0≤𝐺≤1[ 50 , 51 ] which takes quenching
of turbulent flames into account [ 52 ]:

```
𝜔𝑐,def=𝜌𝑢𝑠𝑇|∇𝑐̃|𝐺, (2)
```
```
𝑠𝑇=𝜉𝑠𝐿. (3)
```
𝜌𝑢isthedensityoftheunburnedmixtureand𝑠𝑇the turbulent
burning speed which is modelled as the product of the

```
laminar burning speed𝑠𝐿and a flame wrinkling factor𝜉.The
latter is obtained from a transport equation:
```
```
𝜕
𝜕𝑡
```
### (𝜌𝜉)+

### 𝜕

### 𝜕𝑥𝑗

### (𝜌𝜉𝑢̃𝑗)=

### 𝜕

### 𝜕𝑥𝑗

```
(𝜌𝐷eff
```
### 𝜕𝜉

### 𝜕𝑥𝑗

### )+𝜌𝑃𝜉𝜉−𝜌𝑅𝜉𝜉^2.

### (4)

```
Details about the expressions𝑃𝜉 and 𝑅𝜉 describing the
generation and destruction of flame surface can be found
in [ 37 , 49 ]. Due to the gradient ansatz, ( 2 )leadstocorrect
consumption rates even on underresolved grids. This means,
even if the flame thickness is smeared out over several
computational cells and thus thicker than the physical flame
brush, the overall consumption rate is not affected [ 49 , 52 ].
An adjustment of model constants to grid size or domain
geometry is not required.
Experimental values for the laminar burning speed of
hydrogen-air flames at standard conditions (temperature
𝑇 0 = 298K and pressure𝑝 0 = 1.013bar) have been published
by Konnov [ 53 ]. The dependence of flame speed on molar
hydrogen fraction𝑥H 2 canbeapproximatedasapolynomial
[ 52 ]:
```
### 𝑠𝐿,0=

### {{

### {{

### {{{

### {{

### {{

### {{{

### {{

### {{

### {

### (−488.9𝑥^4 H 2 +285.0𝑥^3 H 2

### −21.92𝑥^2 H 2 +1.351𝑥H 2

```
−0.040)m/s,𝑥H 2 ≤ 0.
(−160.2𝑥^4 H 2 +377.7𝑥^3 H 2
−348.7𝑥^2 H 2 +140.0𝑥H 2
−17.45)m/s,𝑥H 2 > 0.35.
```
### (5)

```
In inhomogeneous mixtures it is essential to compute a
correct flame speed in partially burned cells. Therefore, in
the computation of the laminar flame speed,𝑥H 2 is not
to be based on the actual hydrogen content, but on the
mixture fraction𝑓H, that is, the amount of hydrogen that
wouldbepresentifthecellwascompletelyunburned[ 54 ].
This is achieved by evaluating the hydrogen content𝑥H 2
(molar fraction of the hydrogen molecule) based on the
mixture fraction𝑓H(mass fraction of the hydrogen atom).
The spatial distribution of the mixture fraction is described
by a transport equation [ 54 ]:
```
```
𝜕
𝜕𝑡
```
### (𝜌𝑓̃H)+

### 𝜕

### 𝜕𝑥𝑗

### (𝜌𝑓̃H̃𝑢𝑗)=

### 𝜕

### 𝜕𝑥𝑗

```
(𝜌𝐷eff
```
### 𝜕𝑓̃H

### 𝜕𝑥𝑗

### ). (6)

```
The dependence of laminar flame speed on pressure and
temperature can be approximated as [ 55 ]:
```
### 𝑠𝐿=𝑠𝐿,0(

### 𝑇

### 𝑇 0

### )

```
𝛼
(
```
### 𝑝

### 𝑝 0

### )

```
𝛽
```
. (7)

```
Constant values of𝛼 = 1.75and𝛽=−0.2have been used in
this study.
The detonative source term𝜔𝑐,ignin ( 1 ) accounts for
autoignition effects. Autoignition occurs after the expiry of
the local autoignition delay time𝑡ign.Theautoignitiondelay
time of a gaseous mixture is a function of local temperature
𝑇, pressure𝑝, and mixture composition. In pure hydrogen-
air mixtures, the mixture composition can be described using
```

4 Journal of Combustion

```
0 0.
```
```
0 0.05 0 0.
```
```
0 0.
```
```
0
```
```
5
```
```
10
```
```
400
```
```
600
```
```
800
```
```
0
```
```
100
```
```
200
```
```
300
```
```
400
```
```
1
```
```
2
```
```
3
```
```
4
```
```
p
```
```
(bar)
```
```
x(m)
```
```
−0.
```
```
x(m)
```
```
−0.
x(m)
```
```
−0.
```
```
x(m)
```
```
−0.
```
```
T
```
```
(K)
```
```
𝜌
```
```
(kg/m
```
```
3 )
```
```
u
```
```
(m/s)
```
```
Figure 1: Results of shock-tube calculation with PISO scheme.
```
the mixture fraction𝑓H ( 6 ). In order to avoid frequent
recomputation of the local ignition delay time, a table of𝑡ign
as a function of𝑇,𝑝,and𝑓His generated usingCantera[ 56 ]

and theO Conaire mechanism [ ́ 57 ]. This mechanism is valid
for pressures up to 87 atm and temperatures up to 2700 K.
The flow solver can access the table and query the local
autoignition delay time𝑡ign(𝑇,𝑝,𝑓H)in each computational
cell.
An alternative means of modelling autoignition is the
concept of a virtual radical species𝑅preferred by some
authors [ 46 , 47 ].Whileinthisstudytheconceptofatabulated
ignition delay time is preferred, it can be shown that both
models equivalently lead to the definition of a dimensionless
variable describing the autoignition process [ 52 ]:

### 𝜏=

### 𝑡

```
𝑡ign
```
### =

### 𝑦𝑅

```
𝑦𝑅,critical
```
### . (8)

The ignition variable𝜏reaches unity when the ignition delay
time has passed (equivalently, it can be thought of the virtual
ignition radical reaching a critical concentration). As long as
the ignition delay time has not been reached yet (𝑡<𝑡ign),
there is no impact on the flow properties. Only if𝜏=1is
reached, the mixture is ignited.

```
Due to the fact that autoignition in a DDT context can
be triggered by shock-induced heating, a submodel is intro-
duced that increases the accuracy of autoignition modelling
on coarse grids. Tosatto and Vigevano [ 58 ] demonstrated
that, while the average temperature in a computational cell
canbehighenoughtotriggerautoignition,itisimportant
for detonation simulations to account for the fact that the
shock causing the temperature rise might not have traversed
the entire computational cell yet. Consequently a model that
predicts autoignition of a computational cell based on average
temperature and average pressure leads to incorrect results.
Duetothelargedisparityofscales,thatis,theshockbeing
far too thin to be resolved on the computational grid, each
computational cell is divided into two parts: in one part
(volume fraction𝛼) temperature and pressure are elevated
to𝑇highand𝑝high; in the other part (volume fraction1−𝛼)
the values remain at𝑇lowand𝑝low.𝑝highis defined by the
highest value and𝑝lowby the lowest value that can be found in
the surrounding computational cells. From consistency with
the average pressure𝑝in the computational cell, the volume
fraction𝛼can be determined:
```
### 𝛼=

```
𝑝−𝑝low
𝑝high−𝑝low
```
### . (9)


Journal of Combustion 5

```
0 0.
```
```
0
```
```
5
```
```
10
```
```
400
```
```
600
```
```
800
```
```
0
```
```
100
```
```
200
```
```
300
```
```
400
```
```
1
```
```
2
```
```
3
```
```
4
```
```
p
```
```
(bar)
```
```
x(m)
```
```
−0.
```
```
0 0.
x(m)
```
```
−0.05 0 0.
x(m)
```
```
−0.
```
```
0 0.
x(m)
```
```
−0.
```
```
T
```
```
(K)
```
```
𝜌
```
```
(kg/m
```
```
3 )
```
```
u
```
```
(m/s)
```
```
Figure 2: Results of shock-tube calculation with HLLC scheme.
```
```
Thigh Tlow
```
```
plow
```
```
fH fH
```
```
𝛼1−𝛼
```
```
phigh
```
Figure 3: Model illustration: a shock divides a computational cell
into a volume fraction𝛼of high temperature and pressure and a
volume fraction1−𝛼of low temperature and pressure.

𝑇highand𝑇loware computed subsequently from gas dynamic
shock relations for an ideal gas with heat capacity ratio𝛾[ 59 ]:

```
𝑝high
𝑝low
```
### =1+

```
2𝛾(Ma^2 −1)
𝛾+
```
### , (10)

```
𝑇high
𝑇low
```
### =(1+

```
2𝛾(Ma^2 −1)
𝛾+
```
### )(1−

```
2(1−Ma−2)
𝛾+
```
### ). (11)

When𝑝highand𝑝loware known, ( 10 )canbesolvedforthe
shock Mach number Ma and ( 11 ) yields the according temper-
ature ratio𝑇high/𝑇low. The temperatures can be determined by

```
requiring consistency of𝑇highand𝑇lowwith the cell-averaged
temperature𝑇̃:
```
```
𝑇=𝛼𝑇̃ high+(1−𝛼)𝑇low. (12)
```
```
The resulting representation of a computational cell is
given inFigure 3. While the presence of a shock alters
temperature and pressure, the mixture fraction𝑓His not
affected. The ignition delay time is evaluated separately on
each side of the shock:
```
```
𝑡ign,high=𝑡ign(𝑇high,𝑝high,𝑓H),
```
```
𝑡ign,low=𝑡ign(𝑇low,𝑝low,𝑓H).
```
### (13)

```
It is important to note that this model does not only work
in computational cells where a shock is present but can also
be applied to the entire computational domain. The reason is
that in the case of low pressure differences,𝑝high≳𝑝≳𝑝low,
the temperature rise computed from ( 10 )and( 11 )isquasi-
identical to the temperature rise gained from an isentropic
compression:
```
```
𝑇high
𝑇low
```
### =(

```
𝑝high
𝑝low
```
### )

```
(𝛾−1)/𝛾
```
. (14)

```
In each grid cell, the process of autoignition is evaluated
separately on both sides of the discontinuity. Transport
```

6 Journal of Combustion

and mixing effects are accounted for by solving transport
equations for𝜏highand𝜏low:

### 𝜕

### 𝜕𝑡

```
(𝜌̃𝜏high)+
```
### 𝜕

### 𝜕𝑥𝑗

```
(𝜌𝜏̃high̃𝑢𝑗)=
```
### 𝜕

### 𝜕𝑥𝑗

```
(𝜌𝐷eff
```
```
𝜕𝜏̃high
𝜕𝑥𝑗
```
### )+

### 𝜌

```
𝑡ign,high
```
### ,

### 𝜕

### 𝜕𝑡

```
(𝜌𝜏̃low)+
```
### 𝜕

### 𝜕𝑥𝑗

```
(𝜌𝜏̃low𝑢̃𝑗)=
```
### 𝜕

### 𝜕𝑥𝑗

```
(𝜌𝐷eff
```
```
𝜕̃𝜏low
𝜕𝑥𝑗
```
### )+

### 𝜌

```
𝑡ign,low
```
### .

### (15)

If the critical value of𝜏=1is reached on one side
of the discontinuity (i.e.,𝜏high =1or𝜏low =1), only the
corresponding volume fraction of a computational cell is
ignited. Consequently the autoignition source term in ( 1 )can
be formulated as

```
𝜔𝑐,ign=𝛼
```
### 1−̃𝑐

### Δ𝑡

```
H(̃𝜏high−1)+(1−𝛼)
```
### 1−̃𝑐

### Δ𝑡

```
H(̃𝜏low−1).
(16)
```
Here,Δ𝑡represents the current time step and H(𝑥)
represents the Heaviside function:

### H(𝑥) ={

### 0, 𝑥<

### 1, 𝑥≥0.

### (17)

The Heaviside function activates only the part of the
computational cell in which the local ignition delay time has
expired. This is achieved by weighting the volumetric source
termbythevolumefractionofeither𝛼or1−𝛼.

## 3. Experimental and Numerical Setup

The model has been tested against experimental results
gained in a closed rectangular channel of length𝐿=5.4m,
height𝐻=60mm, and width𝑊 = 300mm. The channel is
equipped with flat plate obstacles (thickness 12 mm) of height
ℎspaced at a distance of𝑆 = 300mm from each other. The
first obstacle is placed at𝑥 = 0.25mfromthefrontplate
whereasparkplugignitesthemixture.Thelastobstacleis
placed at𝑥 = 2.05m and the remaining part of the channel is
unobstructed (seeFigure 4). The obstacle blockage ratio BR
is determined by the obstacle heightℎ:

### BR=

### 2ℎ

### 𝐻

### . (18)

Thetopwallofthechannelisequippedwith42UV
sensitive photodiodes and 6 pressure transducers operated
at a sampling rate of 250 kSamples/s. Another pressure
transducer is mounted head-on in the center of the end wall
(𝑥 = 5.4m). A flame position versus time (𝑥versus𝑡)
correlation is obtained from the photodiode measurements.
The flame velocity between two subsequent photodiodes is
calculated by applying a first order derivative:

### V(𝑥=

### 𝑥𝑖+𝑥𝑖+

### 2

### )=

### 𝑥𝑖+1−𝑥𝑖

### 𝑡𝑖+1−𝑡𝑖

### . (19)

Here,𝑡𝑖and𝑡𝑖+1represent the time at which the flame passes
the photodiodes located at𝑥𝑖and𝑥𝑖+1, respectively. The same

```
Ignition
```
```
h
x
```
```
S H
```
```
Figure 4: Schematic sketch of the channel geometry (side view).
```
```
procedure is applied for evaluating the flame velocity in the
numerical simulations.
Within the channel defined vertical concentration gra-
dients can be generated. The overall amount of hydrogen is
controlled via the partial pressure method. First, the air-filled
channel is partially evacuated. Then, hydrogen is injected
through several nozzles located at the top wall. The injection
velocity is constant due to a choked nozzle upstream of the
point of injection. The injection time defines the amount
of hydrogen injected. Subsequently there is a defined time
interval (waiting time𝑡𝑤) during which diffusion takes place.
Due to the strong density difference between hydrogen and
air, a defined vertical concentration gradient is achieved
while horizontal concentration gradients remain negligible.
Finally the mixture is ignited by a spark plug. For a more
detailed description of the experimental setup, the procedure
of hydrogen injection, and mixture generation it is referred to
the publications of Vollmer et al. [ 29 , 60 ].
In order to determine the hydrogen distribution before
ignition for many different hydrogen/air ratios and different
waiting times, numerical simulations of the injection process
have been conducted. Exemplary results for local hydrogen
mole fraction over channel height at a waiting time𝑡𝑤 =
3 s (the strongest gradient under investigation) are shown
inFigure 5. For waiting times𝑡𝑤 >30sthemixturecan
be considered as homogeneous. The results of the injection
simulations are stored as polynomials (hydrogen content
versus channel height) which are used as initial conditions
for the combustion simulations.
In the two-dimensional combustion simulations pre-
sented in the following section the channel is discretized
with a uniform, rectangular grid of 2 mm grid spacing. Test
runs showed that this resolution is the minimum resolution
required to achieve grid independence with respect to the
location of DDT. On coarser grids, DDT occurred mostly
later or not at all. On finer grids, the location of DDT did not
vary any more. However, at higher grid resolution, pressure
peaks still got a little sharper. This should be kept in mind for
the interpretation of the pressure plots shown in this paper.
Initially the fluid is at rest at a temperature of 293 K and a
pressure of 1.01 bar. The boundary conditions are defined as
adiabatic no-slip walls. Turbulence is modelled using the𝑘-𝜔-
SST model which is known for its good performance for both
free-stream jets and wall-bounded flow [ 61 , 62 ]. The initial
hydrogen distribution either is homogeneous or corresponds
to a concentration gradient of waiting time𝑡𝑤 =3s(see
Figure 5).
Ignition is modelled by patching the site of ignition at
𝑥=0with a burned mixture (𝑐=1,seeFigure 4). The
initial turbulence is vanishingly small and consequently𝜉
```

Journal of Combustion 7

```
0 10 20 30 40 50 60
```
```
0
```
```
10
```
```
20
```
```
30
```
```
Height (mm)
−
```
```
−
```
```
−
```
```
H 2 mole fraction (%)
```
```
10 %H 2
15 %H 2
20 %H 2
```
```
25 %H 2
30 %H 2
```
Figure 5: Local hydrogen content versus channel height after a
waiting time of 3 s. The legend displays the overall hydrogen content
of each mixture.

equals unity so that𝑠𝑇=𝑠𝐿follows from ( 3 ). This means, the
flame starts to propagate at laminar flame speed. However,
turbulence is quickly generated by the flow itself so that the
flame starts to accelerate. Test runs showed that the actual
choice of initial turbulence variables is insignificant as long
as𝜉=1is ensured. As the HLLC scheme gets unstable in
the incompressible limit where no coupling between pressure
and density exists, the first few time steps are calculated with
a pressure-based solver [ 37 ]usingthePISOscheme[ 40 ].
Before the flame reaches the first obstacle, the combustion-
driven flow is usually strong enough to switch to the HLLC
scheme that enables better shock capturing. Test runs showed
that the transition between both schemes is smooth if it
occurs while the maximum Mach number in the flow is in
the range of0.05 <Ma< 0.10.

## 4. Results and Discussion

Experimental and numerical results for a homogeneous
case with 15% hydrogen (volumetric) and blockage ratio
BR =30%areshowninFigure 6. It can be seen that the
agreement between experiment and simulation is very good.
The flame velocity rises continually in the obstructed part
of the channel (𝑥 ≤ 2.05m). This can be attributed to
the mutual amplification of combustion-induced expansion
and turbulence generation due to interaction with obstacles.
Shortly after passing the final obstacle the flame speed reaches
a maximum and then decreases slowly. At𝑥≈4mthe
flame comes to a nearly complete rest before it accelerates
again. This can be explained as follows: after passing the
final obstacle, turbulence generation is diminished so that
decelerating effects like friction outweigh the accelerating
ones.Theflamecontinuouslygetsslower.Simultaneously,
while the flame has been consuming fresh gas, it generated

```
1 2 3 4 5
```
```
0
```
```
100
```
```
200
```
```
300
```
```
400
```
```
500
```
```
600
```
```
700
```
```
800
```
```
Exp.
Sim.
```
```
Velocity
```
```

```
```
(m/s)
```
```
Flame positionx(m)
```
```
Figure 6: Flame propagation in a mixture with 15% H 2 (homoge-
neous).
```
```
1 2 3 4 5
```
```
0
```
```
200
```
```
400
```
```
600
```
```
800
```
```
1000
```
```
1200
```
```
1400
```
```
Exp.
Sim.
```
```
Velocity
```
```
(m/s)
```
```
Flame positionx(m)
```
```
Figure 7: Flame propagation in a mixture with 15% H 2 (max.
concentration gradient).
```
```
pressure waves and displaced the unburned gas into the
positive𝑥direction. Shocks were generated that propagated
towards the end wall from where they are being reflected.
These reflected shocks now generate fluid flow in negative
𝑥direction. When the leading, backwards-running shock
reaches the flame (this happens at𝑥≈4m), negative
flow velocity and positive burning speed nearly cancel out
so that the resulting net propagation velocity approaches
zero.However,asthereisstillunburnedgasinfrontofthe
flame, it recovers and accelerates again. The maximum flame
propagation velocity of approximately 500 m/s indicates that
no DDT occurred and the combustion process remained
entirely deflagrative.
Figure 7shows the results for a mixture that contains
an average hydrogen content of 15% as well, but with a
```

8 Journal of Combustion

```
0
```
```
20
```
```
40
```
```
60
```
```
80
```
```
100
```
```
120
```
```
Sim.
```
```
20 22 24 26 28 30 32 34
```
```
20 22 24 26 28 30 32 34
```
```
0
```
```
20
```
```
40
```
```
60
```
```
80
```
```
100
```
```
120
```
```
Exp.
```
```
x=5.4m
```
```
Timet(ms)
```
```
Pressure
```
```
p
```
```
(bar)
```
```
Timet(ms)
```
```
Pressure
```
```
p
```
```
(bar)
```
Figure 8: Pressure records from the sensor mounted on the end
wall. Mixture with 15% H 2 (max. concentration gradient).

vertical concentration gradient as shown inFigure 5.All
other parameters are kept identical. In the early acceleration
phase the flame velocity increases continually. This is in
good agreement with the experiment. Then the flame is
decelerated for the first time, due to a first shock front
reflected from the end wall. The difference in the experiment
canbeattributedtothedifferentignitionprocess:thespark
generated by the spark plug in the experiment is considerably
smallerthantheignitionpatchusedinthesimulationwhich
islimitedbythegridresolution.Thustheinitialpressure
wave generation in the experiment might be a little different
from the initial pressure rise caused by the ignition in the
numerical simulation. At the end of the obstacle region
the flame speed peaks and then loses some driving force
but eventually recovers. Although there is a considerable
velocity difference between experiment and simulation in
the unobstructed part, the final velocity is nearly the same.
The pressures recorded by the sensor in the end wall reach
extremely high values close to 120 bar (seeFigure 8). In the
homogeneous case, for comparison, the maximum pressure
is in the range of 10 bar. The reason for the extreme pressure
rise in the inhomogeneous case is revealed inFigure 9where
the temperature and pressure distribution in the rear part of
the explosion channel (4.9m< 𝑥 < 5.4m) is displayed.
At𝑡 = 27.15mstheflameapproachestheendwall.Due
to the inhomogeneous fuel distribution the flame is highly
asymmetric and propagates mainly in the upper part of the
channel. A leading shock has already been reflected from
theendwallandmovestowardsthepropagatingflame.At
𝑡 = 27.25ms it reaches the flame. From this point onwards

```
theflameburnsintoaprecompressedmixturewherethe
heat release rate is increased due to the increased density
and increased laminar burning velocity (see ( 2 )and( 7 )). The
increased reaction rate leads to a strong pressure rise and
causes an explosion at𝑡 = 27.40ms. A radial detonation
wave emanates from the explosion center and ignites the gas
over the whole channel height. The newly formed detonation
frontrunstowardstheendwallwhereitcausesanenormous
pressure rise. This DDT mechanism has been suggested as
one possible explanation for the high pressure loads observed
in the experimental work of Eder [ 63 ]. In Eder’s work, high
pressure loads on the end wall of an explosion channel
have been observed, but the flame velocity measurements
indicated only a fast deflagration, not a detonation. As in the
present simulation, the DDT in Eder’s experiments obviously
occurred so late (behind the final photo diode) that the
DDT was not identified as one; only the high pressures on
the end wall gave rise to speculation. Recent experimental
investigations of Boeck et al. [ 64 ]supporttheconclusionthat
a DDT mechanism as identified inFigure 9is responsible for
the high pressure peak.
Due to the limited spatial resolution the present simula-
tion does not resolve the interaction with the boundary layer.
Moreover, it does not capture the shock-flame interaction
in such a detailed manner as previous numerical studies
on highly resolved grids (e.g., [ 12 , 13 ]). Nevertheless the
model is able to correctly predict the consequence of the
backwards-running shock hitting the flame: an increased
reaction rate due to precompression and intensified mixing
which consequently triggers DDT.
From the pressure records inFigure 8it can be con-
cluded that there is a slight difference between experiment
and simulation: the initial pressure rise in the simulation
at𝑡≈26ms (caused by the reflection of the leading
shock) does not appear in the experimental record. Due to
the highly nonlinear dependence of ignition delay time on
temperature and pressure, the higher propagation velocity in
the experiment (Figure 7) is obviously sufficient to cause a
strong autoignition quasi-instantaneously when the leading
shock reaches the end wall. The resulting pressure load on
the end wall, however, is nearly the same in experiment and
simulation.
Increasingthehydrogencontentleadstoanearlier
occurrence of DDT. At a hydrogen content of 25% (again with
a concentration gradient as described inFigure 5)itcanbe
seen fromFigure 10that the flame velocity rises continually to
approximately 1000 m/s in the obstructed part of the channel
and then suddenly jumps to 2500 m/s and finally relaxes to
approximately 2000 m/s.
ThisisaclearindicationfortheoccurrenceofaDDTwith
an initially overdriven detonation decaying to a Chapman-
Jouguet detonation. The large fluctuations in the experimen-
talvelocityaftertheonsetofDDTcanbeexplainedbysmall
measurement errors in flame arrival time having a relatively
large effect when the derivative ( 19 ) is applied to the data.
Using only the𝑥-𝑡diagram (Figure 11)asitiscommonin
most publications does not reveal this difference.
The DDT process occurring in this case is visualized in
Figure 12.At𝑡 = 12.44ms, the flame approaches the final
```

Journal of Combustion 9

```
293 1000 2000 3000
TemperatureT(K)
```
```
t = 27.15ms
```
```
t = 27.20ms
```
```
t = 27.25ms
```
```
t = 27.30ms
```
```
t = 27.35ms
```
```
t = 27.40ms
```
```
t = 27.45ms
```
```
4.9 5.0 5.1 5.2 5.3 5.
x(m)
```
```
t = 27.15ms
```
```
t = 27.20ms
```
```
t = 27.25ms
```
```
t = 27.30ms
```
```
t = 27.35ms
```
```
t = 27.40ms
```
```
t = 27.45ms
```
```
4.9 5.0 5.1 5.2 5.3 5.
x(m)
```
```
0 10 20 30 40
Pressurep(bar)
```
```
Figure 9: Visualization of a DDT caused by interaction of the flame with a reflected shock.
```
```
1 2 3 4 5
```
```
0
```
```
500
```
```
1000
```
```
1500
```
```
2000
```
```
2500
```
```
Exp.
Sim.
```
```
Velocity
```
```
(m/s)
```
```
Flame positionx(m)
```
Figure 10: Flame velocity versus channel length for a mixture with
25% H 2 (max. concentration gradient).

obstacle. The curved shock in front of the flame is reflected
from the bottom wall by forming a Mach stem. At𝑡=
12.45ms, autoignition occurs behind the Mach stem. At𝑡=
12.47ms, the oblique shock hits the upper obstacle which
initiates a second autoignition event. From there a circular
detonation emanates and unites with the autoignition front
from the lower part of the channel. While the detonation
front moves through the gap between the obstacles into the
unburned gas (𝑡 > 12.48ms), the opposite front of the
reaction wave (“retonation wave” [ 65 ]) runs backwards and
consumes the remaining fresh gas in the lower part of the
channel. It is important to note that the two autoignition
kernels inFigure 12arebothwellaheadoftheflamebutoccur

```
0 5 10 15 20
```
```
1
```
```
2
```
```
3
```
```
4
```
```
5
```
```
Exp.
Sim.
```
```
Timet(ms)
```
```
Flame position
```
```
x
```
```
(m)
```
```
Figure 11: Flame position versus time for a mixture with 25% H 2
(max. concentration gradient).
```
```
due to different reasons: the one on the bottom wall is due to
shock compression ahead of the flame while the one on the
upper wall occurs only due to reflection of the shock from
the upper obstacle.
Another simulation with only six obstacles showed that
the final obstacle was not necessary to achieve DDT. Instead,
the autoignition occurring behind the Mach stem at𝑡=
12.45ms is sufficient to trigger DDT and is only amplified
by the second autoignition event occurring on the upper
obstacle. At lower fuel content (20% H 2 )however,theseventh
obstacle is required to obtain a DDT.
It is interesting to note that the first autoignition in
Figure 12occurs at the bottom wall where the mixture is
```

10 Journal of Combustion

```
293 1000 2000 3000
TemperatureT(K)
```
```
010203040
Pressurep(bar)
```
```
t = 12.44ms
```
```
t = 12.45ms
```
```
t = 12.46ms
```
```
t = 12.47ms
```
```
t = 12.48ms
```
```
t = 12.49ms
```
```
t = 12.50ms
```
```
t = 12.51ms
```
```
t = 12.44ms
```
```
t = 12.45ms
```
```
t = 12.46ms
```
```
t = 12.47ms
```
```
t = 12.48ms
```
```
t = 12.49ms
```
```
t = 12.50ms
```
```
t = 12.51ms
```
```
1.8 1.9 2.0 2.1 2.2 2.
x(m)
```
```
1.8 1.9 2.0 2.1 2.2 2.
x(m)
```
```
Figure 12: Visualization of a DDT in the vicinity of the final obstacle.
```
```
293 1000 2000 3000
TemperatureT(K)
```
```
024681012
Pressurep(bar)
```
```
t = 11.16ms
```
```
t = 11.20ms
```
```
t = 11.24ms
```
```
t = 11.28ms
```
```
t = 11.32ms
```
```
t = 11.36ms
```
```
t = 11.40ms
```
```
t = 11.44ms
```
```
t = 11.48ms
```
```
t = 11.16ms
```
```
t = 11.20ms
```
```
t = 11.24ms
```
```
t = 11.28ms
```
```
t = 11.32ms
```
```
t = 11.36ms
```
```
t = 11.40ms
```
```
t = 11.44ms
```
```
t = 11.48ms
```
```
1.2 1.3 1.4 1.5 1.6 1.
x(m)
```
```
1.2 1.3 1.4 1.5 1.6 1.
x(m)
```
```
Figure 13: Shock-flame interaction at an obstacle of blockage ratio 60%. The pink contour shows the Ma = 1 line.
```
leanest. This phenomenon can be explained by taking a closer
look at the shock propagation: the leading shock approaches
the final obstacle at a constant speed ofV≈ 1450m/s. Near
the bottom wall the hydrogen content is 7% (seeFigure 5)
which results in a local speed of sound of𝑎 = 356m/s.

```
Thus, in the near vicinity of the bottom wall, the Mach stem
canbeseenasanormalshockpropagatingatMachnumber
Ma=V/𝑎 = 4.07. For fresh gas properties𝑝 0 =1.01bar and
𝑇 0 = 293Kthenormalshockrelations( 10 )and( 11 ) yield the
postshock state𝑝 1 = 19.4bar and𝑇 1 = 1220K. Near the top
```

Journal of Combustion 11

```
0 0.05 0.10 0.15 0.20 0.25 0.
```
```
0
```
```
5
```
```
10
```
```
15
```
```
20
```
```
25
```
```
30
```
```
35
```
```
40
```
```
To p w a l l
Bottom wall
```
```
Pressure
```
```
p
```
```
(bar)
```
```
Timet(ms)
```
Figure 14: Pressure records from a steadily propagating detonation
in a mixture with 25% H 2 (homogeneous).

wall where the mixture is rich (45%, seeFigure 5)thelocal
soundspeedhasavalueof𝑎 = 452m/s. This corresponds
to a Mach number of Ma = 3.21and yields a postshock
state of𝑝 1 = 12.0bar and𝑇 = 860K. The corresponding
ignition delay time is by orders of magnitude higher than on
the bottom wall. Thus, autoignition near the top wall can only
be achieved via shock reflection from the upper obstacle.
Another important finding is that although DDT occurs
much earlier in the case of 25% hydrogen, the pressure loads
on the wall are higher in the case of 15% hydrogen. This
is due to the different mode of DDT. At 25% hydrogen
(Figure 12), the detonation has sufficient space to expand. At
15% hydrogen (Figure 9), shock and flame interact very close
to the end wall and the overdriven detonation emerges from
a preshocked mixture. As there is no space to expand, the
overdriven detonation hits the end wall without losing much
of its strength.
While both simulations and experiments in this configu-
ration confirm the trend that (at equal average hydrogen con-
tent) a concentration gradient increases the DDT tendency,
this must not be understood as a general conclusion. In other
configurations the opposite effect can occur. For example,
if the blockage ratio is increased from 30% to 60% it has
been observed that the probability of DDT decreases. The
reason for this phenomenon can be seen inFigure 13.At𝑡=
11.16ms, the flame approaches the obstacle. Some pressure
waves have already been generated and passed the obstacle.
The constriction formed by the obstacle acts like a Laval
nozzle behind which an area of supersonic flow (visualized by
the pink line representing the Ma=1contour) is generated.
The obstacles cause the pressure waves to be reflected on 60%
andtopassonlyon40%ofthecross-sectionalarea.Dueto
the gas dynamic constraint formed by the Ma=1line, the
total mass flow through the orifice between the obstacles is
limited. At𝑡 = 11.16ms, a shock front is reflected from the
obstacle which leads to a shock propagation into negative

```
𝑥direction. This process is repeated with an even stronger
shock between𝑡 = 11.24ms and11.32ms. As the parts
of the shock that are reflected from the upper and lower
obstacle unite, a backwards-running shock over the whole
channel height is formed. In the trailing flow behind this
shockanareaofnegativeflowvelocitycausestheapproaching
flame to decelerate, while the part of the shock that passed in
between the obstacles to the right continues to propagate at
nearly unaffected speed. Thus a high blockage ratio destroys
the coupling between shock and flame which existed before
approaching the obstacle. At𝑡 = 11.48ms, the flame finally
manages to enter the region of high flow speed that prevails
between the obstacles. It is convected into the next cavity
wherestrongshocksaregeneratedandtheprocessdescribed
repeats.
These numerical results explain the experimental obser-
vation by Vollmer et al. [ 29 ] that a concentration gradient
can either increase or decrease the tendency towards DDT
with the decisive factor being the obstacle geometry. If the
obstacles are too large, they can lessen the DDT tendency
as the majority of the strong pressure waves causing DDT
are blocked. This is especially valid for an inhomogeneous
mixture as shown inFigure 13,wheretheflamemainlyburns
in the upper part of the channel. In this case the obstacles are
more obstructive than in a case with homogeneous mixture
where the flame can be expected to propagate through the
centerofthechannelwherenoobstaclesarepresent.
Another question that has been addressed with the newly
developed solver concerns the pressure loads that are caused
by a steadily propagating detonation front, that is, after
the occurrence of DDT. Therefore a look is taken at a
detonation propagating in an unobstructed channel. First,
this is demonstrated for a homogeneous mixture with 25%
hydrogen. Pressure records are taken from the top and the
bottom wall of the channel while a detonation passes. Test
runs showed that the axial location of the pressure sensors
did not influence the result any more as soon as a steadily
propagating detonation was achieved. The result is shown
inFigure 14. As the detonation front is nearly planar, the
pressure records from the bottom and the top wall are
virtually simultaneous. Upon arrival of the detonation front
the pressure jumps to approximately 18 bar. The following
expansion lets the pressure decrease slowly.
A completely different picture is found for a case with the
same average hydrogen content, but a strong concentration
gradient (Figure 15). As the leading shock is curved, it reaches
the pressure sensors on the top wall earlier. They show
maximum values of approximately 15 bar. On the bottom
wall,however,apressureofnearly38barisreached.Thisis
especially striking as the hydrogen content on the lower wall
is only 7% and a homogeneous mixture with 7% hydrogen
is basically nondetonable. Here, however, the lack of fuel
does not lead to lower, but to higher, pressure loads. Again,
the reason for this seeming paradox can be found in the
particular structure of the leading shock front: on the bottom
wall it is reflected via a Mach stem. Due to the lower speed
of sound this causes a higher pressure rise on the bottom
wall than on the top wall. After a short decline of the
```

12 Journal of Combustion

pressure, a second pressure rise is observed on both walls.
Thisisduetosecondaryreflectionsoftheleadingshock
thatcanbeseeninthepressurefieldinFigure 16.Behind
the secondary reflections the pressure equalizes so far that it
drops simultaneously on the bottom and the top wall.
The results demonstrate that the pressure loads caused
by a detonation in an inhomogeneous mixture can be
considerably higher than in a homogeneous mixture of the
same hydrogen content. Moreover, the location of the highest
impact can be in fuel-lean regions. Further calculations
showed that even if the hydrogen content on the bottom
wall is reduced to zero, the maximum pressures observed
there can still exceed those of the homogeneous mixture: the
concentration gradient only needs to be strong enough to
form a Mach stem. A simple method for predicting whether
a detonation front in an inhomogeneous mixture develops a
Machstemcanbefoundin[ 66 ].

## 5. Summary, Critical Analysis, and Outlook

Motivated by the current lack of suitable tools for DDT-
related safety studies [ 32 ], this paper presented a newly devel-
oped solver able to simulate flame acceleration, deflagration-
to-detonation transition, and detonation propagation within
a single run. The target was not to obtain detailed insight
and maximum accuracy of the complex interaction between
flow and reaction on microscopic scale, but to obtain a tool
for engineering purposes that works on comparatively coarse
grids and enables numerical safety studies at acceptable
computational costs. The applicability to coarse grids is
achieved by the inclusion of subgrid models. The agreement
with experimental results is very good and the simulation
gives additional insight into phenomena which cannot be
easily observed in experiments. Although the simulations
presented do not resolve all details of the flow, they are
able to capture fundamental phenomena known from highly
resolved simulations and experiments (e.g., [ 12 , 13 , 36 ]): DDT
due to shock compression/Mach stem formation ahead of the
flame,DDTduetoshockreflectionfromobstacles,andDDT
duetoshock-flameinteraction.
It has been found that concentration gradients, which are
likely to occur in accident scenarios, can have a considerable
effect on the nature of flame propagation. Depending on the
enclosing geometry, the presence of a concentration gradient
can decrease or increase flame propagation velocities, the
probability of DDT, and the pressure loads associated with
it. Thus, existing safety criteria developed for homogeneous
mixtures can be inaccurate and nonconservative. Neither
does a homogeneous mixture pose the highest threat regard-
ingtheprobabilityofDDTnordoesitcausethehighest
pressure loads. Due to gas dynamic phenomena within
inhomogeneous mixtures, fuel-lean regions can be more
DDT-prone than stoichiometric or rich regions. This should
be taken into account in future safety studies.
However, although the general agreement with experi-
ments is good, it has to be kept in mind that all results
have been gained on relatively coarse grids, without resolving
the induction distance between shock and reaction in a

```
0 0.05 0.10 0.15 0.20 0.25 0.
```
```
0
```
```
5
```
```
10
```
```
15
```
```
20
```
```
25
```
```
30
```
```
35
```
```
40
```
```
To p w a l l
Bottom wall
```
```
Pressure
```
```
p
```
```
(bar)
```
```
Timet(ms)
```
```
Figure 15: Pressure records from a steadily propagating detonation
in a mixture with 25% H 2 (max. concentration gradient).
```
```
0 5 10 15 20 25 30
Pressurep(bar)
```
```
Figure 16: Pressure distribution in a steadily propagating detona-
tion in a mixture with 25% H 2 (max. concentration gradient).
```
```
detonation front. Boundary layers are not resolved either and
they are known to have an effect on the onset of detonations.
Moreover, all the results presented in this study have been
obtained on 2D grids. Therefore, the authors have deliberately
chosen a geometry which is relatively wide (300 mm) com-
pared to its height (60 mm). Nevertheless transversal waves
are expected to play a role in flame acceleration and the onset
of DDT. While this project has already finished, a follow-up
project has started where 3D simulations are conducted [ 67 ]
and also simulations in large, complex geometries with the
aim of reproducing realistic accident scenarios. Approaches
are being developed to use even coarser grids by applying
subgrid models not only to shock propagation as shown in
this paper, but also to deflagrative flame propagation.
The advantage of the solver developed and its implemen-
tation inOpenFOAMis that it is not limited to structured
grids and thus can be applied to intricate geometries using
unstructured grids as well. The solver and its source code are
madefreelyavailabletothepublic[ 68 ].
```

```
Journal of Combustion 13
```
## Conflict of Interests

```
The authors declare that there is no conflict of interests
regarding the publication of this paper.
```
## Acknowledgments

```
This project is funded by the German Federal Ministry of
Economics and Technology on the basis of a decision of the
German Bundestag (Project no. 1501338) which is gratefully
acknowledged.TheauthorswouldliketothankOliverBorm
for sharing a Riemann solver code within the framework of
OpenFOAMwhich provided a valuable basis for this study.
```
## References

```
[1] Y.-L. Liu, J.-Y. Zheng, P. Xu et al., “Numerical simulation on
the diffusion of hydrogen due to high pressured storage tanks
failure,”JournalofLossPreventionintheProcessIndustries,vol.
22,no.3,pp.265–270,2009.
[2] B. P. Xu, J. X. Wen, S. Dembele, V. H. Y. Tam, and S. J.
Hawksworth, “The effect of pressure boundary rupture rate on
spontaneous ignition of pressurized hydrogen release,”Journal
of Loss Prevention in the Process Industries,vol.22,no.3,pp.
279–287, 2009.
[3] W. Breitung and P. Royl, “Procedure and tools for deterministic
analysis and control of hydrogen behavior in severe accidents,”
Nuclear Engineering and Design,vol.202,no.2-3,pp.249–268,
2000.
[4] M. Manninen, A. Silde, I. Lindholm, R. Huhtanen, and H.
Sj ̈ovall, “Simulation of hydrogen deflagration and detonation in
a BWR reactor building,”Nuclear Engineering and Design,vol.
211, no. 1, pp. 27–50, 2002.
[5] H. Dimmelmeier, J. Eyink, and M.-A. Movahed, “Computa-
tional validation of the EPR combustible gas control system,”
Nuclear Engineering and Design,vol.249,pp.118–124,2012.
[6] A. G. Venetsanos, D. Baraldi, P. Adams, P. S. Heggem, and H.
Wilkening, “CFD modelling of hydrogen release, dispersion
and combustion for automotive scenarios,”Journal of Loss
Prevention in the Process Industries,vol.21,no.2,pp.162–184,
2008.
[7]W.G.Houf,G.H.Evans,E.Merilo,M.Groethe,andS.C.
James, “Releases from hydrogen fuel-cell vehicles in tunnels,”
International Journal of Hydrogen Energy,vol.37,no.1,pp.715–
719, 2012.
[8] S. B. Dorofeev, “Flame acceleration and explosion safety appli-
cations,”Proceedings of the Combustion Institute,vol.33,no.2,
pp.2161–2175,2011.
[9] S. B. Margolis and B. J. Matkowsky, “Nonlinear stability and
bifurcation in the transition from laminar to turbulent flame
propagation,”Combustion Science and Technology,vol.34,no.
1–6, pp. 45–77, 1983.
```
[10] G. I. Sivashinsky, “Instabilities, pattern formation and turbu-
lence in flames,”Annual Review of Fluid Mechanics,vol.15,pp.
179–199, 1983.
[11] E. S. Oran and A. M. Khokhlov, “Deflagrations, hot spots,
and the transition to detonation,”Philosophical Transactions of
the Royal Society A: Mathematical, Physical and Engineering
Sciences, vol. 358, no. 1764, pp. 3539–3551, 2000.

```
[12] E. S. Oran and V. N. Gamezo, “Origins of the deflagration-
to-detonation transition in gas-phase combustion,”Combustion
and Flame,vol.148,no.1-2,pp.4–47,2007.
[13] V. N. Gamezo, T. Ogawa, and E. S. Oran, “Flame acceleration
and DDT in channels with obstacles: effect of obstacle spacing,”
Combustion and Flame,vol.155,no.1-2,pp.302–315,2008.
[14] M.A.Liberman,A.D.Kiverin,andM.F.Ivanov,“Ondetona-
tion initiation by a temperature gradient for a detailed chemical
reaction models,”Physics Letters A: General, Atomic and Solid
State Physics,vol.375,no.17,pp.1803–1808,2011.
[15] M. C. Gwak and J. J. Yoh, “Effect of multi-bend geometry
on deflagration to detonation transition of a hydrocarbon-air
mixture in tubes,”International Journal of Hydrogen Energy,vol.
38, no. 26, pp. 11446–11457, 2013.
[16] P. Hwang , R. P. Fedkiw, B. Merriman, T. D. Aslam, A. R.
Karagozian, and S. J. Osher, “Numerical resolution of pulsating
detonation waves,”Combustion Theory and Modelling,vol.4,no.
3,pp.217–240,2000.
[17] G. J. Sharpe, “Transverse waves in numerical simulations of
cellular detonations,”Journal of Fluid Mechanics,vol.447,pp.
31–51, 2001.
[18]G.Cael,H.D.Ng,K.R.Bates,N.Nikiforakis,andM.
Short, “Numerical simulation of detonation structures using a
thermodynamically consistent and fully conservative reactive
flow model for multi-component computations,”Proceedings
of the Royal Society A: Mathematical, Physical and Engineering
Sciences,vol.465,no.2107,pp.2135–2153,2009.
[19] K. Mazaheri, Y. Mahmoudi, and M. I. Radulescu, “Diffusion
and hydrodynamic instabilities in gaseous detonations,”Com-
bustion and Flame,vol.159,no.6,pp.2138–2154,2012.
[20] J. M. Powers and S. Paolucci, “Accurate spatial resolution
estimates for reactive supersonic flow with detailed chemistry,”
AIAA Journal,vol.43,no.5,pp.1088–1099,2005.
[21] M. Manninen, R. Huhtanen, I. Lindholm, and H. Sjovall, ̈
“Hydrogen in BWR reactor building,” inProceedings of the 8th
InternationalConferenceonNuclearEngineering(ICONE’00),
Baltimore, Md, USA, 2000.
[22] D. M. Prabhudharwadkar, K. N. Iyer, N. Mohan, S. S. Bajaj, and
S. G. Markandeya, “Simulation of hydrogen distribution in an
Indian Nuclear Reactor Containment,”Nuclear Engineering and
Design,vol.241,no.3,pp.832–842,2011.
[23] S. B. Dorofeev, A. S. Kochurko, A. A. Efimenko, and B. B.
Chaivanov, “Evaluation of the hydrogen explosion hazard,”
Nuclear Engineering and Design,vol.148,no.2-3,pp.305–316,
1994.
[24] S.B.Dorofeev,M.S.Kuznetsov,V.I.Alekseev,A.A.Efimenko,
and W. Breitung, “Evaluation of limits for effective flame
accelaration in hydrogen mixtures,”Journal of Loss Prevention
in the Process Industries, vol. 14, no. 6, pp. 583–589, 2001.
[25] A. Eder and N. Brehm, “Analytical and experimental insights
into fast deflagrations, detonations, and the deflagration-to-
detonation transition process,”Heat and Mass Transfer,vol.37,
no. 6, pp. 543–548, 2001.
[26] J. Chao and J. H. S. Lee, “The propagation mechanism of high
speed turbulent deflagrations,”Shock Waves,vol.12,no.4,pp.
277–289, 2003.
[27] M. Kuznetsov, V. Alekseev, I. Matsukov, and S. Dorofeev, “DDT
in a smooth tube filled with a hydrogen-oxygen mixture,”Shock
Waves,vol.14,no.3,pp.205–215,2005.
[28] C. R. L. Bauwens, L. Bauwens, and I. Wierzba, “Accelerating
flames in tubes—an analysis,”Proceedings of the Combustion
Institute,vol.31,pp.2381–2388,2007.
```

```
14 Journal of Combustion
```
```
[29] K. G. Vollmer, F. Ettner, and T. Sattelmayer, “Deflagration-to-
detonation transition in hydrogen/air mixtures with a concen-
tration gradient,”Combustion Science and Technology,vol.184,
pp. 1903–1915, 2012.
[30] O. Auban, R. Zboray, and D. Paladino, “Investigation of large-
scale gas mixing and stratification phenomena related to LWR
containment studies in the PANDA facility,”Nuclear Engineer-
ing and Design,vol.237,no.4,pp.409–419,2007.
[31] D.C.Visser,M.Houkema,N.B.Siccama,andE.M.J.Komen,
“Validation of a FLUENT CFD model for hydrogen distribution
in a containment,”Nuclear Engineering and Design,vol.245,pp.
161–171, 2012.
[32] W. Breitung, C. K. Chan, S. Dorofeev et al., “Flame accel-
eration and deflagration-to-detonation transition in nuclear
safety,” Tech. Rep. NEA/CSNI/R(2000)7, OECD State-of-the-
ArtReportbyaGroupofExperts,2000.
[33] F. Ettner, K. G. Vollmer, and T. Sattelmayer, “Numerical inves-
tigation of DDT in inhomogeneous hydrogen-air mixtures,”
inProceedings of the 8th International Symposium on Hazards,
Prevention and Mitigation of Industrial Explosions, Yokohama,
Japan, 2010.
[34] D. A. Kessler, V. N. Gamezo, and E. S. Oran, “Gas-phase
detonation propagation in mixture omposition gradients,”
Philosophical Transactions of the Royal Society A: Mathematical,
Physical and Engineering Sciences,vol.370,no.1960,pp.567–
596, 2012.
[35] H. Soury and K. Mazaheri, “Utilizing unsteady curved detona-
tion analysis and detailed kinetics to study the direct initiation
of detonation in H 2 -O 2 and H 2 -Air mixtures,”International
JournalofHydrogenEnergy, vol. 34, no. 24, pp. 9847–9856, 2009.
[36] G. Thomas, “Some observations on the initiation and onset of
detonation,”Philosophical Transactions of the Royal Society A:
Mathematical, Physical and Engineering Sciences,vol.370,no.
1960, pp. 715–739, 2012.
[37] OpenFOAM, “User guide, version 2.1.1,” 2012,http://www.
openfoam.org.
[38]E.F.Toro,M.Spruce,andW.Speares,“Restorationofthe
contact surface in the HLL-Riemann solver,”Shock Waves,vol.
4,no.1,pp.25–34,1994.
[39] OpenFOAM Wiki, “Limiters,” 2010,http://openfoamwiki.net/
index.php/OpenFOAMguide/Limiters.
```
[40] R. I. Issa, “Solution of the implicitly discretised fluid flow equa-
tions by operator-splitting,”Journal of Computational Physics,
vol.62,no.1,pp.40–65,1986.
[41] R. J. Kee, F. M. Rupley, J. A. Miller et al., “The chemkin
thermodynamic database, chemkin Collection, release 3.6,”
2000,http://www.sandia.gov/chemkin.
[42]R.B.Bird,W.E.Stewart,andE.N.Lightfoot,Transport
Phenomena, Wiley, New York, NY, USA, 2001.
[43] K. N. C. Bray and J. B. Moss, “A unified statistical model of the
premixed turbulent flame,”Acta Astronautica,vol.4,no.3-4,pp.
291–319, 1977.
[44] A. Favre, “Equations des gaz turbulents compressibles,”Journal
de M ́ecanique,vol.4,pp.361–390.
[45] C.Chen,J.J.Riley,andP.A.McMurtry,“AstudyofFavreaver-
aging in turbulent flows with chemical reaction,”Combustion
and Flame,vol.87,no.3-4,pp.257–277,1991.
[46] M. Brandt, W. Polifke, B. Ivancic, P. Flohr, and B. Paikert, “Auto-
ignition in a gas turbine burner at elevated temperature,” in
Proceedings of the ASME Turbo Expo, pp. 195–205, Atlanta, Ga,
USA,, June 2003.

```
[47] O. Colin, A. Pires da Cruz, and S. Jay, “Detailed chemistry-based
auto-ignition model including low temperature phenomena
applied to 3-D engine calculations,”Proceedings of the Combus-
tion Institute,vol.30,no.2,pp.2649–2656,2005.
[48] J.-B. Michel, O. Colin, and C. Angelberger, “On the formulation
of species reaction rates in the context of multi-species CFD
codes using complex chemistry tabulation techniques,”Com-
bustion and Flame,vol.157,no.4,pp.701–714,2010.
[49] H.G.Weller,G.Tabor,A.D.Gosman,andC.Fureby,“Applica-
tion of a flame-wrinkling LES combustion model to a turbulent
mixing layer,”Symposium (International) on Combustion,vol.
27, pp. 899–907, 1998.
[50] K. N. C. Bray, “Complex chemical reaction systems,” inChapter
Methods of Including Realistic Chemical Reaction Mechanisms
in Turbulent Combustion Models,vol.47ofSpringer Series in
Chemical Physics, pp. 356–375, Springer, 1986.
[51] V. L. Zimont and A. N. Lipatnikov, “A numerical model of
premixed turbulent combustion of premixed gases,”Chemical
Physics Reports,vol.14,pp.993–1025,1995.
[52] F. Ettner,Effiziente numerische simulation des deflagrations-
detonations-Ubergangs [Ph.D. thesis] ̈ ,TUM ̈unchen, 2013.
[53] A. A. Konnov, “Remaining uncertainties in the kinetic mecha-
nism of hydrogen combustion,”Combustion and Flame,vol.152,
no. 4, pp. 507–528, 2008.
[54] W. Polifke, P. Flohr, and M. Brandt, “Modeling of inhomoge-
neously premixed combustion with an extended TFC model,”
Journal of Engineering for Gas Turbines and Power,vol.124,no.
1,pp.58–65,2002.
[55] S. R. Turns,An Introduction to Combustion,McGraw-Hill,2000.
[56] D. Goodwin, “Cantera: an object-oriented software toolkit for
chemical kinetics, thermodynamics and transport processes,”
2009,http://code.google.com/p/cantera.
[57] M.O Conaire, H. J. Curran, J. M. Simmie, W. J. Pitz, and C. ́
K. Westbrook, “A comprehensive modeling study of hydrogen
oxidation,”International Journal of Chemical Kinetics,vol.36,
no. 11, pp. 603–622, 2004.
[58] L. Tosatto and L. Vigevano, “Numerical solution of under-
resolved detonations,”Journal of Computational Physics,vol.
227, no. 4, pp. 2317–2343, 2008.
[59] J. D. Anderson,Modern Compressible Flow, McGraw-Hill, 2004.
[60] K. G. Vollmer, F. Ettner, and T. Sattelmayer, “Influence of
concentration gradients on flame acceleration in tubes,” in
Proceedings of the 8th International Symposium on Hazards,
PreventionandMitigationofIndustrialExplosions, Yokohama,
Japan, 2010.
[61] F. R. Menter, “Two-equation eddy-viscosity turbulence models
for engineering applications,”AIAA Journal,vol.32,no.8,pp.
1598–1605, 1994.
[62] F. R. Menter, “Review of the shear-stress transport turbulence
model experience from an industrial perspective,”International
Journal of Computational Fluid Dynamics,vol.23,no.4,pp.
305–316, 2009.
[63] A. Eder,Brennverhalten schallnaher unduberschall-schneller ̈
Wasserstoff-Luft Flammen [Ph.D. thesis],TUMunchen, 2001. ̈
[64] L. R. Boeck, J. Hasslberger, F. Ettner, and T. Sattelmayer,
“Investigation of peak pressures during explosive combustion
of inhomogeneous hydrogen-air mixtures,” inProceedings of
the 7th International Fire and Explosion Hazards Seminar,
Providence, RI, USA, 2013.
[65] A. K. Oppenheim, A. J. Laderman, and P. A. Urtiew, “The onset
of retonation,”Combustion and Flame, vol. 6, pp. 193–197, 1962.
```

```
Journal of Combustion 15
```
[66] F. Ettner, K. G. Vollmer, and T. Sattelmayer, “Mach reflection
in detonations propagating through a gas with a concentration
gradient,”Shock Waves,vol.23,pp.201–206,2013.
[67] J. Hasslberger, F. Ettner, L. R. Boeck, and T. Sattelmayer,
“2D and 3D flame surface analysis of flame acceleration and
deflagration-to-detonation transition in hydrogenair mixtures
with concentration gradients,” inProceedings of the 24th Inter-
national Conference on the Dynamics of Explosions and Reactive
Systems (ICDERS ’13), Taipei, Taiwan, 2013.
[68] F. Ettner and T. Sattelmayer, ddtFoam, 2013,http://sourceforge.
net/projects/ddtfoam.


