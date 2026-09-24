# Datasheet for the `dengColombo` (`colmozzie`) Dataset

*Following the framework of Gebru et al. (2018): "Datasheets for Datasets"*

## 1\. Motivation

**For what purpose was the dataset created?**

`dengColombo` was assembled to support research into the association between climate conditions and dengue fever incidence in Sri Lanka. It provides a paired time series of weekly reported dengue cases and meteorological measurements for the Colombo district, enabling analysis of climate–disease lag relationships and reproduction-number estimation. The dataset is distributed via the `colmozzie` R package (available on CRAN). In this tutorial the weekly series is read directly as a CSV from the package's GitHub repository (`data-raw/dengColombo.csv`).

**Who created the dataset, and on whose behalf?**

Case counts are sourced from the Epidemiology Unit, Ministry of Health, Sri Lanka — the national authority responsible for notifiable disease surveillance. The `colmozzie` R package was created and is maintained by Thiyanga S. Talagala (Department of Statistics, University of Sri Jayewardenepura) as a convenience wrapper.

---

## 2\. Composition

**What do the instances represent?**

Each instance (row) represents one calendar week of observation associated with the Colombo district, Sri Lanka. Each row pairs a reported dengue case count with a set of weekly climatological measurements.

**How many instances are there?**

279 weekly observations. As distributed in the `colmozzie` data object, the series runs from **2009 (Week 1\) through 2014 (Week 21\)**.

> **Discrepancy to be aware of:** The CRAN package description and help file state the coverage as "2008/week-52 to 2014/week-21." The actual data object begins at 2009/Week 1; there is no 2008 row. Cite the data object, not the package blurb, for the true start date.  
>   
> **Truncated final year:** The series terminates at Week 21 of 2014\. The final 31 weeks of 2014 are absent, producing an incomplete final year. Users performing annual or seasonal aggregations should account for this truncation.  
>   
> **Internal gap:** 2013 contains only 50 weeks — **Weeks 37 and 38 of 2013 are missing** from the series. This is an interior gap, not an end-of-series truncation, and is easy to miss. (Week numbering otherwise runs 1–53; ISO Week 53 appears in the 2009 block.)

**What data does each instance contain?**

| Column | Type (as stored) | Description | Units |
| :---- | :---- | :---- | :---- |
| `Cases` | Integer | Total weekly notified dengue cases | Count |
| `Year` | Integer | Calendar year | — |
| `Week` | Integer | Week number within the year (1–53) | — |
| `TEM` | Float | Weekly average air temperature | °C |
| `TMAX` | Float | Weekly maximum air temperature | °C |
| `Tm` | Float | Weekly minimum air temperature | °C |
| `SLP` | **Character** (should be numeric) | Sea-level pressure | hPa |
| `H` | Float | Relative humidity | % |
| `PP` | Float | Precipitation amount | mm |
| `VV` | Float | Mean visibility | km |
| `V` | Float | Mean wind speed | km/h |
| `VM` | Float | Maximum sustained wind speed | km/h |

*Column names and definitions match the `colmozzie` help file (`?colmozzie`). Note that `SLP` is stored as a character vector in the distributed data because of one corrupted value (see below), and must be coerced to numeric before use.*

**Summary statistics for key variables (n \= 279):** *(recomputed directly from the CSV the notebook ingests and confirmed accurate)*

| Variable | Mean | SD | Min | Q25 | Median | Q75 | Max |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| Cases | 116.3 | 79.5 | 0 | 57 | 99 | 155 | 475 |
| TEM (°C) | 27.6 | 0.88 | 24.2 | 26.9 | 27.5 | 28.2 | 29.7 |
| H (%) | 79.8 | 4.2 | 62.0 | 78.3 | 79.9 | 82.1 | 90.3 |
| PP (mm) | 6.5 | 9.6 | 0.0 | 0.7 | 4.1 | 8.3 | 71.3 |
| SLP (hPa) | 1009.0 | 1.2 | 1006.0 | 1008.3 | 1008.9 | 1009.8 | 1012.8 |

*(SLP statistics computed after dropping the one corrupted value; n \= 278 for SLP.)*

**Is any information missing?**

- The dataset contains **one corrupted value**: `SLP` for **2009 Week 50 is the spreadsheet error string `#DIV/0!`**. This is why `SLP` is imported as character rather than numeric, and it leaves one effectively-missing sea-level-pressure observation. It is not encoded as `NA`, so naïve summaries that assume a numeric column will fail silently.  
- **Weeks 37–38 of 2013 are absent** (interior gap, noted above).

**Are there any known errors, sources of noise, or redundancies?**

- **Case counts** reflect *notified* dengue cases, not total incidence. Undiagnosed or self-managed cases — particularly mild febrile illness — are not captured (see Limitations, Section 7).  
- **Climate variables** represent a single point/station observation of undocumented location; spatial variation across the Colombo district is not captured.  
- `TMAX`, `Tm`, and `TEM` are correlated by construction. Any downstream model that uses all three should account for the resulting multicollinearity (e.g., via regularisation or feature selection). The current tutorial does not train a multi-feature supervised forecaster on these variables.  
- The `SLP` corruption above is a concrete data-quality error.

**Does the dataset contain data that might be considered sensitive?**

No. Case counts are aggregate weekly totals; no individual-level health data, patient identifiers, or demographic breakdowns are present.

---

## 3\. Collection Process

**How was the data associated with each instance acquired?**

*Case data:* Dengue is a notifiable disease in Sri Lanka. Clinicians and laboratories report suspected and confirmed cases to the Epidemiology Unit, Ministry of Health, which aggregates them and publishes Weekly Epidemiological Reports. During this period, the great majority of "cases" were **suspected cases** diagnosed on clinical/syndromic criteria (consistent with the WHO 2009 classification: dengue with or without warning signs, and severe dengue); laboratory/virological confirmation was limited, especially outside the Western Province.

*Climate data:* **The specific weather station and data source are not documented in the `colmozzie` package.**

> **Correction to a common misattribution:** These data should **not** be described as recorded at "Bandaranaike International Airport." That airport is at Katunayake, a suburb of Negombo in **Gampaha district**, roughly 32 km north of Colombo — a different district from the one the case counts describe. The package makes no claim about which station the climate data come from.

**Over what timeframe was the data collected?**

Week 1, 2009 through Week 21, 2014 — approximately 5.4 years of weekly observation (with the interior 2013 W37–38 gap noted above).

**Were any ethical review processes conducted?**

Aggregate, non-identifiable surveillance data of this nature is typically exempt from individual ethics review. Routine public-health surveillance operates under national public-health law in Sri Lanka. No individual consent was required or applicable.

**Did the dataset creators observe the phenomenon directly, or indirectly?**

Indirectly. Case counts are administrative records generated by the health system's reporting infrastructure. Their accuracy depends on healthcare-seeking behaviour, diagnostic capacity, and reporting compliance — all of which vary over time and across subpopulations.

---

## 4\. Preprocessing, Cleaning, and Labeling

**Was any preprocessing applied to the raw data before creating the dataset?**

The `colmozzie` package presents the data with minimal documented preprocessing. No imputation of missing values is documented. The `#DIV/0!` value in `SLP` (2009 W50) should be handled explicitly (coerce to `NA`) before analysis.

**Quantities derived in this tutorial (not part of the source dataset):**

The tutorial derives the following from the case and temperature series; none are columns of the source data:

- **Generation-interval (GI) model.** A temperature-dependent mean generation interval, `GI(T) = IIP + EIP(T)`, with a fixed intrinsic incubation period (IIP ≈ 5.9 days) and a temperature-dependent extrinsic incubation period (EIP) interpolated between literature anchors (≈15 days at 25 °C, ≈6.5 days at 30 °C). Across the observed temperature range this yields a GI of roughly 12–21 days. This climate-adjusted GI is contrasted against a single **fixed** GI (\~2 weeks) of the kind a non-specialist web search would return. Sources: Chan & Johansson (2012) for the incubation-period anchors; Codeço et al. (2018) for the temperature-dependent generation-interval framing.  
- **Effective reproduction number (Rt).** Estimated with a Cori et al. (2013) posterior-mean estimator (Gamma prior on R with mean 2 and sd 2; a 2-week sliding window), computed **identically** for the fixed and the climate-adjusted GI so that the generation interval is the only thing that differs between the two arms.  
- **Outbreak-alert decision.** A binary alert defined as **sustained Rt \> 1 for ≥ 2 consecutive weeks**, evaluated separately for each GI arm. The tutorial's headline result is the count of week-instances in which this alert decision *flips* between the fixed and climate-adjusted GI.

>   
> **Generation-interval requirement.** `EpiEstim::estimate_R` assumes a single fixed serial/generation interval for the whole series and cannot represent a time-varying interval; the tutorial therefore applies the Cori estimator directly with a per-week generation interval. A dengue generation interval is long relative to directly transmitted respiratory viruses because transmission passes through the mosquito (intrinsic plus extrinsic incubation). Empirically, successive dengue illnesses cluster most strongly at a **15–17 day** interval, and the extrinsic component is strongly **temperature-dependent** (Chan & Johansson, 2012). Using a single fixed interval rather than a temperature-dependent one is precisely the simplification this tutorial examines: a substantially shorter interval (of the kind used for respiratory viruses) would systematically bias the Rt estimates.  
> *\[Note: The 15-17 cluster-window is used as a GI substitute for educational purposes only.\]*

**Was the "gold standard" for training computed from the data itself?**

Yes. Both the Rt estimate and the outbreak-alert decision are derived from the case series rather than from an independent clinical or serological reference. This introduces circularity:

- Rt is estimated from case counts using a parametric generation interval, so errors in case ascertainment propagate directly into Rt.  
- The alert decision is a deterministic function of Rt and therefore inherits the same surveillance noise.

---

## 5\. Uses

**What tasks has the dataset been used for?**

- Retrospective analysis of climate–dengue associations in Colombo  
- Exploratory time-series analysis (seasonal decomposition of the case and climate series)  
- Effective reproduction number (Rt) estimation, comparing a **fixed** versus a **temperature-dependent (climate-adjusted)** generation interval  
- Demonstration of retrieval-augmented (RAG) selection of an epidemiological parameter — the generation interval — from the primary literature, versus a single decontextualised value  
- Demonstration of an LLM-as-a-judge step for biological-plausibility validation of model outputs

**Is there anything about the composition or collection that might affect future uses?**

1. **Single district, single serotype era.** The data covers the Colombo district only and spans an epidemiological period whose serotype mix and immune landscape differ from subsequent years (see Section 7).  
2. **Training temporal boundary.** The dataset ends in mid-2014. Any model trained on it is retrospective to 2014 and has not been validated on post-2014 outbreaks, including the major 2017 and 2019 events.  
3. **No demographic or serotype stratification.** Age-specific attack rates, DENV serotype circulation, and immune status are absent. Models cannot learn the serotype-switching dynamics that drive inter-annual outbreak severity.

**Are there tasks for which the dataset should not be used?**

- **Operational real-time surveillance.** The dataset is a static historical archive and cannot support live monitoring without current data integration.  
- **Policy-grade outbreak prediction.** The analysis in this tutorial is explicitly a research and educational demonstration and has not been validated prospectively.  
- **Generalisation to other geographies or diseases** without retraining and local validation.

---

## 6\. Distribution

**How is the dataset distributed?**

- From **CRAN**: `install.packages("colmozzie")` (canonical page: [https://CRAN.R-project.org/package=colmozzie](https://CRAN.R-project.org/package=colmozzie)).  
- From the source repository on **GitHub** (`thiyangt/colmozzie`), via `devtools::install_github("thiyangt/colmozzie")`. This tutorial reads the weekly series directly from the repository's `data-raw/dengColombo.csv`.

**Will the dataset be updated?**

The packaged data covers 2009–2014 only and has not been extended with post-2014 data; no mechanism for versioned data updates is described by the maintainer. Consult the CRAN page for the current package version and publication date.

---

## 7\. Limitations of the Surveillance Data

This section documents limitations that users must understand before drawing epidemiological conclusions from model outputs. These limitations are structural properties of passive disease surveillance systems and are not unique to Sri Lanka.

### 7.1 Underreporting

**Nature of the problem:** `dengColombo` records *notified* cases at health facilities, not total disease incidence. A substantial fraction of dengue infections — particularly mild or asymptomatic cases — are never diagnosed or reported. The national surveillance analysis of this period notes that outpatient and private-sector cases are underrepresented and that clinically inapparent infections are not counted

**Specific implications for this dataset:**

- The **case series is a lower bound on true incidence**. The analysis characterises surveillance output, not biological transmission intensity.  
- **Underreporting is unlikely to be constant over time.** Public-awareness campaigns (e.g., following major outbreaks), changes in diagnostic testing availability, and expansion of reporting networks all alter the reporting fraction independently of transmission. Estimates calibrated during a period of low reporting intensity will misstate risk if surveillance intensity changes, and vice versa.  
- **Spatial aggregation masks within-district heterogeneity.** High-density urban wards with better healthcare access contribute disproportionately to reported counts, creating systematic geographic bias.  
- **The outbreak-alert decision** (sustained Rt \> 1\) is derived from the same reported counts, so periods of changing reporting intensity can move the alert independently of transmission.

**Modelling consequence:** The Rt estimates derived from these case counts are estimates of the *apparent* reproduction number — the rate at which reported cases reproduce — not the true epidemiological R. During periods of changing reporting intensity, Rt will exhibit artefactual trends unrelated to transmission biology.

### 7.2 Health System Disruptions and Case Ascertainment

**Nature of the problem:** Case ascertainment depends on a functioning healthcare pathway: a patient must seek care, a clinician must recognise dengue, and the case must be reported. Any disruption reduces reported counts without reducing transmission.

**Known disruptions relevant to the 2009–2014 period:**

- **Healthcare capacity saturation.** During outbreak peaks (the maximum in this series is 475 cases/week), hospitals may be overwhelmed, reducing diagnostic throughput and delaying or omitting reports. The highest-incidence weeks may therefore be *systematically underreported* relative to endemic-period weeks, attenuating the true amplitude of outbreaks in the case series.  
- **Seasonal access barriers.** The southwest monsoon (roughly May–September) and northeast monsoon (roughly October–January) can reduce mobility and clinic attendance in peri-urban areas, introducing correlated seasonal measurement error in case counts that partially mirrors the seasonal climate signal.  
- **Reporting lag and revision.** Individual facility reports may arrive with variable delays, and weekly aggregates can be revised. The dataset as distributed is a static snapshot without documented revision history.

**What the dataset cannot tell you:** The dataset provides no denominator information (healthcare-seeking population, testing volume, diagnostic positivity), making it impossible to compute a case-detection rate or to distinguish a genuine incidence decline from reduced surveillance effort.

### 7.3 What the Data Does and Does Not Capture About the 2017 and 2019 Outbreaks

**Critical limitation: the dataset ends in mid-2014 and contains no observations from 2017 or 2019\.** Any model trained exclusively on `dengColombo` has not observed these events and cannot be assumed to generalise to them without revalidation.

**The 2017 Sri Lanka dengue outbreak:**

In 2017, Sri Lanka experienced its largest recorded dengue epidemic: the highest single-year total since dengue became notifiable. In response, the Ministry of Health launched an emergency response, and WHO reported the situation through its Disease Outbreak News (WHO, 2017). Contributing factors included:

- **Serotype shift.** A new clade of **DENV-2** (Cosmopolitan genotype) became dominant after several years of DENV-1 predominance (DENV-1 was dominant in the 2009, 2010, and 2012 epidemics). A population with waning cross-protective immunity was effectively naïve to the emerging serotype, enabling explosive transmission. This mechanism is entirely outside the feature space of a model trained on 2009–2014 data.  
- **Rainfall and breeding-site amplification.** Monsoon rainfall and flooding in 2017 expanded *Aedes* breeding habitat. This is one contributing hypothesis, but it is contested as a *primary* driver: the national analysis found that changes in vector abundance were not predictive of the increased incidence and emphasised the serotype shift. Precipitation is present in this dataset, but the maximum weekly precipitation (71.3 mm) is unlikely to bracket 2017 flood-period conditions.  
- **Urban and demographic change.** Colombo's population density and settlement patterns evolved between 2014 and 2017 in ways a pre-2015 model does not reflect. Incidence was highest in the Colombo and Gampaha districts of the Western Province, and disproportionately affected schoolchildren and young adults.  
- **What a model can and cannot detect:** A model retrained with data through 2016 might partially detect rising Rt and above-threshold counts in early 2017 from climate and autoregressive signals, but would have no capacity to anticipate the serotype-driven amplification, and its performance would likely degrade as outbreak magnitude exceeded the training-period maximum.

**Implication for model validation:** Any prospective or out-of-sample evaluation of a model trained on `dengColombo` must explicitly test against post-2014 data. The 2017 outbreak in particular constitutes a genuine distributional shift (serotype change, demographic and reporting changes) that would stress-test the model's extrapolation behaviour. This tutorial's temperature-dependent generation-interval analysis illustrates sensitivity to climate, but cannot substitute for real prospective validation against post-2014 surveillance records.

### 7.4 Absence of Serological, Vector, and Socioeconomic Data

The dataset captures climate and case counts only. The following known drivers of dengue transmission are not represented:

- **Serotype circulation proportions** — which DENV serotypes (1–4) circulate, and in what proportions, determines population-level susceptibility and outbreak severity.  
- **Aedes aegypti / albopictus abundance and distribution** — entomological surveillance (larval indices, adult trap counts) is not included.  
- **Population immunity (seroprevalence)** — the fraction immune to each serotype determines effective transmission potential.  
- **Socioeconomic and land-use variables** — household water storage, urban greenspace, and settlement density affect breeding-site availability independently of rainfall.  
- **Healthcare access and testing volume** — variation in testing intensity affects the reporting fraction (Section 7.1).

Models trained on this dataset absorb all unexplained variance attributable to these omitted factors into the residual error term. Any apparent reliance on lagged autoregressive signal (e.g., recent case history) reflects the information content of epidemic momentum relative to climate features — but also the omission of serological and vector data that would provide independent signal.

---

## 8\. Maintenance

**Who is responsible for maintaining the dataset?**

The `colmozzie` R package is maintained by Thiyanga S. Talagala. The underlying case data are maintained by the Epidemiology Unit, Ministry of Health, Sri Lanka. This tutorial uses the dataset in a static, read-only capacity.

**Will the dataset be updated, corrected, or extended?**

No mechanism for update or correction of the data is documented in the `colmozzie` package. Researchers requiring post-2014 data should consult the Epidemiology Unit's Weekly Epidemiological Reports directly, or resources such as the `denguedatahub` R package and WHO SEARO dengue archives.

**Is there a mechanism for users to flag errors?**

For errors in the R package, issues may be filed on the `colmozzie` GitHub repository. For errors in how the dataset is used in this tutorial, refer to the tutorial's own repository issue tracker.

---

## References

- Gebru, T., Morgenstern, J., Vecchione, B., Vaughan, J. W., Wallach, H., Daumé III, H., & Crawford, K. (2018). Datasheets for datasets. *arXiv:1803.09010*. (Published: *Communications of the ACM*, 2021, 64(12), 86–92.)  
- Talagala, T. S. *colmozzie: Dengue Cases and Climate Variables in Colombo Sri Lanka* (R package; licence CC0). CRAN: [https://CRAN.R-project.org/package=colmozzie](https://CRAN.R-project.org/package=colmozzie) ; source: [https://github.com/thiyangt/colmozzie](https://github.com/thiyangt/colmozzie)  
- Epidemiology Unit, Ministry of Health, Sri Lanka. *Weekly Epidemiological Reports*. [https://www.epid.gov.lk](https://www.epid.gov.lk)  
- WHO (2017). *Dengue – Sri Lanka.* Disease Outbreak News, 19 July 2017\. [https://www.who.int/emergencies/disease-outbreak-news/item/19-july-2017-dengue-sri-lanka-en](https://www.who.int/emergencies/disease-outbreak-news/item/19-july-2017-dengue-sri-lanka-en)  
- WHO (2009). *Dengue: Guidelines for Diagnosis, Treatment, Prevention and Control* (new edition). Geneva: World Health Organization.

---

