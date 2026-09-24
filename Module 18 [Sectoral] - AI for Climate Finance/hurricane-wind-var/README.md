# Estimating Hurricane Wind Value-at-Risk from an AI Weather Ensemble

Hurricanes are among the costliest natural disasters on Earth, and the financial institutions that insure homes, hold mortgages, or invest in coastal regions need forward-looking, quantified estimates of the losses a storm might cause — before it makes landfall, sometimes before it even has a name.

In this tutorial you will turn an ensemble of AI-generated hurricane forecasts (Google's experimental WeatherNext cyclone model, 50 members, for the system that became Hurricane Helene, 2024) into a county-level Climate Value-at-Risk for single-family-home wind damage across Florida, Georgia, South Carolina, and North Carolina.

We follow the standard catastrophe-modeling chain — hazard → exposure → vulnerability → loss — running it once per ensemble member to build a distribution of possible losses per county, then reading a percentile off that distribution: the Value-at-Risk.

Author:
- Tristan Ballard, PhD | Zeus AI

## Access this tutorial

We recommend executing this notebook in a Colab environment to gain access to GPUs and to manage all necessary dependencies. 

<a target="_blank" href="https://colab.research.google.com/github/climatechange-ai-tutorials/hurricane-wind-var/blob/main/Hurricane_Wind_VaR.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

## Contribute to this tutorial

Please refer to these [GitHub instructions](https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project#about-forking) to open a pull request via the "fork and pull request" workflow.

Pull requests will be reviewed by members of the Climate Change AI Tutorials team for relevance, accuracy, and conciseness.

## Climate Change AI Tutorials
Check out the [tutorials page](https://www.climatechange.ai/tutorials?) on our website for a full list of tutorials demonstrating how AI can be used to tackle problems related to climate change.

## License
Usage of this tutorial is subject to the MIT License.

## Cite

### Plain Text
Ballard, T. (2026). Estimating Hurricane Wind Value-at-Risk from an AI Weather Ensemble [Tutorial]. In Climate Change AI Summer School. Climate Change AI. https://doi.org/10.5281/zenodo.21828317

### BibTeX

```
@misc{ballard2026hurricane,
  title={Estimating Hurricane Wind Value-at-Risk from an AI Weather Ensemble},
  author={Ballard, Tristan},
  year={2026},
  organization={Climate Change AI},
  type={Tutorial},
  doi={https://doi.org/10.5281/zenodo.21828317},
  booktitle={Climate Change AI Summer School},
  howpublished={\url{https://github.com/climatechange-ai-tutorials/hurricane-wind-var}}
}
```
