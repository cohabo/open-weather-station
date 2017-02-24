# Open Weather Station

## THE IDEA
To construct a fully open source, open hardware weather station, which publishes it's data in realtime via an open data API on the web.

The main interest in this project is to deal with the full data-processing steps from a sensor and it's hardware over the data transmission towards a server to the final data presentation on the web - everything the open way. This will bring together some re-occuring challenges of hardware and software engineering, like power supply (limations, efficency), sensors (resolution, calibration), housing (maintainance, materials), data transmission (protocolls, checks) and web-presentation (API, visualization, maintainance).

In this repository, the full documentation and the process towards the construction will be organized and documented.


## TIMELINE
The project is planned for the spring and summer of 2017 to happen - from research and planning to the construction of it. 

| Time     | Activity       |
|---------------|--------------|
| March - Mai | Research |
| June - July | Planing and Sourcing |
| July - September | Construction |

## RESEARCH
- Open Hardware Guidelines and Rules
- Best Hardware for the job
- Check professional solutions
	- http://www.funkwetterstationen-test.com/
	- [Netatmo](https://www.netatmo.com/product/weather/weatherstation)
		- [Additional Module](https://www.netatmo.com/product/weather/weatherstation/accessories#module)
		- [Mount](https://shop.netatmo.com/eur_en/netatmo-mount-for-wind-gauge-rain-gauge.html)
		- [Wind Gauge](https://shop.netatmo.com/eur_en/netatmo-wind-gauge.html)
		- [Rain Gauge](https://shop.netatmo.com/eur_en/netatmo-rain-gauge.html)
	- [Davis Vantage Pro II](http://www.davis-wetterstationen.de/6163eu-davis-vantage-pro-2-6163-eu-wireless-aktiv-plus-fars-profi-funk-wetterstation-p-112.html)
	[Open Source wireless weather station](http://www.pittnerovi.com/jiri/hobby/electronics/meteo/)
	- [Wired Test](https://www.wired.com/2015/03/put-4-home-weather-stations-test/)
	- [How I Made a Fully-Functional Arduino Weather Station](https://www.toptal.com/c/how-i-made-a-fully-functional-arduino-weather-station-for-300)
	- [Open Source WiFi Weather Station System](https://wiki.microduino.cc/index.php/Open_Source_WiFi_Weather_Station_System)
	- [OpenWeatherMap weather station prototype](http://openweathermap.org/owmstation)	
	- [How to make a weather station with arduino](http://www.open-electronics.org/how-to-make-a-weather-station-with-arduino/)
	- [Raspberry Pi Weather Station](https://www.raspberryweather.com/)
	- [Open Source Weather Station Development](http://www.wetter-garching.de/howto.html)
	- [Tinkerforge: Starter Kit Weather Station](https://www.tinkerforge.com/en/doc/Kits/WeatherStation/WeatherStation.html)

## PLANING

The minimum requirement is: a small case with a temperature and relative humidity sensor in it, which transfers data onto a server in the web to offer the measurements via an Open Data API.

**General Requirements:**
- as cheap as possible
- easy to copy
- fully open source
- fully open hardware: documented, open hardware parts
- easy to maintain
- easy to repair
- good quality of measurements
- durable: physical and chemical effects (strong wind, hail, strong rain, uv, sand)

**General Questions:**
- what copyright license applies to: source code, raw data and documentation

### Housing
Housing for the weather station. 

**Requirements:**
- Protect the hardware from outer damage
- Safeguard correct measurements of the sensors inside
- durable
- stable and easy mounting

**Questions:**
- Maybe there is already a plan on the web to create one in a 3D printer or by wood.
- which material is best for this: wood, plastic, steel, 
- What are the general requirements for an official weather station?

**Research**
- [Standort-Aufstellungen](http://www.funkwetterstationen-test.com/index.php/category/standort-aufstellung/)

### Sensors

**Sensor Requirements:**
- Specification
- Calibration: cheap, Certificate
- low power usage
- high resolution
- low measuring error

**Sensor Questions:**
- What is the best temporal resolution for the measurement?
- What sensor must be in the weather station, and which one should be optional as extensions later on?
- How will the timestamp be created?

#### 1. Temperatur and relative Humidity

**Requirements:**
- measure temperature
- measure relative humidity

**Questions:**

#### 2. Insolation

**Requirements:**
- measure insolation energy per squaremeter

**Questions:**

#### 3. Windspeed (Anemometer)

**Requirements:**

**Questions:**
- is there a combined device with wind-direction and wind-speed?

#### 4. Winddirection (Anemoskop)

**Requirements:**

**Questions:**

#### 5. Dust

**Requirements:**

**Questions:**

#### 6. Air Pressure

**Requirements:**

**Questions:**

#### Optional
- Groundtemperature
- Soiltemperature
- CO2
- Sonometer (loudness)
- precipitation: when and how much
	- https://shop.netatmo.com/eur_en/netatmo-rain-gauge.html

### Hardware

Arduino or Raspberry Pi or something else i guess. Power supply is a central question: how much power is needed? How often should the data be pushed on the server?

The data must be stored on the computer locally, so that a data transfer loss does not lead to a data loss. 

**Requirements:**
- new sensors should be easy to attach
- protect electrical boards from outer influences
- report errors to user
- monitoring functions for sensors and other weather station parameters.

**Questions:**
- Arduino or Raspy?
- Which data should be stored how on the server?
- how and when should the collected data be deleted?
- Is a on/off button needed for the general power supply?

#### Software
[WeeWX](http://www.weewx.com/): Open Source Software for Weather Stations

### Data Transmission Station 2 Server
How should the data be transfered from the weather station to the server? Via httprest PUT method? 

**Requirements:**
- no data loss
- save power
- as fast as possible and reasonable. realtime prefered. 

**Questions:**
- should only changes be transmitted?

## Server
Small server to host the data and the webservice. 

**Requirements:**
- postgreSQL
- Python3
- Flask
- handle endless numbers of weather stations

**Questions:**

### Webservice
#### API
Open data API of the measurements. 

**Requirements:**
- metadata of sensors
	- resolution
	- limits
- calibration certificates
- sensor data: 
	- value
	- timestamp
	- timestamp data arrived at server
	- timestamp measurement
	- result measurement
- Open: Publlic Domain

**Questions:**
- Which software to use for it? Flask?
- How to deliver documents via the API?

#### Monitoring
Monitor and control the weather station at a web-frontend.

**Requirements:**
- only accessible for logged-in user
- user registration
- responsive
- monitor:
	- data logging: last measures, is it working correctly?, each sensor seperatly, 
	- power supply: actual status, time to work, line-chart
	- data transmission: last transmission, is it working correctly?, line-chart
	- values: outliers, unreasonable results, 
	- error log
	- alerts: send sms when critical problems occure

- control:
	- reset computer
	- change measuring intervalls
	- activate/deactivate sensors
	- alarm: set limits for measurements and other parameters

**Questions:**
- is there a working solution for this?

#### Visualization
Visualize the measurements for everyone accessible on a web-frontend. Use the API for data access.

**Requirements:**
- measures (line chart): default timeintervall, change timeintervall, 
- change of results (line chart): default timeintervall, change timeintervall, 
- download plots as PNG, SVG and CSV.
- distribution of measures: default timeintervall, change timeintervall, 
- average values: default timeintervall, change timeintervall, 
- responsive

**Questions:**
- Pandas and matplotlib oder D3?

#### Alexa 
Connect Amazon Alexa to the data/api.

### Solarpanel

**Requirements:**
- supply the weather station with power
- store power for night and bad weather

**Questions:**
- how much power is needed for the sensors and the hardware? This depends a lot on the sensors used and how often they measure, next to the operation and sending of the computer.

### Camera

Create pictures each day at certain timespots over a full year for automated image analysis.

**Requirements:**
- low power needed
- small housing

**Questions:**
- What resolution is enough?
- How to keep the lens clean?
- How to do the power supply?

## SOURCING
- Conrad
- Amazon

### Parts List


## CONSTRUCTION

## CONTRIBUTE
In the spirit of free software, everyone is invited to contribute to improve this project.

**All Open Weather Station updates, bugs, and feature additions are organized via GitHub's public [issue tracker](https://github.com/skasberger/open-weather-station/issues) in this repository.** 

If you do not already have a GitHub account, you can [sign up for GitHub here](https://github.com/). In the spirit of open source software, everyone is encouraged to help improve this project. Here are some ways you can contribute:
- by reporting bugs
- by suggesting new features
- by bringing in your knowledge and discussing the project in our [wiki](https://github.com/skasberger/open-weather-station/wiki)
- by translating content to a new language
- by writing or editing documentation
- by writing specifications
- by writing code and documentation (**no pull request is too small**: fix typos, add code comments, clean up inconsistent whitespace)
- by reviewing [pull requests](https://github.com/skasberger/open-weather-station/pulls).
- by closing issues
- by using the data for visualizations or an analysis

If you have any questions, you can email me team at [open-weather-station@stefankasberger.at](mailto:open-weather-station@stefankasberger.at).

#### Submit Great Issues
* Before submitting a new [issue](https://github.com/skasberger/open-weather-station/issues), check to make sure [a similar issue isn't already open](https://github.com/skasberger/open-weather-station/issues?q=is%3Aissue+is%3Aopen). If one is, contribute to that issue thread with your feedback.
* When submitting a bug report, please try to provide as much detail as possible, i.e. a screenshot or [gist](https://gist.github.com/) that demonstrates the problem, the technology you are using, and any relevant links. 

# RESOURCES
- [Wetterstation - Wikipedia](https://de.wikipedia.org/wiki/Wetterstation)
- [Wetterstationen im Test](http://www.funkwetterstationen-test.com/)
- [Weather Underground](https://www.wunderground.com)
- [Meteoplug Wiki](http://wiki.meteoplug.com/Main_Page)


