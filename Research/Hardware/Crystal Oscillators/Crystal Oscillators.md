gm### Art of Electronics 5.19 (p.300)
- Much higher precision than RC or LC oscillator circuits.
- External crystal is the best choice in for accurate MCU timing.
- Can be modelled to an RLC circuit tuned to some frequency.
- High Q (typically around 10000)
- Pierce Oscillator is typical for MCU timing applications.
- Complete crystal oscillator modules come in IC-sized packages for a range of typical frequencies and some specialist frequencies.
- Digital wristwatches use 32.768KHz oscillators (2^15)
- Crystal Oscillators can be adjusted slightly by varying a series or parallel capacitor.
- VCXOs use varactor to pull the frequency of the oscillator.
- Temperature Controlled Crystal Oscillators (TCXOs) can provide improved stability over a larger temperature range.
- Aside from temperature, aging is the next biggest factor in crystal oscillator drift and error.

### ST AN2806 Guidelines for oscillator design on STM32s

Harmonic Oscillators can be divided into two subfamilies:
- Negative-resistance oscillators
- Positive-feedback oscillators
Positive feedback oscillators are characterised by the Barkhausen model, where an oscillator must fulfil the Barkhausen criterion to maintain a stable oscillation at a desired frequency.
STM32s feature HSE and LSE oscillators designed according to the negative resistance principle.

Transresistance is defined as the ration of a given voltage variation ∆V and induced current variation ∆I. Transresistance can be positive or negative. Transconductance is the inverse of transresistance.

An oscillation loop is made of two branches:
- The active branch composed of the oscillator itself provides the energy required to make the oscillation start and build up until its stable phase has been reached. Once stable, the active branch provides the energy required to compensate for loses in the passive branch.
- The passive branch is composed of the resonator, two load capacitors and all the parasitic capacitances.
![[crystal_resonator_block_diagram.png]]
To ensure successful oscillation start and to maintain stable oscillation, the ratio between negative resistance of the loop and the crystal maximal equivalent series resistance (ESR) is specified for STM32 products. It is recommended to have a ratio higher than 5 for HSE and 3 for LSE.

Pierce oscillators require low counts of external componentry.
![[pierce_oscillator_circuit.png]]
Cs is the stray capacitance of OSC_IN, OSC_OUT pins and PCB trace
Rf feedback resistor is tuned to bias the inverter amplifier at Vout=Vin and force it to operate in a linear region