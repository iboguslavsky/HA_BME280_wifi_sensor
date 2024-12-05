## Low power temperature / humidity / atmospheric pressure sensor for Home Assistant

![schematic](https://github.com/iboguslavsky/HA_BME280_wifi_sensor/blob/main/img/schematic_1024x800.png)
| ![front](https://github.com/iboguslavsky/HA_BME280_wifi_sensor/blob/main/img/front_640x480.jpg) | | ![back](https://github.com/iboguslavsky/HA_BME280_wifi_sensor/blob/main/img/back_640x480.jpg) |

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

Charge used by the board in deep sleep in 1 year:
$Q_\text{board quiescent\ charge} = 0.006mA * 3.6 * 24h * 365days = 378\ Coulombs$

The L91 AA lithium battery boasts a shelf life of 15 to 25 years at 21°C (70°F), indicating a self-discharge rate of less than 1% per year. Calculating loss of charge due to self-discharge for a 2-year cycle:

$Q_\text{self\ discharge} = 10,800\ Coulombs * 0.02 = 216\ Coulombs$

The remaining useful capacity of the battery after 2 years:

$Q_\text{useful capacity} = 10,800 - 2 * 378 - 216 = 9,828\ Coulombs$

Considering that a single measurement requires 250mC of energy (worst case): 
$N_\text{measurements} = 9,828 / 0.250 = \~\~ 39,000\ measurements$

Considering 30 mins sleep between measurements:
$N_\text{days} = 
  39,000\ measurements / (2\ measurements\ per\ hour * 24 hours) = 
  812\ days\ or\ 2.2\ years$
