# HRS3300 Heart Rate Sensor

## Overview

A sensor application that demonstrates how to poll data from the hrs3300 heart
rate sensor.

## Building and Running

This project configures the hrs3300 sensor on the pinetime_devkit0 board to
enable the green LED and measure the reflected light with a photodiode. The raw
ADC data prints to the console. Further processing (not included in this
sample) is required to extract a heart rate signal from the light measurement.

### Sample Output

```
GREEN=5731
GREEN=5750
GREEN=5748
GREEN=5741
GREEN=5735
GREEN=5737
GREEN=5736
GREEN=5748
```

<repeats endlessly>
