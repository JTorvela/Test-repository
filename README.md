# Project of no name

**Author:** Janne Torvela
**Contact:** janne.torvela@oulu.fi
**Organization:** Intelligent Machines and Systems, University of Oulu
**Website:** -

## Project Overview
* problem statement: 

How to calibrate a large number of identical temperature sensors as a group to get comparable data out of multiple temperature probes constructed out of these sensors. 

* challenge statement: why has this problem not been solved before?

Either the previous researchers hadn't bothered, or they didn't report their methods and results.

* solution statement: what specific element of the challenge does your research resolve?

Addressing common sources of error and describing the data processing in a repeatable manner. 

* objective: how will you accomplish this?

Describing common sources of errors and their solutions, and processing the data. 

* literature review: focus on foundational or methods papers that closely describe your analytical workflow.

Statistical methods here listed as references only: 
Davison A.C., Hinkley D.V., 1997, Bootstrap Methods and their Application. Cambridge: Cambridge University Press (Cambridge Series in Statistical and Probabilistic Mathematics). 
Efron B, 1979, Bootstrap Methods: Another Look at the Jackknife, The Annals of Statistics, Ann. Statist. 7(1), 1-26, (January), DOI: 10.1214/aos/1176344552

Elyounsi A., Kalashnikov A.N., 2021, Evaluating Suitability of a DS18B20 Temperature Sensor for Use in an Accurate Air Temperature Distribution Measurement Network. Eng. Proc. 2021, 10, 56. https://doi.org/10.3390/ecsa-8-11277 
Quote: "We analysed literature data and our experimental results to determine why the readings of different temperature sensors might be notably different in air despite being placed in close proximity. We attributed these differences to two factors—unrestricted air movements and differences in the sensors’ response times. After elimination of these factors, the temperature readings of Pt100 and DS18B20 sensors exhibited an excellent agreement which, together with the convenient networking features provided by the DS18B20 sensors, confirmed their suitability for our use case."

Maxim Integrated Products Inc., 2002, Application note 208. Curve Fitting the Error of a Bandgap-Based Digital Temperature Sensor, https://www.analog.com/en/resources/technical-articles/curve-fitting-the-error-of-a-bandgapbased-digital-temperature-sensor.html (accessed 30.1.2026)
Quote: "A mathematical method is presented in this application note that allows the user to improve the accuracy of bandgap-based digital temperature sensors. This method increases the accuracy by compensating for the offset and curvature of the device error characteristic. This technique is useful for applications that require greater than the ±0.5°C accuracy provided by Maxim Integrated's precision temperature sensor ICs."^ 

Maxim Integrated Products Inc., 2019, Programmable Resolution 1-Wire Digital Thermometer, https://www.analog.com/media/en/technical-documentation/data-sheets/DS18B20.pdf (accessed 30.1.2026)
Quote: "The DS18B20 digital thermometer provides 9-bit to 12-bit Celsius temperature measurements and has an alarm function with nonvolatile user-programmable upper and lower trigger points. The DS18B20 communicates over a 1-Wire bus that by definition requires only one data line (and ground) for communication with a central microprocessor. In addition, the DS18B20 can derive power directly from the data line (“parasite power”), eliminating the need for an external power supply."^
^Reviewer's note: Maxim Integrated Products has been incorporated by Analog Devices Inc. since 2021. 
The closest to a “foundation paper” here would be Elyounsi, Kalashnikov 2021 which details the effects of placement between the reference sensor and the sensors being calibrated, although the basic point and method of calibration is described in Maxim Integrated Products Application note 208. 

* research questions: 

The error characteristic of a DS18B20 digital temperature sensors is described by the manufacturer as a second order curve (Maxim Integrated 2002). To compensate for the measurement error at some arbitrary temperature, we must find a closely fitting second order equation described by its coefficients ax + bx^2 + c for each sensor we intend to use. We must evaluate the following points: 
1) How closely does the error curve match between different sensors? Can we use a single equation for multiple sensors? 
2) How large are the residuals after correction? What is the accuracy we reach after calibration?
3) Can we store the resulting coefficients in reduced precision to save memory on an IoT device without losing accuracy? How much accuracy is lost?
To ensure that the comparisons between a reference sensor and the sensors in calibration are valid, we must ensure that all sensors have stabilized to the same temperature inside an isolated enclosure (Elyounsi, Kalashnikov 2021). Our approach is to provide isothermal conditions by constant air circulation inside an insulated box, which is connected to the external environment through a large mass of aluminum metal to act as a stabilizing heat reservoir. Air is circulated inside the box by a fan to eliminate temperature differences. The mechanical power of the fan will increase the temperature inside the enclosure somewhat, but this is of no consequence to the comparison. 
The box with the sensors inside is placed in an environmental chamber which is cooled to -40 C and heated up to +40 C in discrete steps each lasting two hours. To avoid errors caused by different response times between the sensors, we manually select data which no longer displays monotonic change after each change in temperature and discard the rest from analysis. 

## Data Sources

Describe your study area, and period of interest. Specify whether training data represents a different location/time period than forecast simulations. Detail the temporal and spatial frequency of your process.

### Published Data Sources
| Name | Source | Description | Access Method | data DOI/url | metadata DOI/URL| details | data citation |
|------|--------|-------------|---------------|--------------|-----------------|---------|---------------|

### Data Access Notes
Many public geospatial data repositories require user authentication to access data. In the methods section, detail which data sources require registraton to access. Link to sign up portals for any listed data sources that require user authentication. In the "How to Reproduce," descripe how to configure automatic access control mechanisms for each data source. 

### Inputs folder
Any direct data download links can be pasted into the "datalinks.txt" file in the inputs folder. Specify which dataset links can be accessed via the datalinks.txt folder. Note: this should only be used for PDIs: if the url changes, it will break the reproducibility of your workflow.

Detail any datasets that are in your inputs data folder. Note this is only for data that is too small/trivial to be published: **no files greater than 10 MB can be stored in repository**. Examples might include spatial polygons that have undergone geometry simplification for API searches, text-based keys mapping variable names to integer values, etc.

## Methods Summary

**Model Framework:** {{ cookiecutter.model_framework }}
Describe steps involved in data preprocessing

## Repository Structure

| Folder/File | Description |
|-------------|-------------|
| notebooks/ | SE1–SE4 notebooks |
| inputs/ | minimal input data required, note most data should be stored on OGC/FAIR compliant databases and accessed from stable URLs |
| processed_data/ | analysis-ready datasets |
| model_data/ | Saved model outputs, model configuration files, predictions|
| figures/ | Figures, tables, graphs, and data-derivatives (e.g. summary statistics) displayed in manuscript text |
| run_reproducibility.py | Reproducibility wrapper |
| Dockerfile | Reproducible container |
| CITATION.cff | Citation metadata, sourced directly from Zenodo |

## How to Reproduce

### Computational requirements
What operating system, processor type, and processor specifications (RAM, cores, etc).

If GPU processing, specify CUDA version.

### Data access configurations
Describe in detail any access control mechanisms that need to be configured for an individual user to access data (e.g. tokens, cookies, certificates, URL customization). Provide links to documentation.

### Run the code
```bash
pip install -r requirements.txt
python run_reproducibility.py
```
## Results

Display key figures in `/figures` folder, with description:

![Example](figures/example.png)

## Citation
All repositories should be published on a platform providing persistent object identifiers (e.g. Zenodo).

DOI: **DOI_PENDING**

## License

{{ cookiecutter.license }}

## Contribution Guidelines
Contributions that improve the quality, clarity, and reproducibility of this project are welcome.
* Open an issue before making major or result-affecting changes.
* Keep pull requests focused and clearly describe what changed and why.
* Follow existing code style and update documentation as needed.
* Do not modify code or data used to reproduce published results without discussion.
* Ensure workflows remain reproducible (environment, dependencies, random seeds).
* Do not commit large or restricted datasets; respect data licenses.
By contributing, you agree that your work will be released under the project’s license.

## Notes:
Focus on graphically rich, interactive elements to communicate your research to diverse stakeholders.
[Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/markdown-cheatsheet) 


  
