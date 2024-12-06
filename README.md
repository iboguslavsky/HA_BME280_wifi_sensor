## Summary

This project outlines the hardware and firmware needed to create a low-power environmental (ambient temperature / relative humidity / barometric pressure) Home Assitant-integrated WiFi sensor with a lifespan of over 2 years. The system features an ESP32-C3-based board, which remains in deep sleep mode most of the time and wakes up every 30 minutes to send environmental data to Home Assistant. It uses the low-power [BME280](https://www.bosch-sensortec.com/products/environmental-sensors/humidity-sensors-bme280/) environmental sensor.

The board is powered by a pair of 1.5V AA LiFePO lithium batteries (non-rechargeable). The decision to use these batteries was based on:

- Their ability to discharge almost to capacity while maintainng a steady voltage (unlike alcaline batteries). This eliminates the need for voltage regulation
- This allows for both saving on components count - and the additional power draw
- Batteries very low self-discharge current (ie, shelf life of > 10 years)

The board is using standard [ESPHome](https://esphome.io/) firmware. 

### Hardware

![schematic](https://github.com/iboguslavsky/HA_BME280_wifi_sensor/blob/main/img/schematic_1024x800.png)

<p align="center">
  <img src="https://github.com/iboguslavsky/HA_BME280_wifi_sensor/blob/main/img/front_640x480.jpg" width="320">&nbsp;&nbsp;
  <img src="https://github.com/iboguslavsky/HA_BME280_wifi_sensor/blob/main/img/back_640x480.jpg" width="320">
</p>


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

#### Quiescent Charge
The board consumes < $6\text{uA}$ current while in deep sleep:
![idle](https://github.com/iboguslavsky/HA_BME280_wifi_sensor/blob/main/img/deep_sleep.png)

Charge used by the board in deep sleep in 1 year:
$Q_\text{board quiescent\ charge} = 0.006mA * 3.6 * 24h * 365days = 378\ Coulombs$

#### Self discharge
The L91 AA lithium battery boasts a shelf life of 15 to 25 years at 21°C (70°F), indicating a self-discharge rate of less than 1% per year. Calculating loss of charge due to self-discharge for a 2-year cycle:

$Q_\text{self\ discharge} = 10,800\ Coulombs * 0.02 = 216\ Coulombs$

The remaining useful capacity of the battery after 2 years:

$Q_\text{useful capacity} = 10,800 - 2 * 378 - 216 = 9,828\ Coulombs$

#### Battery lifespan
Single environmental measurement and subsequent communication with HA consumes between 200mC and 250mC of charge:
![measure](https://github.com/iboguslavsky/HA_BME280_wifi_sensor/blob/main/img/measurement.png)

Assuming worst case, the total number of possible measurements is: 

$N_\text{measurements} = 9,828 / 0.250 = \~\~ 39,000\ measurements$

Considering 30 mins sleep between measurements, the sensor lifespan on a single set of fresh batteries would be:

$N_\text{days} = 
  39,000\ measurements / (2\ measurements\ per\ hour * 24 hours) = $
  812 days or **2.2 years**
