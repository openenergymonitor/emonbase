# New: emonBase with RFM69 SPI (Direct)

## Overview

![emonBase_rfm69_spi.jpg](img/emonBase_rfm69_spi.jpg)


## EmonHub Interfacer

Radio packets received by the RFM69 SPI board are read using what is called an `Interfacer` in a piece of software called `emonHub` that runs on the RaspberryPi. The interfacer is called `EmonHubRFM69LPLInterfacer` and makes use of [our modifed version](https://github.com/openenergymonitor/rpi-rfm69) of the [jgillula/rpi-rfm69 library](https://github.com/jgillula/rpi-rfm69).

This library is installed as standard on the latest emonSD image, it will also install automatically if an older emonSD image is upgraded.

If you are adding an RFM69 SPI board to an existing install you will need to add the following interfacer configuration entry in the interfacers section of emonhub.conf to enable reading from this board:

```
[interfacers]
    [[SPI]]
        Type = EmonHubRFM69LPLInterfacer
        [[[init_settings]]]
            nodeid = 5
            networkID = 210
        [[[runtimesettings]]]
            pubchannels = ToEmonCMS,
```

## Radio encryption key

The encryption key for the RFM69 is currently hard coded in the EmonHubRFM69LPLInterfacer. This will be broken out as an emonhub.conf configuration option soon. If you would like to change the encryption key to make it secure, this can be done by modifying the  `encryptionKey` setting on line 51 of the EmonHubRFM69LPLInterfacer itself: [https://github.com/openenergymonitor/emonhub/blob/master/src/interfacers/EmonHubRFM69LPLInterfacer.py#L51](https://github.com/openenergymonitor/emonhub/blob/master/src/interfacers/EmonHubRFM69LPLInterfacer.py#L51).
