## Combustion Science and Technology

```
ISSN: (Print) (Online) Journal homepage: http://www.tandfonline.com/journals/gcst
```
# Numerical Modeling of Hydrogen Flame

# Acceleration and DDT Using Generalized Turbulent

# Flame Closure Approach

### Aditya Karanam & Vishnu Verma

**To cite this article:** Aditya Karanam & Vishnu Verma (28 Sep 2024): Numerical Modeling of
Hydrogen Flame Acceleration and DDT Using Generalized Turbulent Flame Closure Approach,
Combustion Science and Technology, DOI: 10.1080/00102202.2024.

**To link to this article:** https://doi.org/10.1080/00102202.2024.

```
Published online: 28 Sep 2024.
```
```
Submit your article to this journal
```
```
Article views: 46
```
```
View related articles
```
```
View Crossmark data
```
```
Full Terms & Conditions of access and use can be found at
https://www.tandfonline.com/action/journalInformation?journalCode=gcst
```

## Numerical Modeling of Hydrogen Flame Acceleration and DDT

## Using Generalized Turbulent Flame Closure Approach

Aditya Karanama,b and Vishnu Vermab

aHomi Bhabha National Institute, Mumbai, India; bReactor Safety Division, Bhabha Atomic Research Centre,
Mumbai, India

```
ABSTRACT
In this work, a numerical methodology based on the paradigm of
Turbulent Flame Closure (TFC) has been tested to simulate flame
acceleration and Deflagration-to-Detonation Transition (DDT) in
hydrogen air mixtures. Flame tracking is based on the transport equa-
tion for the progress variable. To minimize the need for tuning/cali-
bration of model parameters, a generalized transport equation for the
flame-wrinkling factor is adopted rather than algebraic closure models.
The progress variable equation has been augmented with a sub-model
based on the autoignition delay time parameter, which is crucial for
capturing local explosions. Turbulence modeling is based on RANS. For
sharp resolution of shocks, the conservative form of governing equa-
tions has been adopted. Relatively under-resolved numerical grid has
been employed with the objective of establishing its scalability poten-
tial for large-scale computations. The TFC approach is strictly valid for
fully turbulent flames. In the present work, its applicability for flame
acceleration and DDT in obstructed channels has been investigated.
Initial testing has been carried out for a closed and circular shock tube
fitted with a single concentric obstacle. Further, a detailed study has
been carried out for the GraVent explosion channel. Based on the
validation of (1) flame speed variation during flame acceleration, (2)
final detonation speed and (3) incident and reflected shock pressures,
the capabilities and limitations of the approach have been presented.
For the range considered in the present study, reasonably good pre-
dictions have been obtained with no tuning/calibration of model
parameters. The model is able to capture flame acceleration and
predict the conditions under which DDT can take place. However, it
is further observed that actual DDT mechanism could not be
reproduced.
```
```
ARTICLE HISTORY
Received 10 May 2024
Revised 3 September 2024
Accepted 21 September 2024
KEYWORDS
Turbulent Flame Closure
(TFC); Flame-wrinkling;
Autoignition; Flame
Acceleration (FA);
Deflagration-to-Detonation
Transition (DDT)
```
**Introduction**

Under a postulated severe accident scenario for a water-cooled nuclear reactor, combus-
tion/detonation of hydrogen–air gas mixture is a known hazard (Kuznetsov et al. 2015 ).
Hydrogen–air mixture is hazardous due to its low ignition energy, wide flammability limits
and high chemical reactivity (Crowl and Jo 2007 ). The Fukushima nuclear accident (Holt,
Nikitin, and Campbell 2012 ) is an example of the risk associated with hydrogen explosions.
Hydrogen safety engineering is a very broad field that encompasses a wide range of physical
phenomena (Saffers and Molkov 2014 ). The scope of present work is in the numerical

**CONTACT** Aditya Karanam adityakb@barc.gov.in Homi Bhabha National Institute, Aditya Karanam, Room-330, Hall-
7, BARC, Trombay, Mumbai 400085, India

COMBUSTION SCIENCE AND TECHNOLOGY
https://doi.org/10.1080/00102202.2024.

© 2024 bhabha atomic research centre


modeling and prediction of the combustion-related phenomena of Flame Acceleration (FA)
and Deflagration-to-Detonation Transition (DDT).
Hydrogen combustion initiates as a laminar flame. The volume expansion across the
flame front displaces the reactant mixture, causing the flame to accelerate when observed
from the laboratory frame of reference. Expanding hydrogen flames are intrinsically
unstable due to cellular instabilities (Law, Jomaas, and Bechtold 2005 ). Moreover, hydro-
dynamic and gas-dynamic instabilities arising from the boundary layer can lead to produc-
tion of unsteady and turbulent regions upstream of the flame. The role of turbulence and its
interaction with the flame varies depending on particular experimental conditions.
Liberman et al. ( 2010 ) have carried out experimental and computational studies in an
unobstructed detonation tube of rectangular cross-section initially filled with
a stoichiometric hydrogen–oxygen mixture. It was found that flame acceleration does not
require turbulence and was caused only by increase in flame surface area due to stretching
within the boundary layer. The initial flame acceleration was found to be exponential and
produced weak shocks far upstream of the flame. Subsequently, a period of slower flame
acceleration and wave steepening directly on the flame front was observed. During this
stage, formation of a preheat zone resulted in a strong shock capable of triggering
a detonation. Finally, an abrupt increase in velocity and formation of detonation were
observed. For a wide range of initial pressures, the upstream flow remained laminar until
the transition to detonation. Experimental investigation by Boeck ( 2014 ) in an unobstructed
channel reconfirmed that the bulk of the flame propagation took place in a laminar flow
field, and flame stretching effects due to turbulence were restricted to within the wall
boundary layer.
In an obstructed channel, separation and rotational flow associated with flow over
obstructions can lead to an earlier transition to turbulence compared to a smooth
channel. Shepherd and Lee ( 1992 ) have reported that obstacles provide an extremely
efficient means of converting the mean flow to large-scale turbulent motions. During
flame acceleration experiment in an obstructed channel initially filled with hydrogen–air
mixture, Boeck ( 2014 ) reported both laminar and turbulent regions upstream of the
flame. For a low initial hydrogen concentration (12.5%), the average flame tip speed was
low, and turbulence in the wake of the obstacle was almost invisible. In this case, the
turbulent regions were confined to within the boundary layers of the channel walls. As
the flame passes through the obstacle, it contracts strongly, thereby enlarging its
macroscopic surface area and the associated energy release. This effect of flame folding
is an additional factor for flame acceleration in case of an obstructed channel compared
to a smooth channel. As the hydrogen concentration was increased to 15%, the average
flame tip speed also increased and turbulent regions were visible in the flow upstream of
the flame in shadowgraph images. Moreover, the turbulence in the wall boundary layer
got transported to the bulk of the channel due to deflection by the obstacle (Boeck
2014 ). Flame passage in a turbulent region causes flame surface wrinkling at a smaller
scale, which gets superposed on the macroscopic flame folding effect. For hydrogen
concentration of 20%, Boeck ( 2014 ) reported an average flame tip speed of 300 m/s
approaching the obstacle and clear turbulent regions upstream of the flame. The
shadowgraph image obtained by Boeck ( 2014 ) shows that the flame front gets intensely
wrinkled at very small scales such that the Karlovitz number Ka> 1 , corresponding to
the “thin reaction zones” regime on the Borghi diagram. This suggests that there is

2 A. KARANAM AND V. VERMA


indeed a turbulence-flame interaction in the wake of the obstacle. The role of obstacles
in promoting turbulence has also been reported by Gamezo, Ogawa, and Oran ( 2007 ).
Ciccarelli and Dorofeev ( 2008 ) have reported significant randomization and turbulence
of the flow ahead of the flame resulting in shortening of the run-up distance in
obstructed tubes compared to smooth tubes. It must not be construed that the flow
field is homogenously turbulent in the whole domain, but rather, local turbulent regions
seem to form upstream of the flame in case of a high-speed flame propagation in an
obstructed channel. The ensuing feedback mechanism between turbulence and flame
surface enlargement (micro and macroscopic) causes significant flame acceleration and
can be quantified using the artifact of the turbulent burning velocity.
Both laminar and turbulent flames are subsonic expansion combustion waves and
classified as deflagrations. Geometric confinement can lead to a sustained flame accelera-
tion and formation of precursor shocks. Considering this, deflagrations are categorized as
“Slow” or “Fast.” In the former, the flow is entirely subsonic, while in the latter, flame
propagation may be supersonic with respect to the far-stream unburned gases but still
remains subsonic with respect to the pre-compressed reactants feeding the flame. The flame
speed of a fast deflagration is an order-of-magnitude higher than a slow deflagration. Here,
flame speed refers to the propagation speed of the flame w.r.t the fixed laboratory frame of
reference.
As a fast deflagration undergoes further flame acceleration, it can lead to a rapid
deposition of energy in the mixture and generate a strong precursor shock wave ahead of
it. The reactant parcels that pass through this shock get compressed according to Hugoniot
and may undergo autoignition after an induction delay time or Autoignition Delay Time
(ADT). ADT is the time elapsed between the instant at which a reactant parcel is shocked
and when autoignition or local explosion occurs. The fate of the explosion, i.e., whether it
gets amplified or attenuated, is determined by the gas-dynamic coupling between the
leading precursor shock and the trailing reaction zone. In this regard, three cases have
been distinguished by Shepherd and Lee ( 1992 ). In the subcritical case, the chemical energy
released in the reaction zone does not significantly contribute to the shock motion, resulting
in its decay. Thus, ADT of shocked reactant parcels increase and the local explosion gets
extinguished due to insufficient energy received from the lead shock. The reaction wave lags
behind the shock, the separation increasing with time and ultimately decouples and remains
as a fast deflagration. The subcritical case corresponds to failure of DDT. In the supercritical
case (direct detonation), the shock and reaction zone are strongly coupled from the very
beginning and can be initiated using a high energy explosive charge. Direct detonation
initiation is not in the scope of the present work. Under the critical case, the reaction wave
travels on a parallel trajectory to the lead shock. The engulfed gas in between is a highly
sensitized region in which local explosion or hotspot formation can take place. The
displacement effect of the local explosion produces a secondary shock wave ahead. Under
certain conditions, the trailing reaction zone, the intermediate secondary shock and the lead
shock all merge to form an overdriven detonation (Shepherd and Lee 1992 ). Alternatively,
a number of discrete hotspots may also form and merge into a detonation (Shepherd and
Lee 1992 ). The critical case corresponds to the Deflagration-to-Detonation Transition
(DDT). DDT process is explained in detail by Shepherd and Lee ( 1992 ) and more recently
by Oran and Gamezo ( 2007 ), Ciccarelli and Dorofeev ( 2008 ), Liberman et al. ( 2010 ) and
Oran ( 2015 ).

```
COMBUSTION SCIENCE AND TECHNOLOGY 3
```

A schematic of the physical phenomena, transition mechanisms and order-of-magnitude
flame speed of different flame propagation regimes has been illustrated in Figure 1.
Considering the multitude of physical effects involved in DDT, a state-of-the-art report
was compiled by Breitung et al. ( 2000 ). A similar but more recent compilation was released
by the International Atomic Energy Agency (IAEA) (Park 2011 ). According to these reports
and the references therein, empirical correlations have been developed to predict FA and
DDT. Two such empirical correlations that are widely used are the σ and λ criteria. The
former relates the expansion ratio (σ) across the flame front to its propensity to transition to
a fast deflagration, while the latter gives a criterion for DDT to take place based on the ratio
of the cell width of the detonation to the characteristic length scale of the domain. For
complex geometries, it is difficult to define the characteristic length scale. Also, there is no
universal rule that such a length scale exists. Moreover, empirical criteria have been
established through highly controlled experiments with known and well defined initial
and boundary conditions. It is highly likely that local conditions may prevail that are
outside the range of applicability of these empirical criteria. Thus, these criteria are
necessary only but not sufficient. Whether FA and DDT will actually take place is not
known a-priori, and a case-by-case evaluation is required to unambiguously determine the
combustion regime and its consequences.
To overcome the limitations of empirical criteria, there is a need for detailed numerical
modeling based on the reactive flow Navier-Stokes (NS) equations (Oran and Boris 2000 ;
Veynante and Vervisch 2002 ). Some examples of fully resolved numerical modeling of DDT
process have been presented by Khokhlov, Oran, and Thomas ( 1999 ), Khokhlov and Oran
( 1999 ) and Gamezo, Ogawa, and Oran ( 2007 , 2008 , 2009 ). The review paper by Oran and
Gamezo ( 2007 ) provides a comprehensive description of numerical modeling to understand
the mechanisms involved in DDT. These simulations highlight the importance of condi-
tions created by shock-flame interactions under which DDT can take place. Liberman et al.
( 2010 ) carried out experimental and computational studies to show that DDT occurs
through three processes: (1) flame acceleration to produce a shock wave, (2) formation of
large amplitude pressure pulse at the flame surface and (3) actual transition to detonation.

**Figure 1.** Illustration of physical phenomena, transition mechanisms and order-of-magnitude propaga-
tion speed of different flame propagation regimes.

4 A. KARANAM AND V. VERMA


Kiverin, Ivanov, and Liberman ( 2012 ) carried out high-resolution two-dimensional numer-
ical simulation with detailed chemical kinetics to simulate DDT through shock-flame
interaction under incident and reflected shocks. More recently, Jian and Jianguo ( 2018 )
employed reactive Euler equations with detailed reaction mechanism to model reflection of
detonation over a cylindrical surface and scattering range was established. Zhang, Li, and
Liu ( 2022 ) and Yang and Zhang ( 2023 ) have investigated formation and propagation of
detonation by shock wave focusing. They identified formation of deflagration, quasi-
detonation and direct detonation depending on the intensity of incident shock wave.
These simulations also fortified the importance of local hot-spots and transverse waves in
the onset and maintenance of detonation waves.
While there is scientific merit in fully resolved modeling of DDT, their extensibility to
larger domains is not practical due to the limitations set by Moore’s law of scaling.
Therefore, practical cognizance mandates use of modeling methods based on mechanistic
considerations underlying FA and DDT, which are applicable to relatively coarse grids. The
numerical algorithm should be able to capture the transition between parabolic (subsonic)
to hyperbolic (supersonic) governing equations. For this purpose, the report titled “Status
Report on Hydrogen Management and Related Computer Codes” (Liang et al. 2014 ), issued
by the Nuclear Energy Agency (NEA), cites specialized Computational Fluid Dynamics
(CFD) codes like TONUS (Kudriakov et al. 2008 ), GASFLOW-MPI (Xiao et al. 2017 ) and
FLACS (Arntzen 1998 ), among others.
TONUS (Kudriakov et al. 2008 ) uses compressible NS equations at a low Mach number
and switches to Euler equations at a high Mach number. Flame front tracking is based on
the reaction progress variable. For combustion modeling, an Arrhenius type model for
laminar flames and Eddy Break-Up (EBU) concept (Spalding 1971 ) for turbulent flames is
implemented. For detonations, Arrhenius global reaction rate or the CREBCOM (Efimenko
and Dorofeev 2001 ) model is implemented. However, as per the authors (Kudriakov et al.
2008 ), the model parameters of EBU and the rate parameters of the global one-step reaction
require tuning/calibration from case-to-case basis.
GASFLOW-MPI (Xiao et al. 2017 ) is based on the fully compressible NS formulation for
all Mach numbers. Flame front propagation is again based on the reaction progress variable.
The source term is based on the one-step Arrhenius reaction rate. The authors of
GASFLOW-MPI state that the effective pre-exponential factor and activation energy
needs to be tuned to ensure that energy release rate is consistent with detailed reaction
modeling. Critically, the numerical solver is based on pressure-based segregated concept of
Pressure-Implicit with Splitting of Operators (PISO) that employs the pressure Poisson
equation. However, the highly dissipative character of the second derivative of pressure in
the Poisson equation can degrade discontinuous solutions (like shocks) quickly as noted by
Sathiah, Komen, and Roekaerts ( 2012 ). Moreover, segregated numerical strategy may not be
best suited in high Mach number flows in which physical coupling between density
(continuity equation), pressure (momentum equations) and internal energy (energy equa-
tion) is strong. In this regard, it may be stated that the actual implementation of PISO in
GASFLOW-MPI is robust such that all Mach number flows can be sharply captured; if the
mesh resolution is sufficiently fine.
The FLACS code (Flame Acceleration Simulator) (Arntzen 1998 ) is a specialized CFD
tool for safety applications – also based on the fully compressible NS equation with
a pressure-based solver. It employs a distributed porosity-based concept for grid generation

```
COMBUSTION SCIENCE AND TECHNOLOGY 5
```

with an artificial flame thickening approach (Colin et al. 2000 ) for deflagration modeling.
The thickening procedure allows propagation of the flame on a coarse grid but reduces
flame response to the smallest turbulent motions. This is corrected using an efficiency
function and an empirical thickening factor. Detonation modeling is based on the λ criteria.
Hence, conditions leading to DDT can be achieved, but DDT cannot be computed based on
mechanistic coupling between gas-dynamics and autoignition.
While the codes TONUS (Kudriakov et al. 2008 ), GASFLOW-MPI (Xiao et al. 2017 ) and
FLACS (Arntzen 1998 ) are highly established and well validated, some tuning/calibration of
model constants and manual switching of solver seems to be unavoidable. This is not
favorable, especially for hydrogen flames in which transition between different regimes can
take place (see Figure 1 ). Also, these codes are proprietary and often closed source and
impede the wider development and validation of practically relevant simulation approaches.
Thus, there is a need for development of models that require no tuning of parameters for
simulation of different regimes of combustion and the transition from one to the other. In
the present work, the open-source numerical platform OpenFOAM (Weller et al. 1998 ) has
been adopted for this purpose.
Heidari and Wen ( 2014 ) and Wang and Wen ( 2017 ) have previously used OpenFOAM
for FA and DDT simulations. In these works, the reaction rate was based on a single-step
global reaction of the Arrhenius type, which required carefully tuned rate parameters for
accurately modeling heat release rate. Emami et al. ( 2015 ) used detailed reaction kinetics
modeling within OpenFOAM, but this approach was highly computationally expensive for
larger domains. More recently, Povilaitis and Jaseliunaite ( 2021 ) developed an OpenFOAM
based solver with the Turbulent Flame Closure (TFC) approach. Since autoignition effects
were not considered, the solver could be applied only for flame acceleration phase but not
for modeling DDT. The notable work of Ettner, Vollmer, and Sattelmayer ( 2014 ) also
applies the TFC approach for flame front tracking but includes a separate source term for
autoignition effects. The formulation provided by Ettner, Vollmer, and Sattelmayer ( 2014 )
has been used as the basis for the present work.
The objective is further development of Turbulent Flame Closure–based modeling of FA
and DDT with specific emphasis on minimizing parameter tuning and applicable for large-
scale computation. For model testing, two shock tube channels for which experimental data
are available have been chosen. Several parametric simulations have been carried out for
validation. A detailed analysis of the interaction between flame zone, pressure waves and
precursor shocks has been presented to explain the DDT process. The mathematical
modeling, numerical details, numerical results and some concluding remarks are presented
in this paper.

**Mathematical modeling**

Mathematical modeling of premixed turbulent combustion depends on the Damköhler
number defined as Da¼τt _=_ τc (ratio of turbulent time scale τt to chemical time scale τc)
(Peters 2000 ). In previous work (Karanam, Ganju, and Chattopadhyay 2020 ), the authors
had carried out numerical computation to map variation of the Damköhler number on the
Borghi diagram. It was determined that the Damköhler number is much larger than unity
(Da�1) for the kind of flame propagation considered in the present study. Under such
conditions, the flame is assumed to be a surface convected and wrinkled by the flow field. Its

6 A. KARANAM AND V. VERMA


propagation can be modeled using a transport equation for the progress variable (c). Values
of c¼ 0 and c¼ 1 correspond to unburned and burned mixture respectively. Effect of
turbulence if any can be accounted using the RANS formulation. Due to variation in
density, the Favre-averaging procedure is employed. Flame tracking relies on the transport
equation for the Favre-averaged progress variable hcishown in Eqn. 1. A similar approach
for flame tracking has been successfully adopted by Ettner, Vollmer, and Sattelmayer
( 2014 ), Hasslberger, Boeck, and Sattelmayer ( 2015 ) and Hong et al. ( 2015 ).

The turbulent diffusivity DT is modelled using the eddy viscosity μT and the turbulent
Schmidt number (ScT). The eddy viscosity is obtained from the turbulence model. As the
turbulent Schmidt number (ScT) has no direct physical interpretation, its value is based on
the specific application. In the present work, ScT¼ 1 has been used based on the recom-
mendation of Hasslberger, Boeck, and Sattelmayer ( 2015 ). For a highly turbulent flow field,
DT�DL. On the contrary, in regions of low turbulence, the eddy viscosity and hence the
turbulent diffusivity also tend to zero. The diffusion term is then dominated by the laminar
component DL only.

The source term (ω_) appearing in Eq. 1 represents the mean reaction rate and is modeled
using the Turbulent Flame Closure (TFC) approach proposed by Zimont ( 2000 ).

The Zimont’s model is applicable under high turbulence intensity; therefore, its use is an
approximation in scenarios where both laminar and turbulent flame propagation regimes
may exist during different instants of time. For fully laminar flame propagation, the use of
Zimont’s model leads to high errors. However, for flame propagation in ducts with obstacles,
regions of high turbulence may appear upstream of the flame (Boeck 2014 ; Breitung et al.
2000 ; Ciccarelli and Dorofeev 2008 ; Gamezo, Ogawa, and Oran 2007 ). Under these condi-
tions, the model may be applied. Ideally, the most accurate way is to use instantaneous
reactive flow NS equations with a detailed reaction mechanism and multi-component trans-
port formulation on a very fine grid such as by Ivanov et al. ( 2013 ). However, for engineering
applications, a reasonable compromise between accuracy and scalability has to be pursued.
The present approach seems to be a good candidate in this regard.
The Zimont’s model assumes that the mean turbulent flame propagates in the local
normal direction to the iso-hcisurface with rate of propagation depending on the turbulent
burning velocity (ST) and unburned mixture density (�ρu). The turbulent burning velocity is
a derived quantity introduced to capture the effect of turbulence on the augmentation of
laminar burning velocity. For closure of ST, the flame-wrinkling factor (χ) concept (Peters
2000 ) is applied, χ;AT _=_ A, where AT is the instantaneous turbulent flame surface area and A
is the cross-sectional area projected onto the mean propagation direction. From the con-
tinuity of mass flux, AT _=_ A¼ST _=_ SL\χ¼ST _=_ SL. This approach facilitates the closure of the

mean reaction rate source term (ω_) of Eqn. (1), if a formulation for χ is available. SL is the

```
COMBUSTION SCIENCE AND TECHNOLOGY 7
```

temperature and pressure dependent laminar burning velocity as per Eqn. (4). The refer-
ence laminar burning velocity (SL _;_ o) at standard conditions (298 K, 1.013 bar) is obtained
using the polynomial expressions provided by Ettner, Vollmer, and Sattelmayer ( 2014 ). To
improve prediction at high turbulence intensities, a quenching factor (Q) is incorporated to
account for local quenching effects associated with small-scale flame stretching and mod-
eled as per Polifke, Flohr, and Brandt ( 2002 ) and Hasslberger, Boeck, and Sattelmayer
( 2015 ).

The large-scale effects such as macroscopic enlargement of flame surface due to gradients in
the flow (flame folding) evolve as a solution during the numerical computation and do not
require a sub-grid-scale modeling, but due to the use of RANS, different scales of turbulence
cannot be discerned. Thus, the microscopic flame enlargement due to smaller scales (flame
wrinkling) needs to be modeled using sub-grid-scale modeling. This ensures that while the
sub-grid wrinkling is not captured, its effects on enhanced burning rate and effective flame
speed are still accounted using mean flow quantities. A common approach for large scale
computation is to use algebraic closure correlations for modeling the flame-wrinkling term.
In previous works (Karanam, Sharma, and Ganju 2018 ; Karanam, Verma, and
Chattopadhyay 2024 ), the authors had validated the Gülder’s algebraic closure relation
(Gülder 1991 ; Henriksen et al. 2021 ) for studying flame propagation in a shock tube and
large-scale geometries. While the validity of the model was acceptable for a fixed concen-
tration, a key limitation was that the model parameters required tuning/calibration for
other concentrations. As discussed earlier, such models are applicable only to controlled lab
experiments, but of limited use in real accident scenarios. To overcome this limitation,
a generalized transport equation proposed by Weller ( 1993 ) has been adopted, described in
Eqn. (5), where χ is understood to be Favre-averaged quantity. Compared to algebraic
closure, a transport equation for χ is more general and accounts for non-local effects of
turbulence-chemistry interaction that are especially important for accelerating flames.

For modeling the generation (GχÞand reduction (Rχ) source terms, Weller ( 1993 ) has
proposed closure relations shown in Eqn. (6). The term χeq is the equilibrium flame-

wrinkling, i.e., flame-wrinkling when source and sink terms balance.

Hasslberger, Boeck, and Sattelmayer ( 2015 ) showed that the original formulation of Weller
(Weller 1993 ) for modeling χeq underpredicted flame acceleration especially for lean
mixtures. This deficiency was attributed to insufficient modeling of thermo-diffusive
flame instabilities and its effect on the turbulent burning velocity.
In the present work, to improve predictive capability over a range of mixture conditions,
the equilibrium flame-wrinkling has been modeled using the closure model proposed by
Dinkelacker, Manickam, and Muppala ( 2011 ), as shown in Eqn. (7). The model accounts for
thermo-diffusive instabilities through its dependence on the Lewis number (Le), which is

8 A. KARANAM AND V. VERMA


particularly important for lean mixtures. The model of Dinkelacker, Manickam, and
Muppala ( 2011 ) has been endorsed by Hasslberger, Boeck, and Sattelmayer ( 2015 ) for large-
scale simulations.

In the limit of low turbulence (u^0 !0), the diffusion term on the r.h.s. of Eqn. (1) tends to
its laminar counterpart. Then, Eqn. (7) yields χeq!1, which implies a consistency between

the turbulent and laminar burning velocities (ST!SL). However, the mean reaction term is
still modeled using the TFC equation (Eqn. 3), which is strictly valid for highly turbulent
combustion. Thus, the inherent limitation of the model may lead to errors in scenarios in
which laminar transport is the dominant mechanism such as unobstructed channels. The
model may also not be applicable for obstructed channel in which the flame speed is low
enough.
For modeling of the autoignition phenomena, Ettner, Vollmer, and Sattelmayer
( 2014 ) proposed augmenting the progress variable transport equation (Eqn. 1) with an
additional source term. Autoignition occurs after the expiry of local Autoignition Delay
Time (ADT), which is a function of local temperature, pressure and mixture composi-
tion (Glassman, Yetter, and Glumac 2014 ). In flows involving shock waves in
a combustible mixture, the sudden jump in pressure and temperature across a shock
wave is a typical region where autoignition may occur. Based on the method proposed
by Ettner, Vollmer, and Sattelmayer ( 2014 ), ADT is computed using the detailed
reaction mechanism of Óconaire et al. ( 2004 ) and tabulated in the form of a multi-
dimensional lookup table. The table is generated a priori and made run time available to
the solver. The flow solver queries the local ADT in each computational cell for a given
time using the dimensionless induction parameter τ¼t _=_ ADT (Michel, Colin, and
Angelberger 2010 ). For τ¼ 1 for a given computational cell, the mixture is considered
to be ignited. For earlier time instants (t _<_ ADT;\τ _<_ 1 ), there is no autoignition source
term. This can be implemented using the Heaviside function Hðτ  1 Þas per Ettner,
Vollmer, and Sattelmayer ( 2014 ). To account for transport and mixing effects,
a transport equation for τ is solved as presented in Eqn. 8. In Eqn. 8, τ is understood
to be Favre-averaged quantity.

To compute the autoignition source term, a typical transient profile of
c¼ðT  TuÞ _=_ ðTb  TuÞis considered during autoignition as shown in Figure 2. Two
zones have been demarcated – induction zone in blue (t _<_ 0 _:_ 06 ms) in which the progress
variable is close to initial value of zero and the ignition zone in red (0 _:_ 06 ms _<_ t _<_ 1 ms) in
which the progress variable changes from 0 to 1. The time scale associated with the
induction zone (tind) is 0.06 milliseconds, and the time scale associated with ignition (tign)
is 0.15 milliseconds.
Using these time scales, an analytical profile is used (Eqn. 9) to approximate the ignition
transient. The analytical profile is also presented in Figure 2 and closely matches the

```
COMBUSTION SCIENCE AND TECHNOLOGY 9
```

computed profile only in the ignition zone. In Eqn. 9, c is understood to be Favre-averaged
quantity.

The source term – rate of change of cðtÞcan be written as c_ðtÞ¼ð 1   cðtÞÞ _=_ tign. Since
induction zone also needs to be considered, the overall source term due to autoignition is
1  c
tignHðτ ^1 Þ;c;cðtÞ. The term τ is computed using Eqn. 8. The Heaviside function H
ensures that when τ _<_ 1, the source term is zero, such that the analytical and computed
profiles match in the induction zone. The autoignition source term is augmented in the
progress variable transport equation to assemble the final form shown in Eqn. 10.

The proposed mathematical modeling does not directly address various chemical reactions
occurring in flames and autoignition, but assumes their universal character and accounts
for their effects on the mean reaction rate using mechanistic considerations. Use of Weller’s

**Figure 2.** Computed and analytic profiles for progress variable (c) during induction and ignition phases of
a 0D isochoric combustion process.

10 A. KARANAM AND V. VERMA


transport equation (Weller 1993 ) for flame-wrinkling, Dinkelacker’s model (Dinkelacker,
Manickam, and Muppala 2011 ) for equilibrium flame-wrinkling, autoignition modeling
based on detailed reaction mechanism of ÓConaire (Óconaire et al. 2004 ) and the auto-
ignition source term as per Ettner (Ettner, Vollmer, and Sattelmayer 2014 ) minimize the
need for case-by-case parameter tuning. Use of RANS and efficient SGS models makes the
model scalable to large scale computations. These are in-line with the objectives of the
present work.

**Details of experimental facilities**

For numerical validation, two experimental facilities available in the open literature have
been considered.
The first is a relatively simpler shock tube facility of Knudsen ( 2006 ) with only one
obstacle. The facility is a fully closed horizontal shock tube channel with length of 4 m and
internal diameter of 107 mm, shown schematically in Figure 3. The channel has a provision
to install a concentric obstacle at a distance of 1 m from the ignition end (Ign). The obstacle-
opening diameter (do) can be varied. A smaller opening diameter provides higher blockage
to flame propagation. The high confinement of the channel and flame propagation through
the obstacle can lead to DDT (Knudsen 2006 ). Due to these effects, this facility is suitable for
initial testing and validation of the proposed combustion modeling.
Knudsen (Knudsen 2006 ) has reported that DDT occurs in mixture with 35% by volume
(i.e., v/v) of hydrogen and for obstacle-opening diameter of 30 mm. Further, Vaagsaether,
Knudsen, and Bjerketvedt ( 2007 ) have confirmed through numerical simulation that the
obstacle creates a supersonic jet behind it in which DDT occurs. Thus, this configuration
has been chosen for numerical validation in the present work. For parametric studies,
obstacle-opening diameters of 30 mm, 50 mm and 70 mm and hydrogen concentration in
range of 25%−40% (v/v) have been considered. Obstacle-opening diameter of 30 mm
provides the maximum blockage and 70 mm provides the least blockage. The initial con-
ditions have been taken to be 293 K and 1 atm. The basic validation results and parametric
studies for this facility have been provided in the section “Numerical results 1.”
The second facility used for validation is the GraVent facility (Boeck et al. 2016 ), which
has multiple obstacles along flame propagation path. Comprehensive experimental data on
flame acceleration and DDT obtained from this facility have been made available in the
“GraVent DDT Database” by Boeck et al. ( 2016 ). The facility is an entirely closed shock tube
channel of high aspect ratio with a rectangular cross-section. Length of the channel is 5.1 m

**Figure 3.** Schematic diagram of shock tube experimental facility of Knudsen ( 2006 ). Not to scale.

```
COMBUSTION SCIENCE AND TECHNOLOGY 11
```

and height is 0.06 m. The mixture is ignited at one end of the channel and the flame
propagation characteristics are studied along the channel length. The channel has
a provision to include obstacles at regular intervals along its length to induce turbulence
in the flow to assist flame acceleration. There are seven obstacles with the first one being at
0.25 m and distance between successive obstacles is 0.3 m. The final obstacle is at 2.05 m
from the ignition end. The blockage provided by the obstacles can be varied to 30% or 60%.
The setup also has a provision to create a transverse (normal to flow direction) gradient of
initial hydrogen distribution (i.e., prior to ignition) to capture the effects of stratification on
FA and DDT. A schematic of the experimental setup is shown in Figure 4.
The facility is equipped with optical measurement and photodiodes to measure flame
arrival and pressure transducers to record the pressures at various stations along the
direction of flame propagation. Further details on the exact location of the measuring
instruments can be found in Boeck et al. ( 2016 ).
Of the several experiments carried out in the GraVent facility, one case for which DDT
was reported has been chosen for numerical simulation and validation in the present work.
In this case, the initial hydrogen concentration is 22.5% and distributed homogeneously in
the domain (i.e., without transverse gradient). Blockage ratio provided by obstacles is 30%.
The initial conditions in the channel are 293 K and 1 atm. For a similar configuration with
hydrogen of 20%, Boeck ( 2014 ) has reported turbulent flame propagation with the Karlovitz
number Ka> 1 , which suggests the presence of fine-scale turbulence. To capture the
resulting augmentation of flame speed, the Zimont’s model (Zimont 2000 ) has been
adopted in the present work. The validation results and discussion on the mechanism of
DDT have been provided in the section “Numerical results 2.”

**Numerical setup**

Since both channels considered are fully closed, there are no in-flow or out-flow boundaries.
All external boundaries are modeled as adiabatic walls with no-slip. The tube wall is
modeled as adiabatic since the flame propagation is much faster compared to heat transfer
time scale. Neumann boundary conditions have been imposed for other variables. Ignition

**Figure 4.** Schematic diagram of the GraVent shock tube experimental facility of Boeck et al. ( 2016 ).

12 A. KARANAM AND V. VERMA


is effected by patching a spherical region of radius 40 mm with temperature equal to the
adiabatic flame temperature and a unit progress variable at the ignition location.
The combustion process is characterized by the progress variable (c¼ 0 in the reactant
mixture and c¼ 1 in the product mixture). The transport equation for the progress variable
(Eqn. 1) is solved for flame tracking. Additionally, the solver employs the continuity, NS
equations and the specific internal energy equations. The solution process yields the
temperature, density and progress variable in each computational cells of the domain.
The pressure is computed from the ideal gas equation-of-state. Once the thermodynamic
conditions for a given cell is known, the equilibrium species mass fractions are interpolated
from the lookup table that is generated a priori and made available to the solver. The JANAF
polynomials (Glassman, Yetter, and Glumac 2014 ) yield temperature-dependent specific
heats for a given species. The molecular transport properties are calculated using the
Sutherland’s formula (Glassman, Yetter, and Glumac 2014 ). Then, mixture-averaged for-
mulation is used to derive the mixture average properties in each cell. The influence of
gravitational force has been neglected considering high-speed flow.
Turbulence is modeled using Menter’s SST k  ω two-equation RANS model (Menter
1994 ) due to its good performance in both near-wall and bulk flow regions. Since the flow is
initially undisturbed, a low value of initial turbulent kinetic energy based on a turbulent
intensity of 1% has been used.
The spatial discretization has been achieved using cells with linear size of 3 mm, which is
quite under-resolved compared to the requirements for flame and shock resolving models.
Due to the use of efficient SGS modeling, the macroscopic flame and shock propagation
characteristics can still be obtained. Under-resolved grids with efficient SGS modeling
provide computational scalability for larger domains.
Numerical algorithm is based on density-based approach with the continuity equation in
its conservative form. As the continuity equation (in comparison to pressure Poisson
equation) does not have a diffusive term, it does not suffer from degradation of disconti-
nuities due to excessive dissipation. This is especially important when the underlying grid is
itself under-resolved. The pressure field is computed using the ideal-gas equation-of-state.
The density-based solvers are more efficient for highly compressible flows, particularly with
regard to shock wave capturing, which is crucial for autoignition phenomena. Use of
density-based approach and conservative governing equations has been endorsed by var-
ious researchers working on modeling of FA and DDT (Ettner, Vollmer, and Sattelmayer
2014 ; Gaathaug, Vaagsaether, and Bjerketvedt 2012 ; Hasslberger, Boeck, and Sattelmayer
2015 ; Vaagsaether, Knudsen, and Bjerketvedt 2007 ).
Owing to the predominant hyperbolic nature of strongly compressible flows, explicit
time stepping is applied. The time step was adaptively calculated during the solution based
on the maximum acoustic Courant number of 0.5 to ensure stable progress of the solution.
This resulted in an extremely small time step in the range of 0.1 microseconds to 0.
milliseconds. Acoustic Courant number is used so that pressure waves that are important
for shock formation and propagation are captured.
All simulations have been carried out on workstations equipped with Intel® Xeon®
processors with base frequency of 2.3 GHz and 12 parallel cores. Because OpenFOAM
can be compiled to run in parallel using Open MPI, it is straightforward to run simulations
on all 12 cores available in the machine. On an average, for a grid size with one million
finite-volume cells, it was observed that 1 millisecond of flow time requires approximately

```
COMBUSTION SCIENCE AND TECHNOLOGY 13
```

30 hours of CPU time when running on all 12 cores. This translates to around two weeks per
validation case for total transient of 10 milliseconds. Considering the small time step
induced by the stringent CFL criterion, and the complexity of capturing shock waves and
other governing equations, this seems to be a reasonable turn-around-time.
The combustion equations (Eqn. 1-10) are coupled with continuity, momentum, energy
conservation equations along with the turbulence equations (based on SST k  ω) and
ideal-gas equation-of-state to obtain the final solution. All equations have been discretized
with a second-order schemes and solved with a tolerance of 10 −6 or lower. By using linear
reconstruction within a computational cell, second-order accuracy is ensured.

**Numerical results 1**

This section presents the basic verification and validation of the code and some insights
obtained from parametric studies for the shock tube facility of Knudsen ( 2006 ).

**Basic verification and validation**

The flame trajectory obtained for a mixture with 35% (v/v) of hydrogen and obstacle-
opening diameter of 30 mm is depicted in Figure 5. The flame trajectory is obtained by
tracing the leading edge of the flame at different instants. The slope of this curve may be
interpreted as the flame speed and is shown in Figure 6. Here, flame speed refers to the
propagation speed of the flame w.r.t the fixed laboratory frame of reference. Flame speed is
~50 m/s at the beginning of the section and accelerates to ~500 m/s at an axial location of

**Figure 5.** Transient flame propagation and pressure profiles in a mixture with 35% (v/v) hydrogen and
obstacle-opening diameter of 30 mm.

14 A. KARANAM AND V. VERMA


0.5 m. As the flame front approaches the obstacle at 1 m, a tendency of axial stagnation may
be observed during which flame speed drops significantly. This may be attributed to flame
deceleration and change in direction as it approaches the obstacle. The flame trajectory is
overlaid with pressure traces (blue lines) at three representative locations of 1 m, 2 m and
3 m from the ignition end. The pressure traces correspond to over-pressure; and have been
offset along Y-axis to match the location of the pressure probe and scaled by a suitable
factor. At the location of obstacle (pressure trace at 1 m), a shock discontinuity can be
observed at ~6 milliseconds (ms). At this instant, the flame front can be observed to be
trailing the shock front. Coincident with the formation of shock front (at ~6 ms), the flame
speed shows an increasing trend. Based on pressure traces at 2 m and 3 m, the location of
the pressure discontinuity is coincident with flame position, indicating that propagation
mode is that of a detonation. Considering these observations, DDT may be postulated to
have occurred at the location of the obstacle. The exact location of DDT could not be
validated based on the present analysis, but the numerical interpretation is in line with
observations of Vaagsaether, Knudsen, and Bjerketvedt ( 2007 ), which also report that DDT
occurs in the wake of the obstacle. During detonation propagation, the average flame speed
in a 2–3 m section (Figure 6 ) of the channel is computed to be 2212 m/s and is in reasonable
agreement with the experimental detonation speed of 2033 m/s reported by Knudsen
( 2006 ).

**Figure 6.** Flame speed vs. flame position in a mixture with 35% (v/v) hydrogen and obstacle-opening
diameter of 30 mm.

```
COMBUSTION SCIENCE AND TECHNOLOGY 15
```

Under ideal conditions (1D, no heat loss to surroundings), the jump in pressure
across a detonation is a property of the initial conditions and can be computed
theoretically using RH (Rankine-Hugoniot) equations (Glassman, Yetter, and Glumac
2014 ). The pressure jump predicted by numerical modeling may be compared with this
theoretical value. The numerical pressure jump has been computed from 1.5 to 4 m of
the channel in steps of
0.5 m for hydrogen concentration of 35% (v/v) and the result is shown in Figure 7.
Upstream of 1.5 m has not been taken as there may be interference of flow with the
obstacle. A flat pressure profile may be observed up to 3.5 m with an average value of
1.36 MPa and a sudden jump of 2.9 MPa at the end of the tube. The initial flat profile
may be interpreted as an incident steady detonation wave, whereas at the end of the
tube, the sudden increase may be attributed to reflected shock wave reflecting from the
closed aft end of the tube. The theoretically computed values from SDT toolbox
(Browne, Ziegler, and Shepherd 2008 ) are 1.58 MPa for Chapman-Jouguet (CJ) detona-
tion and 3.79 MPa for normal reflected shock wave. Apart from some deviation
primarily due to numerical dissipation in a coarse grid, the computed values for both
incident and reflected phenomena are in line with theoretical estimates. Thus, it may be
inferred that the numerically obtained detonation is indeed a CJ detonation.

**Figure 7.** Numerically computed pressure at different axial locations of the channel for hydrogen
concentration of 35% (v/v).

16 A. KARANAM AND V. VERMA


**Parametric studies**

Further parametric and validation studies were carried out with experimental data
for various hydrogen concentrations and obstacle-opening diameters. Figure 8 (left)
shows validation at different hydrogen concentrations for a fixed obstacle-opening
diameter of 30 mm and the right part shows validation for a fixed hydrogen of 35%
(v/v) at different obstacle-opening diameters. Across the range of parametric studies
considered, the numerical results overpredict compared to experimental data with an
average error of ~10%. Considering the use of a coarse grid with high numerical
viscosity, the predicted numerical results seem to be reasonable. More importantly, it
is observed that the model requires no tuning/calibration of parameters for the
range considered.
The numerical flame trajectory comparison for different hydrogen concentrations for
a fixed obstacle-opening diameter of 30 mm is shown in Figure 9. In all cases, the flame
propagation is similar up to ~2 ms. At further instants, higher flame acceleration occurs in
a stoichiometric mixture (hydrogen of 30%) compared to rich (35%, 40%) or lean mixtures
(25%). Critically, for the stoichiometric mixture, DDT may be seen to occur at an earlier
instant. This trend seems to be plausible as the specific energy released in a stoichiometric
mixture is the highest.
Further explanation may be provided by computing the detonation time-of-arrival (TOA).
To this end, the time at which a pressure discontinuity appears is computed for different
locations along the channel. The procedure for extracting TOA is shown in Figure 10 for one
representative case with hydrogen of 35% (v/v) and obstacle-opening diameter of 30 mm. The
pressure traces (blue lines) correspond to over-pressure; and have been offset along Y-axis to
match the location at which pressure is extracted and scaled by a suitable factor. The red circles
mark the location of the pressure discontinuity and can be interpreted as a shock wave; or if it
coincides with the flame trajectory, then a detonation wave. For the case shown in Figure 10 , the
location of the discontinuity is coinciding with the flame and is therefore a detonation wave. The
corresponding time on the X-axis is then interpreted as the detonation time-of-arrival.

**Figure 8.** Validation with experimental data of Knudsen ( 2006 ) at fixed obstacle-opening diameter of
30 mm (left) and with fixed hydrogen concentration of 35% (right).

```
COMBUSTION SCIENCE AND TECHNOLOGY 17
```

The detonation TOA comparison for different hydrogen concentrations is shown in
Figure 11. Clearly, in case of 25% and 40%, the first detonation signature is obtained at the
2 m from the ignition end, whereas for 30% and 35% mixtures, detonation is formed at an
earlier location of 1.5 m. An earlier formation of detonation is indicative of higher compres-
sibility owing to higher flame acceleration in case of 30% and 35%. Detonation TOA is lowest
for the stoichiometric mixture. As the mixture becomes lean or rich, TOA increases. Based on
the TOA, observed trends for DDT may be correlated, i.e., a lower TOA implies earlier DDT.
Since experimental results for detonation TOA were not available, the computation of
detonation TOA is qualitative only, but the observed trends for different hydrogen con-
centrations seem to be physically plausible. The simple shock tube channel provided an
opportunity to test the model validity for a range of mixture conditions. A more detailed
study and validation follows in the subsequent section.

**Numerical results 2**

To augment the previous studies, validation with the GraVent experimental data (Boeck
et al. 2016 ) has been carried out for one particular configuration (hydrogen of 22.5%
uniformly distributed and with blockage ratio of 30%).

**Figure 9.** Flame trajectory comparison for different hydrogen concentrations for a fixed obstacle-opening
diameter of 30 mm.

18 A. KARANAM AND V. VERMA


**Validation results**

The numerically obtained flame speed and the corresponding experimental data are shown
in Figure 12. Here, flame speed refers to the propagation speed of the flame w.r.t the fixed
laboratory frame of reference. The numerical result has been obtained by first tracing the
flame position (leading edge) at different instants of time and then computing the flame
speed using linear interpolation between successive instants. The experimental data is the
mean of three repetitions of the experiment available in the GraVent DDT Database (Boeck
et al. 2016 ), and the standard deviation has been used to represent symmetric error. The
figure has been overlaid with sound speeds in reactant (387 m/s) and product (904 m/s)
mixtures, and the vertical lines (O 1 – O 7 ) demarcate the location of the seven obstacles. For
pressure analysis, four locations have been considered − 0.4 m, 1.4 m, 2.3 m and 3.2 m
marked as magenta triangles.
In the obstacle section (0–2.05 m), the data show a monotonous flame acceleration up to
~900 m/s. The numerical prediction is able to capture flame acceleration quite well up to the
third obstacle but shows an undulating trend for further obstacle section. At the end of
the obstacle section, the numerical flame speed is in reasonably good agreement with the
experimental value. Once the flame crosses the final obstacle, continued flame acceleration
is observed as corroborated with experimental data. For flame propagation in tubes with

**Figure 10.** Flame trajectory and pressure traces used to extract detonation TOA in a mixture with 35% (v/v)
hydrogen and obstacle-opening diameter of 30 mm.

```
COMBUSTION SCIENCE AND TECHNOLOGY 19
```

obstacles, it has been reported (Shepherd and Lee 1992 ) that unlike smooth tubes, the
transition to detonation is not abrupt and an almost continuous acceleration to the final
steady state flame speed is observed. Moreover, the presence of obstacles permits the flame
speeds over the entire range from slow deflagration to CJ detonation (Shepherd and Lee
1992 ). The numerical result also shows a continuously increasing flame speed after the final
obstacle and reaches a quasi-steady value through a peak. It is postulated that at the end of
the obstacle section, conditions are reached under which transition to detonation can take
place. The peak value predicted by the numerical model is 2634.6 m/s, which is within 5% of
the experimental peak value of 2514.2 m/s and within the experimental error. The location
of the peak is predicted in the smooth section of the channel and in-line with the experi-
mental observation. However, the predicted peak location is 0.65 m upstream compared to
the experimental value. The difference may be a limitation of the adopted sub-grid-scale
models or the coarse underlying grid used in the present work. Further, the final flame
speed from numerical simulation is 1900 m/s as opposed to the CJ detonation speed of 1788
m/s (Browne, Ziegler, and Shepherd 2008 ) for the 22.5% hydrogen-air mixture considered
in the study. This amounts to an error of 6.26%, which seems to be reasonable.
The numerical model is able to predict the overall trend of increasing flame speed (flame
acceleration) and then reaching a stable value through a peak. The final value is consistent
with the CJ theoretical estimate of 1788 m/s. The model is able to distinguish between energy

**Figure 11.** Detonation TOA for hydrogen (v/v) of 25%, 30%, 35% and 40%. Obstacle-opening diameter is
30 mm.

20 A. KARANAM AND V. VERMA


release rates in the obstacle and post-obstacle sections, thereby, the flame speed along channel
length and the peak value are consistent with experimental data. However, the location of peak
pressure and flame propagation in the aft section of the channel (4 m−5 m) needs to be
improved. Based on the comparison of flame speed along channel length with experimental
data and the final value with the CJ detonation speed, the numerical model has been further
validated.

**Discussion**

To further elucidate the flame propagation mechanisms in different sections of the channel,
it is useful to consider the pressure variation in conjunction with the flame position. In this
regard, four locations have been considered − 0.4 m, 1.4 m, 2.3 m and 3.2 m marked as
magenta triangles in Figure 12. The pressure prediction at these points is shown in
Figure 13. These correspond to overpressures that have been scaled appropriately and
shifted along the vertical axis to indicate the corresponding distance from the ignition
end. Figure 13 is overlayed with flame position as well to depict location of the flame relative
to the pressure traces.
At 0.4 m, the flame has accelerated to a considerable speed of ~132 m/s (Figure 12 ), but
still subsonic. Figure 14 depicts time sequence of contour plots for dynamic eddy viscosity

**Figure 12.** Validation of numerically obtained flame speed with experimental data of Boeck et al. ( 2016 ).

```
COMBUSTION SCIENCE AND TECHNOLOGY 21
```

overlaid with the flame surface (black lines) obtained using iso-value of c¼ 0 _:_ 5. As the
flame propagates, it induces forward motion in the upstream reactant mixture and forces it
to pass through the obstacle. This may lead to a region of higher eddy viscosity in the wake
of the first obstacle at 9 ms. At 9.5 and 10 ms, the flame itself passes through the obstacles
and shows significant folding. Flame folding due to passage through an obstacle may be the
reason for further flame acceleration. Moreover, the flame is observed to be entering
a region of higher eddy viscosity. It is speculated that local regions of high turbulence
may cause additional flame acceleration due to flame wrinkling but needs further substan-
tiation. At 10.5 and 11 ms, both flame folding and eddy viscosity have reduced. At 11 ms,
the leading edge of the flame is at 0.4 m as confirmed from the flame trace (Figure 13 ).
Moreover, the overpressure at 0.4 m (Figure 13 ) shows no sharp discontinuity. Thus, while
is flame is propagating at significant speeds, it is still subsonic and hence not sufficient to
create conditions for formation of pressure or shock waves. Based on these reasons, the
flame propagation may be categorized as a slow deflagration.
As flame propagates further through the obstacle section, flame acceleration continues
and becomes supersonic w.r.t reactant mixture in the wake of the third obstacle (marked (i)
in Figure 12 ). Following this immediately, the flame speed drops (marked (ii)) due to
expansion into the larger area chamber between O 3 and O 4. As the flame is obtaining
feedback from the upstream geometry and flow conditions, a characteristic of subsonic

**Figure 13.** Pressure traces at different locations along the channel overlaid with flame position.

22 A. KARANAM AND V. VERMA


flow, the flame speed is also subsonic as confirmed by point marked (ii). As the flame
accelerates through the fourth obstacle, it reaches a considerable supersonic (w.r.t reactant
mixture) speed of ~683 m/s at 1.25 m (marked (iii)), but still subsonic w.r.t product
mixture. At this point, compressibility effects are non-negligible and formation of weak
pressure waves are possible. This is confirmed by a time sequence contours of overpressure
shown in Figure 15. At 14.35 ms, the flame is passing 1.25 m at high speed of ~683 m/s. As
a result, local high-pressure regions are formed near the walls at 14.45 ms. Further, at 14.5
and 14.55 ms, a uniform high-pressure region with overpressure in the range of 4–8 bar may
be observed upstream of the flame. At 14.55 ms, the flame leading edge (F) is just ahead of
1.35 m, while the high-pressure region is between 1.4 m and the fifth obstacle. As the high-
pressure region is rather smeared and not a sharp discontinuity, it may be interpreted as an
incipient Pressure Wave (PW) or a weak shock wave. While physically even weak shocks are
sharp discontinuities, the smearing observed in the numerical simulation is an artifact of the
coarse underlying grid. The signature of these pressure waves is observed in the pressure
trace at 1.4 m as well (Figure 13 ) between 14.5 and 15 ms. Due to propagation in the
presence of weak shocks and flame speeds being supersonic w.r.t reactant mixture but
subsonic w.r.t product mixture, the flame propagation has transitioned to a fast
deflagration.
The fast moving flame front acts as a piston that displaces the gases ahead of it at very
high speeds and promotes the formation of several pressure waves. Upon continued flame
acceleration, these emanated pressure waves may coalesce into a precursor shock due to

**Figure 14.** Time sequence images depicting flame acceleration due to flame folding. Flame propagation
mode is slow deflagration.

```
COMBUSTION SCIENCE AND TECHNOLOGY 23
```

wave steepening. An instance of precursor shock formation is observed at 15.6 ms, as shown
in the overpressure contour (Figure 16 ). The leading edge of the flame ( **F** ) is approaching
the final obstacle (O 7 ) with flame speed of ~1017 m/s (marked (iv) in Figure 12 ). Upstream
of the flame, a strong shock (S) with overpressure of ~15 bar is observed at the obstacle
location. The shock signature is also visible at the 2.3 m location (Figure 13 ), which shows
a sharp pressure jump at ~15.85 ms. Figure 16 also depicts local regions with overpressure
of ~30 bar at the upstream edge of the obstacle. Clearly, this is a reflected shock (R)
reflecting from the obstacle. Reflected shocks create regions of high pressure and tempera-
ture where local explosion due to autoignition can take place. Thus, at the end of the
obstacle section, amenable conditions are created under which precursor shock formation
and local explosion can take place.
Whether the precursor shock gets amplified or attenuated depends on its coupling
with the local explosion. If the amount of energy released from the local explosion is
sufficient to sustain shock propagation and the rate of energy release corresponds to the
shock time scale, then a spontaneous coupling can take place. This phenomenon is
illustrated in Figure 17 , which shows time sequence shadowgraphy images obtained
from the GraVent DDT database (Boeck et al. 2016 ). The configuration is the same as in
the numerical simulation, i.e., 22.5% homogeneous hydrogen mixture with blockage
ratio of 30%. The first image is at a reference time and subsequent images are at
intervals of +0.05 ms. At the reference time, a precursor shock can be observed
approaching the final obstacle (O 7 ). At +0.05 ms, the shock is passing through the

**Figure 15.** Time sequence images depicting incipient pressure waves (PW) ahead of the flame front (F).
Flame propagation mode is fast deflagration.

24 A. KARANAM AND V. VERMA


obstacle region. The next image at +0.10 ms shows local explosion in the reflected shock
region at the upstream edge of the obstacle. Subsequently, at +0.15 ms and +0.20 ms,
a trailing reaction zone can be observed, finally culminating into a detonation at +0.25
ms. Based on experimental observations, DDT initiates as a result of local explosion
after shock wave reflection from the final obstacle.
In the numerical analysis, as shown in Figure 16 , both the precursor shock passing
through the final obstacle and reflected shock at the upstream edge of the obstacle are
captured. The numerical analysis is able to predict the conditions under which DDT can be
initiated. However, the subsequent strong gas dynamic coupling during DDT process itself
could not be reproduced in the numerical simulation.

**Figure 16.** Overpressure at 15.6 ms showing formation of precursor shock (S) ahead of the flame front (F)
and reflected shock (R).

**Figure 17.** Time sequence of shadowgraphy images obtained from the GraVent DDT database (Boeck
et al. 2016 ) illustrating the experimental DDT mechanism.

```
COMBUSTION SCIENCE AND TECHNOLOGY 25
```

The numerical DDT mechanism is depicted in Figure 18. At 15.9 ms, the flame ( **F** ) is seen
crossing 2.3 m and trailing a precursor shock ( **S** ) at ~2.4 m. A local explosion ( **E** ) of high
pressure (~35 bar) can be observed in the engulfed region between the flame and the shock.
At 16.0 ms, the pressure jump across the shock is much higher than 15.9 ms, suggesting that
shock amplification is occurring, presumably due to stronger coupling with the trailing
flame zone. A stronger shock can in turn causes a stronger local explosion. This can be
observed at 16.05 ms, which depicts a much stronger local explosion (~50 bar) in the
neighborhood of the flame. In the duration between 15.9 and16.05 ms, the flame and the
shock are two physically separated entities, although the flame-to-shock distance is redu-
cing. At 16.1 ms, the flame and shock coalesce to form a detonation wave ( **D** ) that
propagates into the unburned mixture. During the time from 15.9 to 16.1 ms,
a significant jump in flame speed can be observed (1500 m/s to 2600 m/s) from Figure 12.
The pressure spike that can be observed at the 3.2 m location (Figure 13 ) is a direct signature
of the detonation front. The discontinuity front tracked from the pressure trace exactly
overlaps with the flame front, which is consistent with a detonation wave.
There are a few critical differences in the experimental and numerical DDT mechanisms.
In the former, DDT is initiated due to a local explosion arising in the post reflected shock
mixture at the final obstacle. Subsequently, a strong gas dynamic coupling between the
precursor shock and the trailing flame zone is observed in the vicinity of the final obstacle –
ultimately leading to DDT. The numerical simulation is unable to capture this effect,
possibly due to the large numerical viscosity associated with the coarse underlying grid
and the excessive unphysical diffusion of shocks. The numerical simulation predicts DDT at
a further downstream location in the smooth section of the channel. The mechanism
involves a local explosion in the neighborhood the flame and shock formation at the
flame front itself. Since DDT is occurring in the smooth section of the channel, the
mechanism is more in line to the one proposed by Liberman et al. ( 2010 ) for smooth

**Figure 18.** Time sequence images illustrating the numerical DDT mechanism involving the flame (F),
shock (S), local explosion (E) and detonation (D) propagation.

26 A. KARANAM AND V. VERMA


channels. However, the combination of modeling aspects that seem to create conditions
under which DDT can take place, but fails to reproduce the actual DDT mechanism, needs
to be further investigated.

**Concluding remarks**

The present work investigated the numerical modeling of flame acceleration and DDT in
hydrogen air mixtures. Flame tracking was achieved using a transport equation for the
progress variable. The mean reaction rate was modeled based on the Turbulent Flame
Closure (TFC) relation proposed by Zimont ( 2000 ). For modeling sub-grid-scale flame
wrinkling, the generalized transport equation of Weller ( 1993 ) was adopted. The equili-
brium flame-wrinkling was computed using the correlation of Dinkelacker, Manickam, and
Muppala ( 2011 ). To model local explosions, a source term involving the autoignition delay
time parameter (Ettner, Vollmer, and Sattelmayer 2014 ) was appended to the flame tracking
equation. Effect of turbulence if any was accounted using the RANS formulation. For sharp
resolution of shocks, conservative form of the governing equations was adopted. The grid
discretization was relatively under-resolved. The dual objectives were to establish the
scalability potential and generality of the model for large-scale computations.
Numerical simulations were initially carried out for a circular shock tube with a single
concentric obstacle. Based on comparison of incident detonation and reflected shock
pressures with the corresponding CJ values, it was determined that the final propagation
was a CJ detonation. From parametric comparison with experimental data, the numerical
model overpredicted the detonation speed by ~10%. Considering the coarse grid with a high
numerical viscosity, an error of ~10% seemed to be reasonable. More importantly, the
model required no tuning of parameters, thus making it general.
A further detailed study was conducted with the GraVent explosion channel. Based on
a comparison of the numerical flame speed along channel length with corresponding
experimental data, the model was validated for a wide range of flame speeds. During slow
deflagration, flame folding due to passage through an obstacle was identified to be the flame
acceleration mechanism. Transition to a fast deflagration was observed in conjunction with
formation of pressure waves (weak shocks) ahead of the flame. With continued flame
acceleration, coalescence of pressure waves generated a precursor shock at the final obstacle.
Formation of the precursor shock and its reflection from the obstacle were found to be
consistent with experimental observations. Thus, numerical analysis was able to predict the
conditions under which DDT could be initiated. However, the experimental DDT mechan-
ism involving a local explosion arising in the post reflected shock mixture and its strong gas
dynamic coupling with the precursor shock could not be reproduced numerically.
While the model is not perfect in all aspects, it certainly does its intended role of
reproducing macroscopic parameters of interest such as (1) wide range of flame speeds
during flame acceleration, (2) final detonation speed and (3) incident and reflected shock
pressures. The model is tolerant to coarse underlying grid, requires no tuning of parameters
and runs within reasonable computational time, making it applicable for large scale
domains. The model provides a framework for further improvements to capture DDT
mechanism more adequately.
However, a few areas need further consideration. First, the present approach is not
applicable for laminar flame propagation or flame propagation under low turbulence level.

```
COMBUSTION SCIENCE AND TECHNOLOGY 27
```

In this regard, the role of turbulence or lack thereof during flame acceleration requires
further investigation. General applicability of the model for a variety of geometric condi-
tions including smooth channels needs to be addressed. Then, the model cannot be directly
applied to other fuels including hydrogen-blended fuels. From the numerical standpoint,
RANS with a coarse numerical grid may not be the best way to reproduce the actual DDT
mechanism. In this regard, adaptive meshing combined with LES will become necessary.
Finally, the sensitivity of individual parameters needs to be identified to strengthen the
argument for robustness of the model. With due consideration to these aspects, further
work will be carried out.

**Nomenclature**

**Latin Symbols**
c Progress variable (-)
do Obstacle-opening diameter (m)
k Turbulent kinetic energy (m^2 .s−2)
l Length scale (m)
t Time coordinate (s)
u Velocity (m.s−1)
x Spatial coordinate (m)
D Diffusivity (m^2 .s−1)
Da Damköhler number (-)
G Generation of χ (s−1)
H Heaviside function -
Le Lewis number (-)
P Pressure (kg.m−1.s−2)
Q Quenching factor (-)
R Reduction of χ (s−1)
Re Reynolds number (-)
S Burning velocity (m.s−1)
T Temperature (K)
**Greek Symbols**
σ Expansion ratio (-)
λ Detonation cell width
ω Specific dissipation rate (s−1)
ω _ Progress variable source term (kg.m−3.s−1)
ρ Density (kg.m−3)
τ Time scale (s)
χ Sub-Grid-Scale flame-wrinkling factor (-)
O Of the order (-)
**Subscripts**
b burned
c chemical
eq equilibrium
j tensor index
L laminar
o standard conditions (298 K, 1.013 bar)
T turbulent
u unburned
η Kolmogorov scale
**Superscripts**
ð�Þ Reynolds averaged

28 A. KARANAM AND V. VERMA


ð�Þ Favre averaged
ð�Þ^0 Reynolds fluctuating

**Acknowledgements**

The authors would like to thank Dr Deb Mukhopadhyay and Dr Jayanta Chattopadhyay for their
helpful comments during the preparation of this manuscript.

**Disclosure statement**

No potential conflict of interest was reported by the author(s).

**References**

Arntzen, B. J. 1998. Modelling of turbulence and combustion for simulations of gas explosions in
complex geometries. PhD thesis, Ref: The Norwegian University of Science and Technology.
Boeck, L. 2014. Deflagration-to-detonation transition and detonation propagation in H 2 -air mixtures
with transverse concentration gradients. PhD thesis, Germany: Technical University Munich.
Boeck, L. R., P. Katzy, J. Hasslberger, A. Kink, and T. Sattelmayer. 2016. The GraVent DDT database.
Shock. Waves. 26 (5):683–85. doi: 10.1007/s00193-016-0629-0.
Breitung, W., C. Chan, S. Dorofeev, A. Eder, B. Gerfand, M. Heitsch, R. Klein, A. Malliakos,
J. Shepherd, E. Studer, et al. 2000. Flame acceleration and deflagration-to-detonation transition
in nuclear safety. Technical report. OECD/NEA/CSNI/R7.
Browne, S., J. Ziegler, and J. E. Shepherd. 2008. Numerical solution methods for shock and detonation
jump conditions. Technical report, GALCIT report FM2006.006.
Ciccarelli, G., and S. B. Dorofeev. 2008. Flame acceleration and transition to detonation in ducts. Prog
Energy Combust. Sci. 34 (4):499–550. doi: 10.1016/j.pecs.2007.11.002.
Colin, O., F. Ducros, D. Veynante, and T. Poinsot. 2000. A thickened flame model for large eddy
simulations of turbulent premixed combustion. Phys. of Fluids 12:1843–1863. doi: 10.1063/1.
870436.
Crowl, D. A., and Y.-D. Jo. 2007. The hazards and risks of hydrogen. J. Loss. Prev. Process. Industries
20 (2):158–64. doi: 10.1016/j.jlp.2007.02.002.
Dinkelacker, F., B. Manickam, and S. Muppala. 2011. Modeling and simulation of lean premixed
turbulent methane/hydrogen/air flames with an effective Lewis number approach. Combust.
Flame. 158 (9):1742–49. doi: 10.1016/j.combustflame.2010.12.003.
Efimenko, A. A., and S. B. Dorofeev. 2001. CREBCOM code system for description of gaseous
combustion. J. Loss. Prev. Process. Industries 14 (6):575–81. doi: 10.1016/S0950-4230(01)00049-3.
Emami, S., K. Mazaheri, A. Shamooni, and Y. Mahmoudi. 2015. LES of flame acceleration and DDT
in hydrogen-air mixture using artificially thickened flame approach and detailed chemical kinetics.
Int. J. Hydrogen Energy 40 (23):7395–408. doi: 10.1016/j.ijhydene.2015.03.165.
Ettner, F., K. G. Vollmer, and T. Sattelmayer. 2014. Numerical simulation of the deflagration-to-
detonation transition in inhomogeneous mixtures. J. Combust. 2014:1–15. doi: 10.1155/2014/686347.
Gaathaug, A. V., K. Vaagsaether, and D. Bjerketvedt. 2012. Experimental and numerical investigation
of DDT in hydrogen-air behind a single obstacle. Int. J. Hydrogen Energy 37 (22):17606–15. doi: 10.
1016/j.ijhydene.2012.03.168.
Gamezo, V. N., T. Ogawa, and E. S. Oran. 2007. Numerical simulation of flame propagation and DDT
in obstructed channels filled with hydrogen-air mixture. Proc. Combust. Inst. 31 (2):2463–71. doi:
10.1016/j.proci.2006.07.220.
Gamezo, V. N., T. Ogawa, and E. S. Oran. 2008. Flame acceleration and DDT in channels with
obstacles: Effect of obstacle spacing. Combust. Flame. 155 (1–2):302–15. doi: 10.1016/j.combust
flame.2008.06.004.

```
COMBUSTION SCIENCE AND TECHNOLOGY 29
```

Gamezo, V. N., T. Ogawa, and E. S. Oran. 2009. Deflagration-to-detonation transition in H2-air mixtures:
Effect of blockage ratio. AIAA, 47th Aerospace Sciences Meeting. doi: 10.2514/6.2009-440.
Glassman, I., R. A. Yetter, and N. G. Glumac. 2014. Combustion. 5th ed. Academic Press. doi: 10.
1016/C2011-0-05402-9.
Gülder, Ö. L. 1991. Turbulent premixed flame propagation models for different combustion regimes.
Symp. (Int). Combust. 23 (1):743–50. doi: 10.1016/S0082-0784(06)80325-5.
Hasslberger, J., L. R. Boeck, and T. Sattelmayer. 2015. Numerical simulation of deflagration-to-
detonation transition in large confined volumes. J. Loss. Prev. Process. Industries 36:371–79. doi:
10.1016/j.jlp.2014.11.018.
Heidari, A., and J. X. Wen. 2014. Numerical simulation of flame acceleration and deflagration to
detonation transition in hydrogen-air mixture. Int. J. Hydrogen Energy 39 (36):21317–27. doi: 10.
1016/j.ijhydene.2014.10.066.
Henriksen, M., K. Vaagsaether, J. Lundberg, S. Forseth, and D. Bjerketvedt. 2021. Simulation of
a premixed explosion of gas vented during Li-ion battery failure. Fire. Saf. J. 126:103478. doi: 10.
1016/j.firesaf.2021.103478.
Holt, M., M. B. Nikitin, and R. J. Campbell. 2012. Fukushima nuclear disaster. CRS report, R41694.
https://crsreports.congress.gov/product/pdf/R/R41694.
Hong, S.-W., J. Kim, H.-S. Kang, Y.-S. Na, and J. Song. 2015. Research efforts for the resolution of
hydrogen risk. Nucl. Eng. Technol. 47 (1):33–46. doi: 10.1016/j.net.2014.12.003.
Ivanov, M. F., A. D. Kiverin, I. S. Yakovenko, and M. A. Liberman. 2013. Hydrogen–oxygen flame
acceleration and deflagration-to-detonation transition in three-dimensional rectangular channels
with no-slip walls. Int. J. Hydrogen Energy 38 (36):16427–40. doi: 10.1016/j.ijhydene.2013.08.124.
Jian, L., and N. Jianguo. 2018. Experimental and numerical studies on detonation reflections over
cylindrical convex surfaces. Combust. Flame. 198:130–45. doi: 10.1016/j.combustflame.2018.07.017.
Karanam, A., S. Ganju, and J. Chattopadhyay. 2020. Time scale analysis, numerical simulation and
validation of flame acceleration and DDT in hydrogen air mixtures. Combust. Sci. Technol.
193 (13):2217–40. doi: 10.1080/00102202.2020.1732363.
Karanam, A., P. K. Sharma, and S. Ganju. 2018. Numerical simulation and validation of flame
acceleration and DDT in hydrogen air mixtures. Int. J. Hydrogen Energy 43 (36):17492–504. doi:
10.1016/j.ijhydene.2018.07.108.
Karanam, A., V. Verma, and J. Chattopadhyay. 2024. Numerical validation and benchmarking of
hydrogen flame propagation in vertical acceleration tube experimental facility. Fluid. Mech. Fluid.
Power. Chapter 11 (4). doi: 10.1007/978-981-99-7177-0_11.
Khokhlov, A. M., and E. S. Oran. 1999. Adaptive mesh numerical simulation of deflagration-to-
detonation transition - the dynamics of hot spots. AIAA, 30th Fluid Dynamics Conference. doi: 10.
2514/6.1999-3439.
Khokhlov, A. M., E. S. Oran, and G. O. Thomas. 1999. Numerical simulation of deflagration-to-
detonation transition: The role of shock–flame interactions in turbulent flames. Combust. Flame.
117 (1–2):323–39. doi: 10.1016/S0010-2180(98)00076-5.
Kiverin, A. D., M. F. Ivanov, and M. A. Liberman. 2012. Shock-flame interaction and deflagration-to-
detonation transition in hydrogen/oxygen mixtures. 28th International Symposium on Shock
Waves. doi: 10.07/978-3-642-25688-2_49.
Knudsen, V. 2006. Hydrogen gas explosions in pipelines – modeling and experimental investigations.
PhD thesis, Norway: Telemark University College.
Kudriakov, S., F. Dabbene, E. Studer, A. Beccantini, J. P. Magnaud, H. Paillere, A. Bentaib, A. Bleyer,
J. Malet, E. Porcheron, et al. 2008. The TONUS CFD code for hydrogen risk analysis: Physical
models, numerical schemes and validation matrix. Nucl. Eng. Des. 238 (3):551–65. doi: 10.1016/j.
nucengdes.2007.02.048.
Kuznetsov, M., J. Yanez, J. Grune, A. Friedrich, and T. Jordan. 2015. Hydrogen combustion in a flat
semi-confined layer with respect to the Fukushima Daiichi accident. Nucl. Eng. Des. 286:36–48.
doi: 10.1016/j.nucengdes.2015.01.016.
Law, C. K., G. Jomaas, and J. K. Bechtold. 2005. Cellular instabilities of expanding hydrogen/propane
spherical flames at elevated pressures: Theory and experiment. Proceedings of the Combustion
Institute, vol. 30, 159–67. doi: 10.1016/j.proci.2004.08.266.

30 A. KARANAM AND V. VERMA


Liang, Z., M. Sonnenkalb, A. Bentaib, and M. Sangiorgi. 2014. Status report on hydrogen manage-
ment and related computer codes. Technical report, NEA/CSNI/R(2014)8.
Liberman, M. A., M. F. Ivanov, A. D. Kiverin, M. S. Kuznetsov, A. A. Chukalovsky, and
T. V. Rakhimova. 2010. Deflagration-to-detonation transition in highly reactive combustible
mixtures. Acta. Astronautica. 67 (7–8):688–701. doi: 10.1016/j.actaastro.2010.05.024.
Menter, F. R. 1994. Two-equation eddy-viscosity turbulence models for engineering applications.
Aiaa. J. 32 (8):1598–605. doi: 10.2514/3.12149.
Michel, J.-B., O. Colin, and C. Angelberger. 2010. On the formulation of species reaction rates in the
context of multi-species CFD codes using complex chemistry tabulation techniques. Combust.
Flame. 157 (4):701–14. doi: 10.1016/j.combustflame.2009.12.014.
Óconaire, M., H. J. Curran, J. M. Simmie, W. J. Pitz, and C. K. Westbrook. 2004. A comprehensive
modeling study of hydrogen oxidation. Int. J. Chem. Kinet. 36 (11):603–22. doi: 10.1002/kin.20036.
Oran, E. S. 2015. Understanding explosions – from catastrophic accidents to creation of the universe.
Proc. Combust. Inst. 35 (1):1–35. doi: 10.1016/j.proci.2014.08.019.
Oran, E. S., and J. P. Boris. 2000. Numerical simulation of reactive flow. Cambridge University Press.
doi: 10.1017/CBO9780511574474.
Oran, E. S., and V. N. Gamezo. 2007. Origins of the deflagration-to-detonation transition in gas-phase
combustion. Combust. Flame. 148 (1–2):4–47. doi: 10.1016/j.combustflame.2006.07.010.
Park, C. O. 2011. Mitigation of hydrogen hazards in severe accidents in nuclear power plants.
Technical report, IAEA-TECDOC-1661.
Peters, N. 2000. Turbulent combustion. Cambridge University Press. doi: 10.1017/
CBO9780511612701.
Polifke, W., P. Flohr, and M. Brandt. 2002. Modeling of inhomogeneously premixed combustion with
an extended TFC model. J. Eng. Gas. Turbines Power 124 (1):58–65. doi: 10.1115/1.1394964.
Povilaitis, M., and J. Jaseliunaite. 2021. Simulation of hydrogen-air-diluents mixture combustion in
an acceleration tube with FlameFoam solver. Energies 14 (17):5504. doi: 10.3390/en14175504.
Saffers, J.-B., and V. V. Molkov. 2014. Hydrogen safety engineering framework and elementary design
safety tools. Int. J. Hydrogen Energy 39 (11):6268–85. doi: 10.1016/j.ijhydene.2013.06.060.
Sathiah, P., E. Komen, and D. Roekaerts. 2012. The role of CFD combustion modeling in hydrogen
safety management – part I: Validation based on small scale experiments. Nucl. Eng. Des.
248:93–107. doi: 10.1016/j.nucengdes.2012.03.047.
Shepherd, J. E., and J. H. S. Lee. 1992. On the transition from deflagration to detonation. In Major
research topics in combustion, 439–87. New York: Springer. doi: 10.1007/978-1-4612-2884-4_22.
Spalding, D. B. 1971. Mixing and chemical reaction in steady confined turbulent flames. Symp. (Int).
Combust. 13 (1):649–57. doi:10.1016/S0082-0784(71)80067-X.
Vaagsaether, K., V. Knudsen, and D. Bjerketvedt. 2007. Simulation of flame acceleration and DDT in
H 2 H 2 -air mixture with a flux limiter centered method. Int. J. Hydrogen Energy 32 (13):2186–91.
doi: 10.1016/j.ijhydene.2007.04.006.
Veynante, D., and L. Vervisch. 2002. Turbulent combustion modeling. Prog. Energy. Combust. Sci.
28 (3):193–266. doi: 10.1016/S0360-1285(01)00017-X.
Wang, C. J., and J. X. Wen. 2017. Numerical simulation of flame acceleration and deflagration-to-
detonation transition in hydrogen-air mixtures with concentration gradients. Int. J. Hydrogen
Energy 42 (11):7657–63. doi: 10.1016/j.ijhydene.2016.06.107.
Weller, H. G. 1993. The development of a new flame area combustion model using conditional
averaging. Thermo-fluids section report, TF/9307. Imperial College.
Weller, H. G., G. Tabor, H. Jasak, and C. Fureby. 1998. A tensorial approach to computational
continuum mechanics using object-oriented techniques. Comput. Phys. 12 (6):620–31. doi: 10.
1063/1.168744.
Xiao, J., W. Breitung, M. Kuznetsov, H. Zhang, J. R. Travis, R. Redlinger, and T. Jordan. 2017.
GASFLOW-MPI: A new 3-D parallel all-speed CFD code for turbulent dispersion and combustion

```
COMBUSTION SCIENCE AND TECHNOLOGY 31
```

simulations: Part I: Models, verification and validation. Int. J. Hydrogen Energy 42 (12):8346–68.
doi: 10.1016/j.ijhydene.2017.01.215.
Yang, Z., and B. Zhang. 2023. Numerical and experimental analysis of detonation induced by shock
wave focusing. Combust. Flame. 251:112691. doi: 10.1016/j.combustflame.2023.112691.
Zhang, B., Y. Li, and H. Liu. 2022. Analysis of the ignition induced by shock wave focusing equipped
with conical and hemispherical reflectors. Combust. Flame. 236:111763. doi: 10.1016/j.combust
flame.2021.111763.
Zimont, V. L. 2000. Gas premixed combustion at high turbulence: Turbulent flame closure combus-
tion model. Exp. Therm. Fluid. Sci. 21 (1–3):179–86. doi: 10.1016/S0894-1777(99)00069-2.

32 A. KARANAM AND V. VERMA


