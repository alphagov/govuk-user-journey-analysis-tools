# `govuk-user-journey-analysis-tools`

Data analysis pipelines to investigate distinct user journey behaviour across GOV.UK:
1. Spider diagram tool

    Visualisation displaying entry and exit data of a [GOV.UK][govuk] page of interest, over a date range and device category(ies). This data is broken down further by internal/external links, and the individual entry/exit pages paired with the count and proportion of page views. Answers the question, *'In regards to page X, which page have users come from, and which page do they go to next?'*

2. Reverse path tool

   A CSV file presenting the *previous* page paths that reached a [GOV.UK][govuk] page of interest, over a date range and device category(ies). The count and proportion of sessions visiting distinct, subsetted journeys are compiled together, and returned as a sorted list in descending order. Answers the question, *'What journeys have users gone on to arrive at page X?'*

3. Forward path tool

  A CSV file presenting the *following* page paths that reached a [GOV.UK][govuk] page of interest., over a date range and device category(ies). The count and proportion of sessions visiting distinct, subsetted journeys are compiled together, and returned as a sorted list in descending order. Answers the question, *'What journeys do users go on to following page X?'*


## Getting started

> ⚠️ **This repository is for version control purposes only**. You are expected to run the notebooks in
> [Google Colab][google-colab]! For further information, see the [Background](#background) section.

To run the tools, make sure you meet the [requirements](#requirements) first, and then follow the tool's README instructions detailed in [here][user-guide].


### Requirements

The following are the minimum requirements to use all tools:

- Access to [Google Colab][google-colab]
- Access rights to your Google BigQuery dataset of choice

If you would like to contribute to this project, see the [Contributing](#contributing) section.

### Background

[Google Colab][google-colab] is a new research project from Google, which allows you to run Jupyter notebooks in a
cloud environment at no extra cost. [Jupyter Notebook][jupyter] in turn is an open-source web application that allows
for the creation of documents with live code, which can be run to generate results on-the-fly. Data scientists at GDS
are regular uses of Jupyter notebooks, as they can use them to clean data, test out new ideas and fine tune existing
models.

## Licence

Unless stated otherwise, the codebase is released under the MIT License. This covers
both the codebase and any sample code in the documentation. The documentation is ©
Crown copyright and available under the terms of the Open Government 3.0 licence.

## Contributing

If you want to help us build, and improve these tools, view our [contributing guidelines][contributing].

## Acknowledgements

This project structure is based on the [`govcookiecutter`][govcookiecutter] template project.


[contributing]: ./CONTRIBUTING.md
[google-colab]: https://colab.research.google.com/notebooks/welcome.ipynb
[govcookiecutter]: https://github.com/ukgovdatascience/govcookiecutter
[govuk]: https://www.gov.uk/
[jupyter]: https://jupyter.org/
[user-guide]: ./docs/user_guide/
