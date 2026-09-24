# Detecting Deforestation from Satellite Image Time Series

A hands-on tutorial for the Climate Change AI Virtual Summer School 2026, AI for Forestry module.

Participants learn to detect tropical deforestation by treating each ground location as a time series of a vegetation index (NDVI) across one year, and training models to tell stable forest, freshly deforested, and old clearing trajectories apart. The workflow uses real Sentinel-2 imagery and official INPE PRODES deforestation labels over an active frontier in the Brazilian Amazon, then extends to AlphaEarth foundation-model embeddings (Google's Satellite Embedding dataset) read by a small time series Transformer.

Author:
- Eduardo Ulises Moya-Sanchez, ulises.moya@iieg.gob.mx

## Access this tutorial

We recommend executing this notebook in a Colab environment to gain access to GPUs and to manage all necessary dependencies. 

<a target="_blank" href="https://colab.research.google.com/github/climatechange-ai-tutorials/detect-deforestation/blob/main/detect_deforestation_time_series.ipynb">
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
Moya-Sanchez, E.U. (2026). Detecting Deforestation from Satellite Image Time Series [Tutorial]. In Climate Change AI Summer School. Climate Change AI. https://doi.org/10.5281/zenodo.21613534

### BibTeX

```
@misc{moya2026deforestation,
  title={Detecting Deforestation from Satellite Image Time Series},
  author={Moya-Sanchez, Eduardo Ulises},
  year={2026},
  organization={Climate Change AI},
  type={Tutorial},
  doi={https://doi.org/10.5281/zenodo.21613534},
  booktitle={Climate Change AI Summer School},
  howpublished={\url{https://github.com/climatechange-ai-tutorials/detect-deforestation}}
}
```
