# ArduinoIDE_ESP8266_Customizations
Customizations I've made on ESP8266 library for Arduino IDE that I've used on a personal project

Those customizations were made to:

1 - I have a design for ESP-01 that I want to use as much as 450KB of firmware and be able to update the firmware either remotely or locally, and still be able to get a 196/256KB SPIFFs partition, that partition holds the SSL certificates. So, there is a trade off, you can have SPIFFs and still force an update that its size*2 + spiffs size exceeds flash size but size*2 doesn't exceed flash size, and still be a safe update that if it fails, main firmware is still intact, but on the other hand spiffs will be ruined and MUST be updated right after firmware is updated.
2 - That design follows MSX TCP-IP UNAPI specification, which requires the possibility of opening a TCP/IP connection and not only assign the remote port but also the local port, so I've added this possibility.
3 - That design also needs, for TLS/SSL connections, to be able to connect and authenticate with a given hostname, or, alternatively, do not authenticate hostname, so BearSSL methods for both cases were added.
4 - It will build the firmware with PUYA flash chip support. Those are the most used flash memory chips on ESP-01 modules and need the flash to work reliably with the firmware, as the firmware uses it for SPIFFs / Certificate reading and need to write to the flash when creating its certificate index.

I've tried to make those changes in a way that it doesn't break the default behavior and current applications written for ESP8266 Arduino IDE Library do not need to change anything as long as they do not want to use the new features.

Observing the library LGPL v2.1, I'm releasing the library changes to the public.
