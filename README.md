# Fuzzy Logic Based Shunt Active Power Filter

> A Fuzzy powered DC link Capacitor voltage regulating algorithm

## About Project

This Project tries to successfully replicate the process used in a [Scholarly Article](https://www.researchgate.net/publication/229017965_Shunt_Active_Filter_Controlled_by_Fuzzy_Logic). The Shunt Active Power Filter uses Fuzzy logic to determine the output current (from shunt) which helps reduce filter the harmonics in a system.

## Introduction

### _What is Harmonics in Electrical System?_

In power systems, a harmonic is a voltage or current occurs at a multiple of the fundamental frequency. They are integral multiples of a fundamental frequency. It is often regarded as noise in the power line.

![harmnoics](https://circuitdigest.com/sites/default/files/inlineimages/u1/Harmonics-in-Electrical.png)

In the above image notice how current is distorted due to voltage harmonics? Well, we are trying to remove exactly this.

### _Why it is necessary to eliminate Harmonics in the Power System?_

It is well known that Current and the voltage harmonics are directly proportional to the noisy power transfer to the Load. Various household equipments are responsible for the harmonics in the power system. The power system harmonics often manifolds the load current. Equipments like lights, LEDs, Television face the adverse consequence if power system harmonics is allowed to exist.

To overcome this power system harmonics, one need to reconstruct the power connection to introduce harmonics filters in the power system.

### _Why Active Filter?_

Active harmonic filters use a neat method where the filter injects compensating harmonics into the system nullifying the effect. The development in this field has become pretty advanced. The following are some of the widely used active filtering methods:

- PWM method

- Voltage source inverting method

- Sampling and Control strategy

- **Fuzzy Based Shunt Active filter strategy** (most recent and most effective)

## Plan Of Attack

### Understand the Role of Fuzzy in SAPF

- _Used as DC-Link Capacitor Voltage Algorithm_

- _Capacitor Voltage, `Vc` is taken as `14v`, ( [refer ijsert page6](http://www.ijesrt.com/issues%20pdf%20file/Archive-2018/June-2018/64.pdf) )_

- _A voltage is measured after the shunt and before Fuzzy, `Vm`_

- _Resistor of `0.1 Ohm` is taken due to impedence_

### Crafting Fuzzy Sets

**_Input Set_**

There are two sets: _Set1, Set2_

*Set1* : Set of errors (`E`) are collected between `Vc` and `Vm` at a specific point of time `t`, given by:

```bash
                                   E = Vc - Vm
```

*Set2* : Set of errors described by (`dE`):

```bash
                                dE = E(t) - E(t-1)
                                
                                        or
                                        
                                dE = E - d(E)/dt

```

**_Output Set_**

The output set is a crisp value (percentage) of the current produced with effective magnitude: `Ic`. The range of `Ic` can be easily calculated from `Vc` assuming the shunt has a resistance of `0.1 Ohm` (caused by impedance).

Since the `E` range is from 7 to 14, `Vc` is 14V, `Ic` can be calculated by:

```bash
                                Ic = x ∈ {(Vc-Vm) / R}
```

**_Fuzzy Set Ranges_**

_E Range_:

The experimentally permitted range is : `E = {7 to 14}`

_dE Range_:

The expereimentally feasible range is : `dE = {-0.4 to 0.5}`

_Ic Range_:

The range acquired by calculation from above : `Ic = {0 to 70}`

> All ranges are being refered from [ijsert-page3](http://www.ijesrt.com/issues%20pdf%20file/Archive-2018/June-2018/64.pdf)

### Chosing Fuzzy Inference System

Using _SKFuzzy `control.ControlSystem`_ which defaults to _Mamdani Inference System_ with defuzzification using _centroid_

### Coding

- _Defining universe_
- _Initializing Antecedents, Consequents fuzzy variables_
- _Populate the universe with membership functions_
- _Rule Writing_
- _Control System + Simulation_

## Experimental Results

Successfully performed fuzzification and defuzzification using `SkFuzzy` module.

Below are the observations from the experiment conducted:

- _Membership Graph for `Input Set E`_

![e membership](https://i.imgur.com/hFVcOVX.png)

- _Membership Graph for `Input Set dE`_

![de membership](https://i.imgur.com/qTPCn1A.png)

- _Membership Graph for `Output Set Ic`_

![Ic membership](https://i.imgur.com/QiMTrFC.png)

- _Final Output for `E = 12, dE = -0.1` came out to be 45.99Amps_

![Output](https://i.imgur.com/nkVoFFT.png)

## Resources

- Moscow Scientific Reviews

- Ijesrt Scholarly Article

- MDPI-RES Electronics

## Contributors

<a href="https://github.com/P0intMaN/FUZZY-BASED-SAPF/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=P0intMaN/FUZZY-BASED-SAPF" />
</a>

###### Pratheek & Sourav

