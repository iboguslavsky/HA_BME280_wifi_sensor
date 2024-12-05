### Battery Capacity Equation

The total battery capacity $C_\text{battery}$ can be calculated as:

$$ C_\text{battery} = C_\text{self\ discharge} + C_\text{board quiescent current} + C_\text{measurements} $$

Where:
- $C_\text{self\ discharge}$: Capacity consumed due to self-discharge.
- $C_\text{board quiescent\ current}$: Capacity consumed by the quiescent current of the circuit.
- $C_\text{measurements}$: Capacity consumed during measurements or operations.

Lets calculate reamingin battery capacity after accounting for self-discharge and idle board current:

## Calculate available battery capacity and longevity

#### Converting Milliampere-Hour (mAh) to Coulombs (C)

The conversion from milliampere-hour (\( \text{mAh} \)) to coulombs (\( \text{C} \)) is given by:

$$
Q (\text{C}) = I (\text{mAh}) \times 3.6
$$

Where:
- \( Q \): Charge in coulombs (C)
- \( I \): Current capacity in milliampere-hours (mAh)
- \( 3.6 \): Conversion factor (1 mAh = 3.6 C)
- 
For Energizer Ultimate [L91 ](https://data.energizer.com/pdfs/l91.pdf):

$C_\text{battery} = 3,000 mAh * 3.6 = 10,800 Coulumbs$
