# _Wetlands Geoprocessor (v 1.0)_

## _Contact_

Questions on this model should be directed to Cleve Davis (clevebdavis@gmail.gov).

## _Module Summary_

Wetlands have often been described as the “Earth’s kidneys” because wetlands have the ability filter pollutants and purify water. Based upon wetland storage capacity, average daily flow, and inflow nutrient loading this model estimates potential load reductions of nitrate (NO<sub>3</sub><sup>-</sup>) and orthophosphate (PO<sub>4</sub><sup>3-</sup>) from a constructed surface flow wetland (CW). The model relies upon equations, coefficients, and models provided by Cheng et al. 2020 and Cheng & Basu 2017.

Nitrogen (N) and phosphorus are important nutrients to ecosystems, but high concentrations can lead to water quality issues. Major sources of these nutrients come from agricultural areas where fertilizer is applied in large quantitates and/or animal waste is present. Excess nitrate and phosphorus may result in overgrowth of algae, which can decrease the dissolved oxygen in water, thereby harming and killing fish and other aquatic species. This model evaluates water purification results and estimates cost to install a surface flow constructed wetlands.

## Data Sources & Pre-processing

**Data Sources:** User interacts with online map by drawing a polygon where the CW will be located along the system. The user is required to enter the total number of days to evaluate and the average flow in cubic feet per second (cfs) for the specified time period. The user has a few options for entering incoming nitrate (NO<sub>3</sub><sup>-</sup>) and orthophosphate (PO<sub>4</sub><sup>3-</sup>) loads.

If known, the user can enter the average value in mg/L or parts per million (ppm) entering the CW. Under this scenario the tool will calculate an exact value based upon model. Please keep in mind that there is high variability on estimated removal potential of CW and debate on this topic. For more information on the accuracy of the model see the discussion on Expected Accuracy below.

If nitrate and orthophosphate loads are not known, the user also has the option to select three "at-risk" categories. These at-risk categories have been established to identify the potential for algal blooms based upon the EPA recommendations and scientific literature and what the user knows about their respective system. Descriptions of the categories are as follows.

| Nitrate Concentration Level (mg/L or ppm) | Orthophosphate Concentration Level (mg/L or ppm) | Category    | Characteristics of the Category                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |     |
| ----------------------------------------- | ------------------------------------------------ | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --- |
| 0.12 to 2.2                               | 0.01 to 0.075                                    | Low-Risk    | Drainage area dominated mostly by native vegetation and waterways support connected wetlands that provide habitat for a diversity of native plants, wildlife, and fish. Water is typically cool and clear year around.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |     |
| >2.2 to 5                                 | >0.076 to 0.1                                    | Medium-Risk | Drainage area supports some farmlands, pasture/rangeland, and residential development. Most waterways have intact wetlands and/or natural vegetation that minimizes runoff discharge into streams. However, there may be some places where applied fertilizer, animal waste and sewage may reach waterways through runoff or seepage. The temperature of the water is typically cool and color can vary from clear to slightly cloudy. During warmer times of year, slow moving reaches or ponds within the system may turn slightly green due to algal growth. Wetland areas and riparian areas provide some habitat for native fish and wildlife, but may also harbor non-native species, especially rough fish. |     |
| >5 to 10                                  | >0.1 to 1                                        | High-Risk   | Streams within the drainage area subjected to high levels of runoff from intensive agricultural activities and other industrial activities, confined animal feeding operations, and/or municipal waste. Non-native vegetation is abundant and provide little to no benefit to native fish and wildlife. Most riparian areas within the system support non-native species and lack adequate vegetation buffers to prevent runoff into streams. The temperature of the water is usually cool to warm and water is cloudy from sedimentation and algal growth. During warmer times of year, slow moving reaches or ponds often require herbicide treatment to maintain flow and irrigation equipment operation.       |     |

Naturally occurring levels of nitrate and total nitrogen vary substantially and statistical analysis by the [Environmental Protection Agency](https://cfpub.epa.gov/roe/indicator.cfm?i=31) (EPA) suggests that appropriate reference levels range from 0.12 to 2.2 mg/L total N, such that some streams in the lowest category (less than 1 mg/L) may still exceed recommended water quality criteria.

However, there is currently no national water quality criterion for total phosphorus and orthophosphate to protect surface waters. Nuisance algal growths are not uncommon in rivers and streams below the low reference level (0.1 mg/L) for phosphorus. EPA statistical analyses of water quality data suggest that a more appropriate reference level for total P range from 0.01 to 0.075 mg/L, depending upon the ecoregion.

Nitrate and phosphate levels both significantly affect algal growth and observations have demonstrated when one nutrient is substantially increased the other nutrient will limit the growth (Fried et al. 2003). For example, if nitrogen is present in very high concentrations, and phosphorus is not, the algae will proliferate until it has used up all of the phosphorus. Therefore, proliferation of algal blooms can be expected if both nutrient are present in high concentrations.

Although the [EPA](https://www.epa.gov/ground-water-and-drinking-water/national-primary-drinking-water-regulations) recommends that nitrate concentrations be kept below 10 mg/L and phosphorus be kept below 0.1 mg/L to keep algae growth at a minimum, algae can proliferate at phosphorus levels of 0.05 mg/L when substantial amounts of nitrogen is available (Fried et al. 2003). It should also be mentioned that various algal species likely have varying physiological responses to varying concentrations of nutrients. However it is generally accepted that fertilizer runoff affects the entire aquatic community.

**Pre-processing:** None.

## Inputs & Outputs

**Inputs Required**

- **Flow (cfs)**: User will enter estimated average flow in cubic feet per second (cfs) for time period analyzed.
- **Acres**: <span dir="">Users will draw a polygon to identify the surface area of the wetland along the system.</span>
- **Days**: <span dir="">User will enter the time period to be analyzed in days.</span>
- **no3_data**: NO<sub>3</sub><sup>-</sup><span dir=""> User will enter inflow load of Nitrate entering constructed wetland in mg/L or ppm.</span>
- **po4_data**: PO<sub>4</sub><sup>3-</sup><span dir=""> User will enter inflow load of orthophosphate entering constructed wetland in mg/L or ppm.</span>

**Outputs/Results**

- **ppm_no3**: Value represents nitrate load of inflow. This is actually input but was provided to show values used when running the load-risk calculation.
- **ppm_po4**: Value represents orthophosphate load of inflow. This is actually input but was provided to show values used when running the load-risk calculation.
  Outputs for kg removed and percent removed are provided in two ways. If the user enters the actual values into no3_data and po4_data only two values will be returned. The first value corresponds to the amount of N removed and the second value corresponds to the amount of P removed. If the user selects a load_risk (i.e., low, mid, high) option the tool returns two arrays. The first array corresponds to the low and high value of N removed and the second array corresponds to the low and high value of P removed.
- **kg_removed**: Kilograms of NO<sub>3</sub><sup>-</sup> and PO<sub>4</sub><sup>3-</sup> removed based upon surface area, time, and flow.
- **pct_removed**: Percentage of NO<sub>3</sub><sup>-</sup> and PO<sub>4</sub><sup>3-</sup> removed based upon surface area and flow.
- **load**: NO<sub>3</sub><sup>-</sup> and PO<sub>4</sub><sup>3-</sup> load remaining in the outflow.
- **P ppm remaining**: PO<sub>4</sub><sup>3-</sup> load remaining in the outflow.
- **t_cost**: Estimated total cost in dollars for installing a constructed wetland. Value includes lower confidence interval, mean, and upper confidence interval.
- **c_acre**: Estimated cost per acre in dollars for installing a constructed wetland. Value includes lower confidence interval, mean, and upper confidence interval.

## Module Formulations

**Purification Equations**

- The percent wetland NO<sub>3</sub><sup>-</sup> and PO<sub>4</sub><sup>3-</sup> for the CW was estimated as a function of the removal-rate constant and water residence time for the CW using first-order removal rate kinetics (Cheng & Basu 2017, Spieles & Mitsch 1999).

## _Module Formulation_

- **Module Equations**

  ```math
  p_{wet} = (1 - e^{-kt}) * 100
  ```

  - $`k`$ = Removal-rate constants for the CW. Estimated values of constructed surface flow (CSF) from Cheng & Basu 2017 were used.
  - $`t`$ = Water residence time in days. Estimated by taking the average depth of the CW (1.35 m) multiplied by surface area (SA) to yield storage volume. The time in days could then be obtained by calculating the amount of time it took to fill the storage volume. The model assumes the average depth by taking a weighted average of important CW components necessary for removing sediment, nutrients, bacteria, pesticides, and organic matter from runoff identified in the 2007 USDA Technical Notes Biology No. 22 (revised). The coefficients and exponents _a_, _b_, _c_, and _d_ were empirically derived by Cheng & Basu 2017.

  ```math
  t_ = a(SA)^{b}
  ```

  ```math
  k_{i} = ct_{i}^{d}
  ```

## _Module Formulation_

- **Module Equations**

  - _Means calculated with the equation:_

  ```math
  \bar{x} = \frac{\sum_{i=1}^{n} x_{i}}{n}
  ```

  - Confidence intervals calculated with the equation with an alpha of 0.05:

  ```math
  \text{Confidence Interval} = \bar{x}\pm z \frac{s}{\sqrt{n}}
  ```

  - Opportunity cost calculated with the equation:

  ```math
  \text{Opp. Cost (\$)}=\frac{\text{Lease Value (\$)}}{acre}*\text{Wetland Size(acres)}
  ```

  - Material cost equation:

  ```math
  \text{Materials (\$)} = \text{Plant Materials (\$)}+\text{Construction Materials (\$)}
  ```

  - Total cost equation:

  ```math
  \text{Total Cost (\$)} = \text{Planning Cost (\$)}+\text{Labor Cost (\$)}+\text{Fuel Cost (\$)}+\text{Materials Cost (\$)}+\text{Opp. Cost (\$)}
  ```

  - Total cost per acre equation:

  ```math
  \text{Total Cost}\frac{\$}{Acre}=\frac{\text{Total Cost (\$)}}{\text{Wetland Size(acres)}}
  ```

  - Inflation for empirical construction cost estimation equation is provided below. The Consumer Price Index (CPI) for "All items in U.S. city average, all urban consumers, seasonally adjusted (Month of June)" was used to account for inflation.

  ```math
  \text{Inflation}=(\text{CPI Current}-\text{CPI Estimated Year})/\text{CPI Estimated Year}
  ```

  - Equation to account for inflation:

  ```math
  \frac{Dollars_{2020}}{\text(Acre)}=\text{Inflation}*\frac{\text{Cost Estimate (\$)}}{\text(Acre)}
  ```

  - Equation to estimate constructed wetland cost in 2020 Dollars:

  ```math
  \text{Constructed Wetland Cost (\$2020)}=\frac{Dollars_{2020}}{\text(Acre)}+\text{Original Estimated Cost (\$)}
  ```

  - Confidence intervals for estimations were calculated using the t distribution.

## Expected Accuracy

**Purification Potential Estimations**

A wide range of estimates for NO<sub>3</sub><sup>-</sup> and PO<sub>4</sub><sup>3-</sup> removal arise from complexities of removal processes in wetlands. Wetland removal of NO<sub>3</sub><sup>-</sup> and PO<sub>4</sub><sup>3-</sup> can be influenced by a number of factors including nutrient loading, temperatures, precipitation, flows, available carbon, wetland area, residence time, wetland type, plant biomass, substrate, microbial activity, etc.

To check the accuracy of the model, the model was simulated controlling NO<sub>3</sub><sup>-</sup> and PO<sub>4</sub><sup>3-</sup> loads, number of days, and flow to compare how the model compared with published percent removal rates for NO<sub>3</sub><sup>-</sup> (Reilley et al. 2000, Moreno-Mateos et al. 2010, Baker 1998, Raisin et al. 1997, Kovacic et al. 2000, Harrington et al. 2007, [Minnesota Pollution Control Agency](https://www.pca.state.mn.us/water/nitrogen), Cheng & Basu 2017) and PO<sub>4</sub><sup>3-</sup> (Raisin et al. 1997, Kovacic et al. 2000, Kasak 2018, [Minnesota Pollution Control Agency](https://www.pca.state.mn.us/water/nitrogen), Cheng & Basu 2017).

Based upon these published papers the average percent removal of NO<sub>3</sub><sup>-</sup> was 52.4% with an upper CI of 69% and lower CI of 37%). For orthophosphate the average percent removal was 24.6% with an upper CI of 46% and lower CI of 3%. Although there are many factors related to sizing a constructed wetland, one general rule of thumb is that wetlands should be sized to be 1-2 acres per cfs (personal communication with Megan Skinner USFWS).

To evaluate if the model predicted values within published percent removal ranges, it was simulated by controlling loads for NO<sub>3</sub><sup>-</sup> at 5 ppm and PO<sub>4</sub><sup>3-</sup> at 0.5 ppm. A flow of 400 cfs and time period of 180 days was also controlled for all simulations. The results of the simulations are provided in the graphic below. Utilizing the general rule of thumb on sizing a wetland to be 1-2 acres per cfs the model output values are within the percent removal CI estimations. It should also be noted that the equation is likely biased towards "appropriately sized" wetlands and the estimations of removal potential for undersized wetlands is likely inflated, while estimations for oversized wetlands is likely underestimated.

![Constructed_Wetlands_Percent_Removal](uploads/375303fef9469b1938cd135cf3cdef3a/Constructed_Wetlands_Percent_Removal.png)

As can be observed with the large confidence intervals for percent removal estimates, actual removal rates can vary substantially and the potential to remove contaminates is an active area of research. Nonetheless it is well established that wetlands can be effective tools to remove fertilizer and other contaminants, despite the debate among researchers on modelling approaches. Therefore, the results of this model should be viewed as approximations with high variability.

**Construction Cost Estimations**

In regard to the accuracy of construction costs, the values calculated by the model are dependent upon published results of wetland purification potentials and construction costs.

## Assumptions

Despite a large body of research on designing wetlands is available, the optimal design of constructed wetlands for various applications is not known. Purification performance is also highly impacted by location, water inflow, design, climate, weather, disturbances, as well as daily, seasonal variability, etc. Therefore, this model makes a number of assumptions about the constructed wetland and it is important to acknowledge that each wetland project is unique and one size does not fit all. In other words, the design of the constructed wetland system will be site-specific. In general, wetland designs should attempt to mimic natural wetlands for the area. Some basic assumptions of this model includes the following. The constructed wetland will have adequate drainage area and be appropriately sized. It is also important that plants receive adequate water to ensure viability and function. The established wetland should also have multiple vegetative growth zones through varying depths and robust and diverse vegetation has been established within the wetland. Relatively impermeable soils or engineered liner is part of the construction. Sediment collection and removal is performed regularly to maintain wetland function. The wetland has an adjustable permanent pool and dewatering mechanism (outlet control device). Invasive weeds are eliminated/controlled to allow planted vegetation to take.

## Limitations

As mentioned under the model accuracy section, the model is likely biased towards "appropriately sized" wetlands. Therefore, it is recommended that the user create a wetland polygon area with IrrigationViz that would be considered an appropriately sized and shaped wetland. Optimally, this would be done by digitizing a engineered design that was created for the site in question. If an engineering design is not available, the rule of thumb for appropriately sizing (1-2 acres per cfs) the wetland could be used and located where a natural wetland once existed, or a low-lying area at the end of an irrigation system that has high loads of fertilizer pollution.

The model also currently does not provide CI's for purification potential estimations which likely vary greatly between systems.

## References

- BF Environmental Consultants. n.d. "Constructed Wetlands." BF Environmental Consultants. Accessed March 15, 2021. https://www.bfenvironmental.com/pdfs/ConstrWetlands.pdf.

- Carroll, P., Harrington, R., Keohane, J., & Ryder, C. (2005). Wetland Treatment Performance and Environmental Impact of Integrated Constructed Wetlands in the Anne Valley Watershed, Ireland. In E. Dunne, K. Reddy, & O. Carton, Nutrient Management in Agricultural Watersheds: A Wetland Solution (pp. 207-217). The Netherlands: Wageningen Academic Publishers.

- Cheng, F.Y., Basu, N.B. 2017. Biogeochemical hotspots: role of small water bodies in landscape nutrient processing. Water Resource Research. 53:5038-5056.

- Cheng, F.Y., Van Meter, K.J., Byrnes, D.K., Basu, N.B. 2020. Maximizing US nitrate removal through wetland protection and restoration. Nature 588:625-630.

- Fried, S., Mackie, B., Nothwehr, E. 2003. Nitrate and phosphate levels positively affect the growth of algae species found in Perry Pond. Tillers 4:21-24.

- Harrington, R., P. Carroll, A.H. Carty, J. Keohane, and C. Ryder. 2007. "Integrated Constructed Wetlands: concept, design, site evaluation and performance." International Journal of Water 243-256.

- Kasak, K., K Kill, J. Pärn, and Ü Mander. 2018. "Efficiency of a newly established in-stream constructed wetland treating diffuse agricultural pollution." Ecological Engineering 1-7.

- Kovacic, D.A., M.B. David, L.E., Starks, K.M. Gentry, and R.A. Cooke. 2000. "Effectiveness of constructed wetlands in reducing nitrogen and phosphorus export from agricultural tile drainage." Journal of Environmental Quality 1262-1274.

- Minnesota Pollution Control Agency. 2019. Overview for stormwater wetlands. August 13. Accessed February 13, 2021. https://stormwater.pca.state.mn.us/index.php?title=Overview_for_stormwater_wetlands.

- Moreno-Mateos, D., D. Pedrocchi, and F.A. Comín. 2010. "Effect of wetland construction on water quality in a semi-arid catchment degraded by intensive agricultural use." Ecological Engineering 631-639.

- Newton, Rebecca. 2006. "Constructed Wetlands." Colorado State University Department of Biology. Accessed March 15, 2021. https://sites.biology.colostate.edu/phytoremediation/2006/Rebecca%20Newton%20Website%20Files/public_html/CW.html.

- Noack, Tim. 2018. "Costs and Other Considerations for Constructed Wetlands." Texas A&M University Kingsville. March 7. Accessed February 22, 2021. https://tamuk-isee.com/wp-content/uploads/2018/03/Costs-and-Other-Considerations-for-Constructed-Wetlands-Tim-Noack.pdf.

- Ohio State University Extension. 2016. "Constructed Wetlands (NRCS 656)." https://agbmps.osu.edu/. Accessed March 15, 2021. https://agbmps.osu.edu/bmp/constructed-wetlands-nrcs-656.

- Raisin, G.W., D.S. Mitchell, and R.L. Croome. 1997. "The effectiveness of a small constructed wetland in ameliorating diffuse nutrient loadings from an Australian rural catchment." Ecological Engineering 19-35.

- Reilly, J.F., A.J. Horne, and C.D. Miller. 2000. "Nitrate removal from a drinking water supply with large free-surface constructed wetlands prior to groundwater recharge." Ecological Engineering 33-47.

- Tyndall, J., and T. Bowman. 2016. Draft Iowa Nutrient Reduction Strategy Best Management Practice cost overview series: Constructed wetlands. Accessed February 22, 2021. https://www.nrem.iastate.edu/bmpcosttools/files/page/files/2016%20Cost%20Sheet%20for%20Constructed%20Wetlands.pdf.

- Spieles, D.J., Mitsch, W.J. 1999. The effects of season and hydrologic and chemical loading on nitrate retention in constructed wetlands: a comparison of low- and high-nutrient riverine systems. Ecological Engineering 14:77-91.

- USDA. 2007. Technical Notes USDA-Natural Resources Conservation Service Boise, Idaho. TN Biology No. 22 (revised).
