# Changing Course: What Australians Choose to Study

FIT3179 Data Visualisation 2 — a single scrolling web page built with Vega-Lite.
Topic: University Course Preferences in Australia.

Author: Gan Jia Hui · October 2026

## Folder structure

```
index.html          the web page (short text + the 11 charts, loaded at the bottom with vegaEmbed)
css/style.css       layout grid, typography and colours
js/                 one Vega-Lite JSON specification per chart (01 … 11)
data/               the CSV tables each chart reads, plus the map outline
data/source/        the three original Excel files from the Department of Education (unchanged)
```

## The 11 charts

| # | Section | File | Idiom | Data table |
|---|---------|------|-------|------------|
| 1 | Fields of Study Today | js/01_students_by_field_waffle.vl.json | Waffle chart (small multiples) | Table 2 |
| 2 | Fields of Study Today | js/02_domestic_international_stacked.vl.json | Proportional stacked bar | Tables 2 + 4 |
| 3 | Fields of Study Today | js/03_city_regional_spine.vl.json | Spine chart | A6 |
| 4 | Changing Interests | js/04_enrolments_small_multiples.vl.json | Line chart (small multiples) | Table 2 |
| 5 | Changing Interests | js/05_applicant_rank_bump.vl.json | Bump chart | A4.1 |
| 6 | Changing Interests | js/06_enrolment_change_heatmap.vl.json | Heat map | Table 2 |
| 7 | Fastest-Growing Fields | js/07_enrolment_slope.vl.json | Slope graph | Table 2 |
| 8 | Fastest-Growing Fields | js/08_applicant_change_diverging.vl.json | Diverging bar chart | A4.1 |
| 9 | Across Australia | js/09_field_share_choropleth.vl.json | Choropleth map (with field menu) | Table 2.10 |
| 10 | Across Australia | js/10_state_dorling_cartogram.vl.json | Dorling cartogram (scaled cartogram) | Table 2.10 |
| 11 | Across Australia | js/11_interstate_flow_map.vl.json | Flow map (with state menu) | Table 2.4 |

Maps use a conic equal-area projection centred on Australia (standard parallels 18°S and 36°S).

## Data

| CSV in `data/` | Copied from (Excel file → sheet) |
|----------------|----------------------------------|
| A4-1_applications_offers_by_field.csv | Undergraduate_Applications_and_Offers_2025_Appendices.xlsx → Tables A4.1 and A4.2 (A4.1 only) |
| A6_applications_offers_by_region_and_field.csv | Undergraduate_Applications_and_Offers_2025_Appendices.xlsx → Table A6 |
| T2_all_student_enrolments.csv | 2024_Summary_Timeseries.xlsx → 2 |
| T4_domestic_student_enrolments.csv | 2024_Summary_Timeseries.xlsx → 4 |
| 2-4_home_state_vs_study_state.csv | 2024_Section2_All_Students.xlsx → 2.4 |
| 2-10_students_by_university_and_field.csv | 2024_Section2_All_Students.xlsx → 2.10 |
| australia_states.topo.json | State boundaries (ABS ASGS via github.com/rowanhogan/australian-states), simplified with mapshaper |

Each CSV is a straight copy of one table. No numbers were changed and no tables were merged.
Only the changes needed to save a table as CSV were made:

- the title line, the "Back to contents" link and the footnotes were removed, so the column headings are on the first row;
- **Tables A4.1 and A6** have two heading rows (e.g. Applicants / Offers above the years, or Metropolitan /
  Non-Metropolitan above Applicants), so the two heading rows are joined into one, e.g. `Applicants 2010`
  or `Non-Metropolitan Applicants`.

All calculations (shares, ranks, growth rates, offer rates) happen inside the chart specifications.
Values shown as `np` (not published) or `< 5` in the original tables are kept as they are and treated as missing.
Table A6 stores applicant counts with decimals; they are kept exactly as published.

Sources:

1. Department of Education (2026). Undergraduate Applications and Offers 2025 — Appendices. CC BY 4.0.
   https://www.education.gov.au/undergraduate-applications-offers-and-acceptances-publications
2. Department of Education (2025). Selected Higher Education Statistics — 2024 Student data.
   https://www.education.gov.au/higher-education-statistics/student-data/selected-higher-education-statistics-2024-student-data
