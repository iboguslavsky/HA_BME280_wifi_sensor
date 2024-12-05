### Battery Capacity 

The total battery capacity $Q_\text{battery}$ can be calculated as:

$$ Q_\text{battery} = Q_\text{self\ discharge} + Q_\text{board quiescent charge} + Q_\text{useful capacity} $$

Where:
- $Q_\text{self\ discharge}$: Capacity consumed due to self-discharge
- $Q_\text{board quiescent\ charge}$: Capacity consumed by the quiescent current of the circuit
- $Q_\text{useful capacity}$: Capacity consumed during measurements


### Calculate available battery capacity and longevity

To convert mAh to Coulombs:

$Q (\text{C}) = I (\text{mAh}) \times 3.6$

Where:
- $\(Q\)$: Charge in coulombs (C)
- $\(I\)$: Current capacity in milliampere-hours (mAh)
  
For Energizer Ultimate [Energizer L91 AA lithium battery](https://data.energizer.com/pdfs/l91.pdf):

$Q_\text{battery} = 3,000 mAh * 3.6 = 10,800\ Coulombs$

Charge used by the board in deep sleep over 2 year span:
$Q_\text{board quiescent\ charge} = 0.006mA * 3.6 * 24 * 365 = 378\ Coulombs$

The L91 AA lithium battery boasts a shelf life of 15 to 25 years at 21°C (70°F), indicating a self-discharge rate of less than 1% per year. Calculating loss of charge due to self-discharge for a 2-year cycle:

$Q_\text{self\ discharge} = 10,800\ Coulombs * 0.02 = 216\ Coulombs$

The remaining useful capacity of the battery:

$Q_\text{useful capacity} = 10,800 - 378 - 216 = ~10,200\ Coulombs$

Considering that a single measurement requires 250mC of energy (worst case): 
$N_\text{measurements} = 10,200 / 0.250 = 40,800\ measurements$

Considering 30 mins sleep between measurements:
$N_\text{days} = 40,800\ measurements / (2\ measurements\ per\ hour * 24 hours) = 850\ days\ or\ 2.3\ years$
