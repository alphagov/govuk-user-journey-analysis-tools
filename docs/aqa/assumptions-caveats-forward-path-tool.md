# Assumptions and caveats log

This log contains a list of assumptions and caveats used in the Forward Path tool analysis.

## Definitions

Assumptions are RAG-rated according to the following definitions for quality and impact<sup>1</sup>:

<!-- Using reStructuredText table here, otherwise the raw Markdown is greater than the 120-character line width -->
```{eval-rst}
+-------+------------------------------------------------------+-------------------------------------------------------+
| RAG   | Assumption quality                                   | Assumption impact                                     |
+=======+======================================================+=======================================================+
| GREEN | Reliable assumption, well understood and/or          | Marginal assumptions; their changes have no or        |
|       | documented; anything up to a validated & recent set  | limited impact on the outputs.                        |
|       | of actual data.                                      |                                                       |
+-------+------------------------------------------------------+-------------------------------------------------------+
| AMBER | Some evidence to support the assumption; may vary    | Assumptions with a relevant, even if not critical,    |
|       | from a source with poor methodology to a good source | impact on the outputs.                                |
|       | that is a few years old.                             |                                                       |
+-------+------------------------------------------------------+-------------------------------------------------------+
| RED   | Little evidence to support the assumption; may vary  | Core assumptions of the analysis; the output would be |
|       | from an opinion to a limited data source with poor   | drastically affected by their change.                 |
|       | methodology.                                         |                                                       |
+-------+------------------------------------------------------+-------------------------------------------------------+
```
<sup><sup>1</sup> With thanks to the Home Office Analytical Quality Assurance team for these definitions.</sup>

## Assumptions and caveats

The log contains the following assumptions and caveats:

### Assumption 1: Only exact matches to `DESIRED_PAGE` are currently supported.

* **Quality**: GREEN
* **Impact**: AMBER

The query parameter for `DESIRED_PAGE` cannot evaluate the field using regular expression, and therefore only exact matches are currently supported. This is acceptable as users of these tools are accustomed to providing exact matches for analyses.

### Assumption 2: Previous visits to `DESIRED_PAGE` are ignored, only the last visit is used.

* **Quality**: GREEN
* **Impact**: AMBER

The subsetted journey considers the last visit to the `DESIRED_PAGE` as the goal location (i.e. the first step). Therefore, any previous visits to the `DESIRED_PAGE` are ignored. This was decided as the main aim of the tool is to understand which pages are visited following the `DESIRED_PAGE`. However, it is important that the user of the tool is aware of this assumption, as it will impact the subsetted journey output.

### Assumption 3: If `REMOVE_DESIRED_PAGE_REFRESHES` is `TRUE`, only the first visit in a series of sequential visits (page refreshes) to `DESIRED_PAGE` are used to determine which is the last visit.

* **Quality**: GREEN
* **Impact**: GREEN

Therefore, if TRUE, it will only use the first visit in a series of sequential visits to `DESIRED_PAGE` of hit type PAGE. Other earlier visits to `DESIRED_PAGE` will remain, as will any earlier desired page refreshes.

### Assumption 4: Journeys shorter than the number of desired stages (`NUMBER_OF_STAGES`) are always included.

* **Quality**: GREEN
* **Impact**: AMBER

While journeys shorter than the number of desired stages are always included, journeys longer than the number of desired stages will not be accurately represented. For example, if `NUMBER_OF_STAGES` = 2, and the journey consists of 3 stages, then the user of the tool will not be provided with the full journey (i.e. the 3rd page path). Therefore, this journey will be amalgamated with other journeys that consist of the same 2 page paths (`NUMBER_OF_STAGES = 2`), even if further page paths differ.

### Assumption 5: GOV.UK search page paths are assumed to have the format /search/{TYPE}?keywords={KEYWORDS}{...}, where {TYPE} is the GOV.UK search content type, {KEYWORDS} are the search keywords, where each keyword is separated by +, and {...} are any other parts of the search query that are not keyword-related (if they exist).

* **Quality**: GREEN
* **Impact**: GREEN

### Assumption 6: GOV.UK search page titles are assumed to have the format {KEYWORDS} - {TYPE} - GOV.UK, where {TYPE} is the GOV.UK search content type, and {KEYWORDS} are the search keywords.

* **Quality**: GREEN
* **Impact**: GREEN

### Assumption 7: If `ENTRANCE_PAGE` is FALSE, each journey contains both instances where the entrance page is included, and the entrance page is not included.

* **Quality**: GREEN
* **Impact**: RED

Therefore, if `ENTRANCE_PAGE` is TRUE, these two instances (where the entrance page is included vs when the entrance page is not included) will be considered two separate journeys. This is a truer representation of the journey, as a TRUE flag indicates that the journey had more page paths than `NUMBER_OF_STAGES`. The user must have a good understanding of what the `ENTRANCE_FLAG` represents, as this could drastically change the output.

### Assumption 8: If `DEVICE_ALL` is selected in combination with either `DEVICE_DESKTOP`, `DEVICE_MOBILE`, and/or `DEVICE_TABLET`, then the analysis will use `DEVICE_ALL` and ignore all other arguments.

* **Quality**: GREEN
* **Impact**: RED

Be default, `DEVICE_ALL` argument will be implemented over `DEVICE_DESKTOP`, `DEVICE_MOBILE`, and `DEVICE_TABLET`. Therefore, if the user accidentally selects `DEVICE_ALL`, the query will ignore the desired arguments `DEVICE_DESKTOP`, `DEVICE_MOBILE`, and/or `DEVICE_TABLET`. This will drastically change the expected output, as `DEVICE_ALL` will split up journeys undertaken on a desktop, mobile, and tablet device. The output CSV file flags which device category(ies) were used, which should mitigate errors related to interpreting the data.
