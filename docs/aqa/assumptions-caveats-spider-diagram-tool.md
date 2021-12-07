# Assumptions and caveats log

This log contains a list of assumptions and caveats used in the spider diagram tool analysis.

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

### Assumption 1: Prioritise visualisation by aggregating all pages that have less than 2.5% of sessions to `(other)`

* **Quality**: GREEN (for visualisation purposes)
* **Impact**: GREEN (for visualisation purposes)

Pages that contain less than 2.5% of overall sessions are difficult to see in the diagram both in terms of their
volume, and any associated labels.

To mitigate this, all pages with less than 2.5% of overall sessions are aggregated/binned together into a separate
category `(other)`. This happens immediately after the SQL queries have been executed, but before the visualisations
and outputs have been rendered.

As this is **strictly for visualisation purposes**, it is acceptable. However, any downstream analysis of the outputs
is obviously limited due to this aggregation. As such, **outputs of this tool should not be used for further
quantitative analysis** without a thorough understanding of this assumption's implications.

### Assumption 2: URL query parameters and anchors are excluded from page paths

* **Quality**: GREEN
* **Impact**: GREEN

All URL query parameters and anchors have been removed from page paths so that page views are associated with the
general page path URL, rather than specific query parameters and anchors. The URL parameters and anchors are removed
during SQL execution.

The URL parameters and anchors are removed as the overall aim of the tool is to provide an understanding of which page
paths have been viewed, regardless of query parameters and anchors. This is in line with Google Analytics, which also
excludes query parameters and anchors from the page path.
