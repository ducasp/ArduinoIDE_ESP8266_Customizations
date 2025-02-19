Those are the customized ESP8266 Arduino IDE files for version 3.1.2

I've created those additions to suit the needs for my ESP8266 customized firmware for MSX Interfaces using UNAPI

Those library additions are like the original Arduino IDE ESP8266 library, following the LGPL and having its source code released

There is no need to release the ESP8266 custom firmware for MSX Interfaces using UNAPI as LGPL mandates to release only the library changes, not the code/executable that uses the library

Changes made by Oduvaldo Pavan Junior, ducasp@gmail.com , 2019-2025

Users
 |USERNAME
	|AppData
		|Local
			|Arduino15
				|packages
					|esp8266
						|hardware
							|esp8266
								|2.7.1
									+platform.local.txt
									|cores
										|esp8266
											+Esp.cpp
											+Esp.h
											+Updater.cpp
											+Updater.h
									|libraries
										|ESP8266httpUpdate
											|src
												+ESP8266httpUpdate.cpp
												+ESP8266httpUpdate.h
										|ESP8266WiFi
											|src
												+CertStoreBearSSL.cpp
												+CertStoreBearSSL.h
												+WiFiClient.cpp
												+WiFiClient.h
												+WiFiClientSecureBearSSL.cpp
												+WiFiClientSecureBearSSL.h

Those are the changes:

platform.local.txt -> This will force PUYA support that makes flash operations slower but works on PUYA flash memory, which are the majority of chips used on ESP-01 modules
Esp.cpp / Esp.h -> getFreeSketchSpace can be told that SPIFF allocated space can be overwritten by code, this allows up ~450KB of code updates at the expense of always having to flash SPIFFs after a firmware update, which is a good trade-off for some situations
Updater.cpp / Updater.h -> begin can be told that SPIFF allocated space can be overwritten by code, this allows up ~450KB of code updates at the expense of always having to flash SPIFFs after a firmware update, which is a good trade-off for some situations
ESP8266httpUpdate.cpp / ESP8266httpUpdate.h -> add the updateSpiffs(WiFiClient& client, const String& host, uint16_t port, const String& uri = "/", const String& currentVersion = "") method to allow OTA update of SPIFFs on a given port/WifiClient connection class
CertStoreBearSSL.cpp / CertStoreBearSSL.h -> initCertStore can be told to force the creation of a New Index
WiFiClient.cpp / WiFiClient.h -> add the method connect(IPAddress ip, uint16_t port, uint16_t localPort) so you can define the local port of a connection to a remote port
WiFiClientSecureBearSSL.cpp / WiFiClientSecureBearSSL.h -> add the methods mentioned below to have different possibilities of opening SSL Connections:
    connect(IPAddress ip, uint16_t port, uint16_t localPort) override - Will open SSL connection ignoring hostname authentication
    connect(IPAddress ip, uint16_t port, const char* name) - Will open SSL connection trying to autenticate hostname (name)
    connect(IPAddress ip, uint16_t port, uint16_t localPort, const char* name) - Will open SSL connection trying to autenticate hostname (name) and force local port to localPort