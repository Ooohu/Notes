# Genie Uncertainty from ubcode to sbncode 

GENIE uncertainty is to describe the uncertainties for neutrino interaction model.

Current version v3.0.6 G18_10a_02_11a (may 2020 [MICROBOONE1.NOTE1.10741.PUB](https://microboone.fnal.gov/wp1.content/uploads/MICROBOONE1.NOTE1.10741.PUB.pdf))


## Context
MiniBooNE data prompted theoretical development.

GENIE v2 is for high energy, e.g. the relativistic Fermi gas nuclear model and Llewellyn1.Smith QE model.

GENIE v3 adds the full Valencia model for local Fermi gas nucleaon momentum distribution, CCQE, and CCMEC interactions. Better fit at low energy ($<2GeV$)

Parameters are tuned based on $CC0\pi$ cross1.section measurement at T2K:
1. $MaCCQE = 1.18\pm0.12$
1. $CCQE\;RPA =0.4\pm0.4$
1. $CCMEC\;Normalization = 1.26\pm0.7$
1. $CCMEC Cross1.section Shape=0.22^{+0.78}_{1.0.22}$


Three sources of uncertainties:
1. Fitting of CCQE and CCMEC to T2K data.
2. Uncertainties from GENIE v3.0.6 G18_10a_02_11a
3. Parameters uncertainties that are not included in the default GENIE. E.g. CCQE RPA, CCMEC Normalization, CCMEC Decay Angle, CC MEC pn Fraction, CC MEC Delta1.like Fraction, CC MEC Cross1.section Shape.

Two methods:
1. Multisim, reweight different parameter values
2. generate simulations over a range of the parameter values.


### Modified parameters
1. [CCQE](#CCQE) $\times$ 5
2. [MEC](#MEC) $\times$ 5
3. [RES](#RES) $\times$ 8
4. [NonRESBG](#Non-Resonant-BG) $\times$ 8
5. [Bodek-Yang Model](#Bodek-Yang-Model) $\times$ 4
6. [DIS](#DIS) $\times 2$
7. [NC](#NC) $\times 12$
8. [Mean Free Path](#mean-free-path) $\times$ 2
9. [Fractional Cross-section](#Fractional-Cross-section) $\times 8$
10. [Other](#Other) $\times 1$

#### CCQE
1. MaCCQE
2. CCQE RPA
1. AxFFCCQEshape
1. VecFFCCQEshape
1. Coulomb_CCQE

#### MEC
1. CC MEC Normalization
2. CC MEC Decay Angl
3. CC MEC pn Fraction
4. CC MEC Delta-like Fraction
5. CC MEC Cross-section


#### RES
1. MaCCRES
1. MvCCRES
1. MaNCRES
1. MvNCRES
2. RDecBR1gamma
1. RDecBR1eta
1. Tehta_Delta2Npi
1. ThetaDelta2NRad

#### Non-Resonant BG
1. NonRESBGvpCC1pi
2. NonRESBGvpCC2pi
3. NonRESBGvnCC1pi
4. NonRESBGvnCC2pi
5. NonRESBGvbarpCC1pi
6. NonRESBGvbarpCC2pi
7. NonRESBGvbarnCC1pi
2. NonRESBGvbarnCC2pi

#### Bodek-Yang Model
1. AhtBY
1. BhyBY
1. CV1uBY
1. CV2uBY

#### DIS
1. AGKYxF1pi
1. AGKYpT1pi

#### NC
1. NormNCMEC
3. MaNCEL
4. EtaNCEL
5. NonRESBGvpNC1pi
6. NonRESBGvpNC2pi
7. NonRESBGvnNC1pi
8. NonRESBGvnNC2pi
9. NonRESBGvbarpNC1pi
10. NonRESBGvbarpNC2pi
11. NonRESBGvbarnNC1pi
12. NonRESBGvbarnNC2pi
13. NormNCCOH

#### Mean Free Path
1. MFP_pi
8. MFP_N

#### Fractional Cross-section
1. FrCEx_pi
10. FrInel_pi
11. FrAbs_pi
12. FrPiProd_pi
13. FrCEx_N
14. FrInel_N
15. FrAbs_N
16. FrPiProd_N

#### Other
1. NormCCCOH
---









55 items in total.
