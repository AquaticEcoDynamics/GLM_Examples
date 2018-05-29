# Lake Kinneret

## Study Site
Lake Kinneret is a [freshwater lake](https://www.researchgate.net/publication/289411199_Water_quality_modelling_of_Lake_Kinneret_Sea_of_Galilee) (32 ºN, 35 ºE) situated in northern Israel, and is the lowest freshwater lake in the world (209m below Mediterranean Sea Level).
The lake has a surface area of 173 km<sup>2</sup>, and is about 49 m deep.

## Model Setup
The model is set-up to simulate the hydrological domain of Lake Kinneret for 2 years, from **1997-01-01** to **1999-01-01** (`&time`), with water balance and heat fluxes [hypothetically calculated](http://aed.see.uwa.edu.au/research/models/GLM/downloads/AED_GLM_v2_0b0_20141025.pdf) based on the lake configuration and input data. Water quality functionality (AED2) is disabled for the simulation (`&wq_setup`).


#### Lake Configuration
The flexible model structure allow users to configure the switches of the individual model components, enabling the customization of the physical model, meteorological and flow conceptualisations.


**Physical Model Configuration**

| Configuration Flags | Description | Activation |
| ---------------- |:----------|:-----------:|
| `&morphometry` | Lake location (*latitude and longitude*) and bathymetry (*depth and area*) setup | - |
| `&wq_setup` | Water Quality setup | *Disabled* |
| `&init_profiles` | Initial lake conditions with depths (eg. *temperature and salinity* ) | - |
| `&output` | Specification of output file details | - |

**Meteorological Configuration**

| Configuration Flags | Description | Activation|
| ---------------- |:----------|:-----------:|
| `met_sw = .true.` | Surface meteorological forcing | *Enabled* |
| `lw_type = 'LW_IN'` | Incident longwave radiation is provided in the meteorological data | *Enabled* |
| `subdaily = .true.` | Subdaily meteorological input setup switch (in *hourly timesteps*; `dt = 3600`) | *Enabled* |
| `&bird_model` | Incorporation of *Bird Solar Radiation* model which theoretically computes solar radiation based on available data| *Enabled* |

**Flow Configuration**

| Configuration Flags | Description | Activation |
| ---------------- |:----------|:-----------:|
| `subm_flag = .false.` | Configuration of submerged inflow; Disable to activate surface inflow | *Disabled* by default|
| `seepage = .false.` | Configuration of seepage processing | *Disabled* by default|


#### Input Data
Model inputs include a time-series of hourly meteorological conditions, 6 daily inflows, and 1 daily outflow in the [specified format and column order](http://aed.see.uwa.edu.au/research/models/GLM/downloads/AED_GLM_v2_0b0_20141025.pdf) (Table 1).

**Table 1**  Input data for simulation of Lake Kinneret.

| Input Data     | Filename   | Code Section |
| ---------------- |:----------:|:-----------:|
| meteorological | *met_1997_2004.csv*| `&meteorology`|
| inflows | **Jordan** *inflow_1_v2_wq_1997_2004.csv*, **Neger** *inflow_2_v2_wq_1997_2004.csv*, **Yarmuch** *inflow_3_v2_wq_1997_2004.csv*, **Groundwater** *inflow_4_v2_wq_1997_2004.csv*, **Kinneret7** *inflow_5_v2_wq_1997_2004.csv*, **Salt Canal** *inflow_6_v2_wq_1997_2004.csv*, |`&inflow`|
| outflows | *outflow_v2_1997_2004.csv*|`&outflow`|

### Example Output
Following each simulation, the model produces a .csv of time-series reservoir conditions detailing heat fluxes/water balance (*lake.csv*), an optional .csv of specific depth time-series water quality values (*WQ_5*), along with a NetCDF file detailing the values of each in-lake variables with time and depth (*output.nc*). For simple time-series plots, users can extract the values directly from the .csv file; For advanced plots, user may load the *output.nc* into MATLAB to produce the following outputs :

![alt text](https://fuybrg-dm2305.files.1drv.com/y4mmRBjPuET6q9VjZjGpFoF7tjdu2HU-fdXZbksl0CmVeJFvGgKHhjgR_O4tV0IqLrqoR9IBgs2stTd-DmmEJOSzTtr9J6tCPFTP7-Wv6aA25jd0ESjpc07ypbzyScvbquAh8766t9AqgjM3U141hts-bszOVc4enlZZGatDKi7rj8Th3TrVz59ihe22OerxzaO1zK1nEVIu2mJ5LFVd4GHtJiLyd2g9MhNn6QXrKR1p1I?width=1460&height=565&cropmode=none)
**Figure 1** Time-series Heat Fluxes of Lake Kinneret over 2 years

![alt text](https://gpybrg-dm2305.files.1drv.com/y4mrGuVhInGaTKVraS--wePbVIsMTRUTvuwemCFwx-UMUPsuvSbcBvRA5Y2Qou6d2T80sJBl2nf-X0kRii_Z8itsGHDRpIY5y5lzTVV_7SNTmJeLLDFhLERGR8uYPE2W1pdDNgQYAaG3JiRyf6HrJ4a5kEOCeLBS9Q-qymB2fTDLHHaAp39bdqC3reJV7vUzS7WRGxQk4IaJ_ia-sT8pZme0llL3BkGtCSsW4EBC_gpb60?width=1460&height=565&cropmode=none)
![alt text](https://guybrg-dm2305.files.1drv.com/y4mFupf8UPzOF0dOSYcVNabt0Rb-ZH3mPZwz3LjLO7v9Zy5eiuy5xD7SPq1SbwhEw_q4m4q8kwVGZWPs9_oHBeqv4XiFcvcaZte_d6ci9DwY1NEWGDMzqlq4oCYSGKrnLTwr8f9C-CNCLd2bRIZVnI6ylmAA_66OVnOu6-E3Y4pCapsZ4_jzR0FOijJsa7D0NXLyi5j2gaQOtfR8tEnipnDCayrjr_ST-NmqVpzLKRLlzU?width=1460&height=565&cropmode=none)
**Figure 2** Time-series Water Balance of Lake Kinneret over 2 years


![alt text](https://eow2iw-dm2305.files.1drv.com/y4mRI5yJ8Wo88qXyWnJ920CG-r8MBW3f4RweBLLEytgSjzuwLPgQye6Z2L6r1IMCl0wMUC6Uj1YQ4XMuuJMYGAd-KbdAY4_m2FZkbZnpBHcRpZ2GFu0l48k_qjkGoD75poc1LVXeMJPCf7fEeW_wmuJq2JvgRUtdp_52yPes2pyIvVmp876yQti04XFwu2tS8hKWapZa1gZt9CnqMsT8Y1FjBFIImwZLOlcSM2cRcL95Zs?width=875&height=656&cropmode=none)
**Figure 3** Temperature-Depth contour plot of Lake Kinneret over 2 years


## Further Notes
- Users can switch off individual model components of interest by inserting `!` before the codes.
- Users can tweak the resolution of model simulation by adjusting `min_layer_thick` and `max_layer_thick`.
- Users can set output directory/filenames under `&output`, along with the option of exporting modelled data at different specified depths.
- Users can choose to incorporate AED2 water quality module by switching on `&wq_setup` component (i.e. remove `!` before the codes).
