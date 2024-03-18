
## addindicators

<!-- badges: start -->

[![Contributor
Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](code_of_conduct.md)
[![R-CMD-check](https://github.com/impact-initiatives/impactR4PHU/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/impact-initiatives/impactR4PHU/actions/workflows/R-CMD-check.yaml)
[![Codecov test
coverage](https://codecov.io/gh//branch/main/graph/badge.svg)](https://app.codecov.io/gh/?branch=main)
<!-- badges: end -->

## Overview

`impactR4PHU` is designed for creating quality check reports, cleaning,
analysing and outputing results of core outcome indicators of Public
Health Unit. This package will target mainly Food Security and
Livelihoods, WASH, Nutrition and Health Sectors.

## Installation

You can install the development version from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("impact-initiatives/impactR4PHU")
```

## Examples

``` r
library(impactR4PHU)
df <- impactR4PHU_data_template
```

### Example:: Add Food Consumption Score (FCS)

``` r
df_with_fcs <- df %>% add_fcs(
  cutoffs = "normal",
  fsl_fcs_cereal = "fsl_fcs_cereal",
  fsl_fcs_legumes = "fsl_fcs_legumes",
  fsl_fcs_veg = "fsl_fcs_veg",
  fsl_fcs_fruit = "fsl_fcs_fruit",
  fsl_fcs_meat = "fsl_fcs_meat",
  fsl_fcs_dairy = "fsl_fcs_dairy",
  fsl_fcs_sugar = "fsl_fcs_sugar",
  fsl_fcs_oil = "fsl_fcs_oil"
)
df_with_fcs %>%
  dplyr::select(
    uuid, fsl_fcs_score, fsl_fcs_cat, fcs_weight_cereal1, fcs_weight_legume2,
    fcs_weight_dairy3, fcs_weight_meat4, fcs_weight_veg5,
    fcs_weight_fruit6, fcs_weight_oil7, fcs_weight_sugar8
  ) %>%
  head(20)
```

    ## # A tibble: 20 × 11
    ##    uuid          fsl_fcs_score fsl_fcs_cat fcs_weight_cereal1 fcs_weight_legume2
    ##    <chr>                 <dbl> <chr>                    <dbl>              <dbl>
    ##  1 eaf540cd-32b…          48.5 Acceptable                   0                  0
    ##  2 89e706c3-53d…          50.5 Acceptable                   4                  6
    ##  3 afd921c6-e54…          46.5 Acceptable                   8                  0
    ##  4 d8b05f39-ba8…          42.5 Acceptable                  14                  3
    ##  5 d6b42f9e-c20…          55.5 Acceptable                   6                  6
    ##  6 f1b9ec67-20d…          37.5 Acceptable                   0                  6
    ##  7 95ea286d-ae8…          50.5 Acceptable                   4                 15
    ##  8 85b4a96f-cea…          31.5 Borderline                   0                 15
    ##  9 ef13a764-0af…          49.5 Acceptable                  14                  0
    ## 10 1a69e87b-ec6…          52.5 Acceptable                   8                 12
    ## 11 5613d0fe-34d…          69   Acceptable                  12                  3
    ## 12 091aef7d-2b3…          34   Borderline                   4                  0
    ## 13 e21a34f5-1a4…          36   Acceptable                   0                  6
    ## 14 42dc8573-e2d…          39   Acceptable                  14                  3
    ## 15 3a180db5-d12…          47   Acceptable                  10                  9
    ## 16 789a632b-53d…          46.5 Acceptable                   4                  9
    ## 17 cd41675b-eb4…          61.5 Acceptable                  14                 18
    ## 18 f741c29d-b7c…          77   Acceptable                  10                 12
    ## 19 2516eba7-789…          76.5 Acceptable                   2                 15
    ## 20 c7896215-b36…          20.5 Poor                         2                  3
    ## # ℹ 6 more variables: fcs_weight_dairy3 <dbl>, fcs_weight_meat4 <dbl>,
    ## #   fcs_weight_veg5 <dbl>, fcs_weight_fruit6 <dbl>, fcs_weight_oil7 <dbl>,
    ## #   fcs_weight_sugar8 <dbl>

### Example:: Add Household Hunger Scale (HHS)

``` r
df_with_hhs <- df_with_fcs %>% add_hhs(
  fsl_hhs_nofoodhh = "fsl_hhs_nofoodhh",
  fsl_hhs_nofoodhh_freq = "fsl_hhs_nofoodhh_freq",
  fsl_hhs_sleephungry = "fsl_hhs_sleephungry",
  fsl_hhs_sleephungry_freq = "fsl_hhs_sleephungry_freq",
  fsl_hhs_alldaynight = "fsl_hhs_alldaynight",
  fsl_hhs_alldaynight_freq = "fsl_hhs_alldaynight_freq",
  yes_answer = "yes",
  no_answer = "no",
  rarely_answer = "rarely",
  sometimes_answer = "sometimes",
  often_answer = "often"
)
df_with_hhs %>%
  dplyr::select(
    uuid, fsl_hhs_comp1, fsl_hhs_comp2, fsl_hhs_comp3,
    fsl_hhs_score, fsl_hhs_cat_ipc, fsl_hhs_cat, hh_size
  ) %>%
  head(20)
```

    ##                                        uuid fsl_hhs_comp1 fsl_hhs_comp2
    ## 1  eaf540cd-32bd-41474b-b4beb5-d62fc987e45a             0             0
    ## 2  89e706c3-53d8-4a4049-898586-4926085db71e             1             0
    ## 3  afd921c6-e54a-4c4740-919c93-87f59bd0e63a             0             2
    ## 4  d8b05f39-ba85-494c4d-808c84-9dc57823a4f1             0             0
    ## 5  d6b42f9e-c209-4c4541-808a81-86bea53df142             0             0
    ## 6  f1b9ec67-20db-47404d-a3ada0-1a37e5c49d02             1             0
    ## 7  95ea286d-ae86-47404a-828487-feba6d1503c9             0             0
    ## 8  85b4a96f-cea2-4f4b48-9d929f-5d76892f31b0             0             0
    ## 9  ef13a764-0af7-4f494c-838b88-6cb31a50842e             1             0
    ## 10 1a69e87b-ec61-4e4a40-8f868a-fe24c6a705bd             1             1
    ## 11 5613d0fe-34dc-474c43-b4b0bd-36a4c8edf902             0             0
    ## 12 091aef7d-2b31-4f4741-a5a8af-36e8f1bd075a             0             2
    ## 13 e21a34f5-1a46-42404b-b7b6be-7bc9286d0f13             1             0
    ## 14 42dc8573-e2d0-43484b-aaada2-c37ef865d041             0             0
    ## 15 3a180db5-d126-4d4b49-808d88-b3e5c71d908f             1             1
    ## 16 789a632b-53da-4c4f40-a0a1ad-f53ca2e9074b             0             0
    ## 17 cd41675b-eb48-444e4f-b8b7b3-1e493cb02f5a             0             0
    ## 18 f741c29d-b7c5-424a4d-94999c-6018bac9274e             0             0
    ## 19 2516eba7-789c-4c4b41-afa0ad-f0a7365bd81c             2             0
    ## 20 c7896215-b36f-40444c-aaa2af-fa4d37c6502e             1             1
    ##    fsl_hhs_comp3 fsl_hhs_score fsl_hhs_cat_ipc  fsl_hhs_cat hh_size
    ## 1              0             0            None No or Little      19
    ## 2              0             1    No or Little No or Little      21
    ## 3              0             2        Moderate     Moderate      21
    ## 4              0             0            None No or Little      23
    ## 5              0             0            None No or Little      22
    ## 6              2             3        Moderate     Moderate      19
    ## 7              0             0            None No or Little      22
    ## 8              0             0            None No or Little      17
    ## 9              1             2        Moderate     Moderate      21
    ## 10             1             3        Moderate     Moderate      19
    ## 11             0             0            None No or Little      16
    ## 12             0             2        Moderate     Moderate      17
    ## 13             0             1    No or Little No or Little      19
    ## 14             0             0            None No or Little      20
    ## 15             1             3        Moderate     Moderate      19
    ## 16             0             0            None No or Little      19
    ## 17             0             0            None No or Little      17
    ## 18             0             0            None No or Little      22
    ## 19             0             2        Moderate     Moderate      23
    ## 20             2             4          Severe       Severe      21

### Example:: Add Livelihood Coping Strategy score (LCSI)

``` r
df_with_lcsi <- df_with_hhs %>% add_lcsi(
  fsl_lcsi_stress1 = "fsl_lcsi_stress1",
  fsl_lcsi_stress2 = "fsl_lcsi_stress2",
  fsl_lcsi_stress3 = "fsl_lcsi_stress3",
  fsl_lcsi_stress4 = "fsl_lcsi_stress4",
  fsl_lcsi_crisis1 = "fsl_lcsi_crisis1",
  fsl_lcsi_crisis2 = "fsl_lcsi_crisis2",
  fsl_lcsi_crisis3 = "fsl_lcsi_crisis3",
  fsl_lcsi_emergency1 = "fsl_lcsi_emergency1",
  fsl_lcsi_emergency2 = "fsl_lcsi_emergency2",
  fsl_lcsi_emergency3 = "fsl_lcsi_emergency3",
  yes_val = "yes",
  no_val = "no_had_no_need",
  exhausted_val = "no_exhausted",
  not_applicable_val = "not_applicable"
)
df_with_lcsi %>%
  dplyr::select(uuid, fsl_lcsi_cat, fsl_lcsi_cat_exhaust, fsl_lcsi_cat_yes) %>%
  head(20)
```

    ##                                        uuid fsl_lcsi_cat fsl_lcsi_cat_exhaust
    ## 1  eaf540cd-32bd-41474b-b4beb5-d62fc987e45a    Emergency            Emergency
    ## 2  89e706c3-53d8-4a4049-898586-4926085db71e    Emergency            Emergency
    ## 3  afd921c6-e54a-4c4740-919c93-87f59bd0e63a    Emergency            Emergency
    ## 4  d8b05f39-ba85-494c4d-808c84-9dc57823a4f1    Emergency            Emergency
    ## 5  d6b42f9e-c209-4c4541-808a81-86bea53df142    Emergency            Emergency
    ## 6  f1b9ec67-20db-47404d-a3ada0-1a37e5c49d02    Emergency            Emergency
    ## 7  95ea286d-ae86-47404a-828487-feba6d1503c9    Emergency            Emergency
    ## 8  85b4a96f-cea2-4f4b48-9d929f-5d76892f31b0    Emergency               Crisis
    ## 9  ef13a764-0af7-4f494c-838b88-6cb31a50842e    Emergency            Emergency
    ## 10 1a69e87b-ec61-4e4a40-8f868a-fe24c6a705bd    Emergency            Emergency
    ## 11 5613d0fe-34dc-474c43-b4b0bd-36a4c8edf902    Emergency                 None
    ## 12 091aef7d-2b31-4f4741-a5a8af-36e8f1bd075a       Crisis               Crisis
    ## 13 e21a34f5-1a46-42404b-b7b6be-7bc9286d0f13       Crisis               Crisis
    ## 14 42dc8573-e2d0-43484b-aaada2-c37ef865d041    Emergency            Emergency
    ## 15 3a180db5-d126-4d4b49-808d88-b3e5c71d908f    Emergency                 None
    ## 16 789a632b-53da-4c4f40-a0a1ad-f53ca2e9074b    Emergency               Stress
    ## 17 cd41675b-eb48-444e4f-b8b7b3-1e493cb02f5a       Crisis               Crisis
    ## 18 f741c29d-b7c5-424a4d-94999c-6018bac9274e    Emergency            Emergency
    ## 19 2516eba7-789c-4c4b41-afa0ad-f0a7365bd81c    Emergency            Emergency
    ## 20 c7896215-b36f-40444c-aaa2af-fa4d37c6502e    Emergency               Crisis
    ##    fsl_lcsi_cat_yes
    ## 1         Emergency
    ## 2         Emergency
    ## 3            Crisis
    ## 4            Crisis
    ## 5         Emergency
    ## 6            Stress
    ## 7            Crisis
    ## 8         Emergency
    ## 9         Emergency
    ## 10        Emergency
    ## 11        Emergency
    ## 12           Crisis
    ## 13           Stress
    ## 14           Stress
    ## 15        Emergency
    ## 16        Emergency
    ## 17           Crisis
    ## 18           Crisis
    ## 19        Emergency
    ## 20        Emergency

### Example:: Add Reduced Household Coping Strategy score (rCSI)

``` r
df_with_rcsi <- df_with_lcsi %>% add_rcsi(
  fsl_rcsi_lessquality = "fsl_rcsi_lessquality",
  fsl_rcsi_borrow = "fsl_rcsi_borrow",
  fsl_rcsi_mealsize = "fsl_rcsi_mealsize",
  fsl_rcsi_mealadult = "fsl_rcsi_mealadult",
  fsl_rcsi_mealnb = "fsl_rcsi_mealnb"
)
df_with_rcsi %>%
  dplyr::select(uuid, fsl_rcsi_score, fsl_rcsi_cat) %>%
  head(20)
```

    ##                                        uuid fsl_rcsi_score fsl_rcsi_cat
    ## 1  eaf540cd-32bd-41474b-b4beb5-d62fc987e45a             34         High
    ## 2  89e706c3-53d8-4a4049-898586-4926085db71e             37         High
    ## 3  afd921c6-e54a-4c4740-919c93-87f59bd0e63a             30         High
    ## 4  d8b05f39-ba85-494c4d-808c84-9dc57823a4f1             29         High
    ## 5  d6b42f9e-c209-4c4541-808a81-86bea53df142             14       Medium
    ## 6  f1b9ec67-20db-47404d-a3ada0-1a37e5c49d02             37         High
    ## 7  95ea286d-ae86-47404a-828487-feba6d1503c9             20         High
    ## 8  85b4a96f-cea2-4f4b48-9d929f-5d76892f31b0             31         High
    ## 9  ef13a764-0af7-4f494c-838b88-6cb31a50842e             32         High
    ## 10 1a69e87b-ec61-4e4a40-8f868a-fe24c6a705bd             17       Medium
    ## 11 5613d0fe-34dc-474c43-b4b0bd-36a4c8edf902              9       Medium
    ## 12 091aef7d-2b31-4f4741-a5a8af-36e8f1bd075a              8       Medium
    ## 13 e21a34f5-1a46-42404b-b7b6be-7bc9286d0f13             35         High
    ## 14 42dc8573-e2d0-43484b-aaada2-c37ef865d041             17       Medium
    ## 15 3a180db5-d126-4d4b49-808d88-b3e5c71d908f             40         High
    ## 16 789a632b-53da-4c4f40-a0a1ad-f53ca2e9074b             31         High
    ## 17 cd41675b-eb48-444e4f-b8b7b3-1e493cb02f5a             24         High
    ## 18 f741c29d-b7c5-424a4d-94999c-6018bac9274e             15       Medium
    ## 19 2516eba7-789c-4c4b41-afa0ad-f0a7365bd81c             34         High
    ## 20 c7896215-b36f-40444c-aaa2af-fa4d37c6502e             25         High

### Example:: Add Household Dietery Diversity Score (HDDS)

``` r
df_with_hdds <- df_with_rcsi %>% add_hdds(
   fsl_hdds_cereals = "fsl_hdds_cereals",
   fsl_hdds_tubers = "fsl_hdds_tubers",
   fsl_hdds_veg = "fsl_hdds_veg",
   fsl_hdds_fruit = "fsl_hdds_fruit",
   fsl_hdds_meat = "fsl_hdds_meat",
   fsl_hdds_eggs = "fsl_hdds_eggs",
   fsl_hdds_fish = "fsl_hdds_fish",
   fsl_hdds_legumes = "fsl_hdds_legumes",
   fsl_hdds_dairy = "fsl_hdds_dairy",
   fsl_hdds_oil = "fsl_hdds_oil",
   fsl_hdds_sugar = "fsl_hdds_sugar",
   fsl_hdds_condiments = "fsl_hdds_condiments"
)
df_with_hdds %>%
  dplyr::select(uuid, fsl_hdds_score, fsl_hdds_cat) %>%
  head(20)
```

    ##                                        uuid fsl_hdds_score fsl_hdds_cat
    ## 1  eaf540cd-32bd-41474b-b4beb5-d62fc987e45a              7         High
    ## 2  89e706c3-53d8-4a4049-898586-4926085db71e              4       Medium
    ## 3  afd921c6-e54a-4c4740-919c93-87f59bd0e63a              7         High
    ## 4  d8b05f39-ba85-494c4d-808c84-9dc57823a4f1              2          Low
    ## 5  d6b42f9e-c209-4c4541-808a81-86bea53df142              6         High
    ## 6  f1b9ec67-20db-47404d-a3ada0-1a37e5c49d02              7         High
    ## 7  95ea286d-ae86-47404a-828487-feba6d1503c9              7         High
    ## 8  85b4a96f-cea2-4f4b48-9d929f-5d76892f31b0              5         High
    ## 9  ef13a764-0af7-4f494c-838b88-6cb31a50842e              6         High
    ## 10 1a69e87b-ec61-4e4a40-8f868a-fe24c6a705bd              8         High
    ## 11 5613d0fe-34dc-474c43-b4b0bd-36a4c8edf902              6         High
    ## 12 091aef7d-2b31-4f4741-a5a8af-36e8f1bd075a              5         High
    ## 13 e21a34f5-1a46-42404b-b7b6be-7bc9286d0f13              6         High
    ## 14 42dc8573-e2d0-43484b-aaada2-c37ef865d041              8         High
    ## 15 3a180db5-d126-4d4b49-808d88-b3e5c71d908f              7         High
    ## 16 789a632b-53da-4c4f40-a0a1ad-f53ca2e9074b              5         High
    ## 17 cd41675b-eb48-444e4f-b8b7b3-1e493cb02f5a              7         High
    ## 18 f741c29d-b7c5-424a4d-94999c-6018bac9274e              9         High
    ## 19 2516eba7-789c-4c4b41-afa0ad-f0a7365bd81c              8         High
    ## 20 c7896215-b36f-40444c-aaa2af-fa4d37c6502e              4       Medium

### Example:: Add Food Consumption Matrix (FCM) using FCS, RCSI, and HHS

**Notice that these functions are also pipable**

``` r
df_with_fcm_1 <- df_with_hdds %>%
  add_fcm_phase(
    fcs_column_name = "fsl_fcs_cat",
    rcsi_column_name = "fsl_rcsi_cat",
    hhs_column_name = "fsl_hhs_cat_ipc",
    fcs_categories_acceptable = "Acceptable",
    fcs_categories_poor = "Poor",
    fcs_categories_borderline = "Borderline",
    rcsi_categories_low = "No to Low",
    rcsi_categories_medium = "Medium",
    rcsi_categories_high = "High",
    hhs_categories_none = "None",
    hhs_categories_little = "No or Little",
    hhs_categories_moderate = "Moderate",
    hhs_categories_severe = "Severe",
    hhs_categories_very_severe = "Very Severe"
  )
df_with_fcm_1 %>%
  dplyr::select(uuid, fc_cell, fc_phase) %>%
  head(20)
```

    ##                                        uuid fc_cell   fc_phase
    ## 1  eaf540cd-32bd-41474b-b4beb5-d62fc987e45a      31 Phase 2 FC
    ## 2  89e706c3-53d8-4a4049-898586-4926085db71e      32 Phase 2 FC
    ## 3  afd921c6-e54a-4c4740-919c93-87f59bd0e63a      33 Phase 3 FC
    ## 4  d8b05f39-ba85-494c4d-808c84-9dc57823a4f1      31 Phase 2 FC
    ## 5  d6b42f9e-c209-4c4541-808a81-86bea53df142      16 Phase 2 FC
    ## 6  f1b9ec67-20db-47404d-a3ada0-1a37e5c49d02      33 Phase 3 FC
    ## 7  95ea286d-ae86-47404a-828487-feba6d1503c9      31 Phase 2 FC
    ## 8  85b4a96f-cea2-4f4b48-9d929f-5d76892f31b0      36 Phase 2 FC
    ## 9  ef13a764-0af7-4f494c-838b88-6cb31a50842e      33 Phase 3 FC
    ## 10 1a69e87b-ec61-4e4a40-8f868a-fe24c6a705bd      18 Phase 2 FC
    ## 11 5613d0fe-34dc-474c43-b4b0bd-36a4c8edf902      16 Phase 2 FC
    ## 12 091aef7d-2b31-4f4741-a5a8af-36e8f1bd075a      23 Phase 3 FC
    ## 13 e21a34f5-1a46-42404b-b7b6be-7bc9286d0f13      32 Phase 2 FC
    ## 14 42dc8573-e2d0-43484b-aaada2-c37ef865d041      16 Phase 2 FC
    ## 15 3a180db5-d126-4d4b49-808d88-b3e5c71d908f      33 Phase 3 FC
    ## 16 789a632b-53da-4c4f40-a0a1ad-f53ca2e9074b      31 Phase 2 FC
    ## 17 cd41675b-eb48-444e4f-b8b7b3-1e493cb02f5a      31 Phase 2 FC
    ## 18 f741c29d-b7c5-424a4d-94999c-6018bac9274e      16 Phase 2 FC
    ## 19 2516eba7-789c-4c4b41-afa0ad-f0a7365bd81c      33 Phase 3 FC
    ## 20 c7896215-b36f-40444c-aaa2af-fa4d37c6502e      44 Phase 4 FC

### Example:: Add Food Consumption Matrix (FCM) using HDDS, RCSI, and HHS

**Notice that these functions are also pipable**

``` r
df_with_fcm_2 <- df_with_hdds %>%
  add_fcm_phase(
    hdds_column_name = "fsl_hdds_cat",
    rcsi_column_name = "fsl_rcsi_cat",
    hhs_column_name = "fsl_hhs_cat_ipc",
    hdds_categories_low = "Low",
    hdds_categories_medium = "Medium",
    hdds_categories_high = "High",
    rcsi_categories_low = "No to Low",
    rcsi_categories_medium = "Medium",
    rcsi_categories_high = "High",
    hhs_categories_none = "None",
    hhs_categories_little = "No or Little",
    hhs_categories_moderate = "Moderate",
    hhs_categories_severe = "Severe",
    hhs_categories_very_severe = "Very Severe"
  )
df_with_fcm_2 %>%
  dplyr::select(uuid, fc_cell, fc_phase) %>%
  head(20)
```

    ##                                        uuid fc_cell   fc_phase
    ## 1  eaf540cd-32bd-41474b-b4beb5-d62fc987e45a      31 Phase 2 FC
    ## 2  89e706c3-53d8-4a4049-898586-4926085db71e      32 Phase 2 FC
    ## 3  afd921c6-e54a-4c4740-919c93-87f59bd0e63a      33 Phase 3 FC
    ## 4  d8b05f39-ba85-494c4d-808c84-9dc57823a4f1      31 Phase 2 FC
    ## 5  d6b42f9e-c209-4c4541-808a81-86bea53df142      16 Phase 2 FC
    ## 6  f1b9ec67-20db-47404d-a3ada0-1a37e5c49d02      33 Phase 3 FC
    ## 7  95ea286d-ae86-47404a-828487-feba6d1503c9      31 Phase 2 FC
    ## 8  85b4a96f-cea2-4f4b48-9d929f-5d76892f31b0      36 Phase 2 FC
    ## 9  ef13a764-0af7-4f494c-838b88-6cb31a50842e      33 Phase 3 FC
    ## 10 1a69e87b-ec61-4e4a40-8f868a-fe24c6a705bd      18 Phase 2 FC
    ## 11 5613d0fe-34dc-474c43-b4b0bd-36a4c8edf902      16 Phase 2 FC
    ## 12 091aef7d-2b31-4f4741-a5a8af-36e8f1bd075a      23 Phase 3 FC
    ## 13 e21a34f5-1a46-42404b-b7b6be-7bc9286d0f13      32 Phase 2 FC
    ## 14 42dc8573-e2d0-43484b-aaada2-c37ef865d041      16 Phase 2 FC
    ## 15 3a180db5-d126-4d4b49-808d88-b3e5c71d908f      33 Phase 3 FC
    ## 16 789a632b-53da-4c4f40-a0a1ad-f53ca2e9074b      31 Phase 2 FC
    ## 17 cd41675b-eb48-444e4f-b8b7b3-1e493cb02f5a      31 Phase 2 FC
    ## 18 f741c29d-b7c5-424a4d-94999c-6018bac9274e      16 Phase 2 FC
    ## 19 2516eba7-789c-4c4b41-afa0ad-f0a7365bd81c      33 Phase 3 FC
    ## 20 c7896215-b36f-40444c-aaa2af-fa4d37c6502e      44 Phase 4 FC

### Example:: Add Food Consumption Matrix (FCM) using FCS and HHS

**Notice that these functions are also pipable**

``` r
df_with_fcm_3 <- df_with_hdds %>%
  add_fcm_phase(
    fcs_column_name = "fsl_fcs_cat",
    hhs_column_name = "fsl_hhs_cat_ipc",
    fcs_categories_acceptable = "Acceptable",
    fcs_categories_poor = "Poor",
    fcs_categories_borderline = "Borderline",
    hhs_categories_none = "None",
    hhs_categories_little = "No or Little",
    hhs_categories_moderate = "Moderate",
    hhs_categories_severe = "Severe",
    hhs_categories_very_severe = "Very Severe"
  )
df_with_fcm_3 %>%
  dplyr::select(uuid, fc_cell, fc_phase) %>%
  head(20)
```

    ##                                        uuid fc_cell   fc_phase
    ## 1  eaf540cd-32bd-41474b-b4beb5-d62fc987e45a      31 Phase 2 FC
    ## 2  89e706c3-53d8-4a4049-898586-4926085db71e      32 Phase 2 FC
    ## 3  afd921c6-e54a-4c4740-919c93-87f59bd0e63a      33 Phase 3 FC
    ## 4  d8b05f39-ba85-494c4d-808c84-9dc57823a4f1      31 Phase 2 FC
    ## 5  d6b42f9e-c209-4c4541-808a81-86bea53df142      16 Phase 2 FC
    ## 6  f1b9ec67-20db-47404d-a3ada0-1a37e5c49d02      33 Phase 3 FC
    ## 7  95ea286d-ae86-47404a-828487-feba6d1503c9      31 Phase 2 FC
    ## 8  85b4a96f-cea2-4f4b48-9d929f-5d76892f31b0      36 Phase 2 FC
    ## 9  ef13a764-0af7-4f494c-838b88-6cb31a50842e      33 Phase 3 FC
    ## 10 1a69e87b-ec61-4e4a40-8f868a-fe24c6a705bd      18 Phase 2 FC
    ## 11 5613d0fe-34dc-474c43-b4b0bd-36a4c8edf902      16 Phase 2 FC
    ## 12 091aef7d-2b31-4f4741-a5a8af-36e8f1bd075a      23 Phase 3 FC
    ## 13 e21a34f5-1a46-42404b-b7b6be-7bc9286d0f13      32 Phase 2 FC
    ## 14 42dc8573-e2d0-43484b-aaada2-c37ef865d041      16 Phase 2 FC
    ## 15 3a180db5-d126-4d4b49-808d88-b3e5c71d908f      33 Phase 3 FC
    ## 16 789a632b-53da-4c4f40-a0a1ad-f53ca2e9074b      31 Phase 2 FC
    ## 17 cd41675b-eb48-444e4f-b8b7b3-1e493cb02f5a      31 Phase 2 FC
    ## 18 f741c29d-b7c5-424a4d-94999c-6018bac9274e      16 Phase 2 FC
    ## 19 2516eba7-789c-4c4b41-afa0ad-f0a7365bd81c      33 Phase 3 FC
    ## 20 c7896215-b36f-40444c-aaa2af-fa4d37c6502e      44 Phase 4 FC

### Example:: Add Food Consumption Matrix (FCM) using HDDS and HHS

**Notice that these functions are also pipable**

``` r
df_with_fcm_4 <- df_with_hdds %>%
  add_fcm_phase(
    hdds_column_name = "fsl_hdds_cat",
    hhs_column_name = "fsl_hhs_cat_ipc",
    hdds_categories_low = "Low",
    hdds_categories_medium = "Medium",
    hdds_categories_high = "High",
    hhs_categories_none = "None",
    hhs_categories_little = "No or Little",
    hhs_categories_moderate = "Moderate",
    hhs_categories_severe = "Severe",
    hhs_categories_very_severe = "Very Severe"
  )
df_with_fcm_4 %>%
  dplyr::select(uuid, fc_cell, fc_phase) %>%
  head(20)
```

    ##                                        uuid fc_cell   fc_phase
    ## 1  eaf540cd-32bd-41474b-b4beb5-d62fc987e45a      31 Phase 2 FC
    ## 2  89e706c3-53d8-4a4049-898586-4926085db71e      32 Phase 2 FC
    ## 3  afd921c6-e54a-4c4740-919c93-87f59bd0e63a      33 Phase 3 FC
    ## 4  d8b05f39-ba85-494c4d-808c84-9dc57823a4f1      31 Phase 2 FC
    ## 5  d6b42f9e-c209-4c4541-808a81-86bea53df142      16 Phase 2 FC
    ## 6  f1b9ec67-20db-47404d-a3ada0-1a37e5c49d02      33 Phase 3 FC
    ## 7  95ea286d-ae86-47404a-828487-feba6d1503c9      31 Phase 2 FC
    ## 8  85b4a96f-cea2-4f4b48-9d929f-5d76892f31b0      36 Phase 2 FC
    ## 9  ef13a764-0af7-4f494c-838b88-6cb31a50842e      33 Phase 3 FC
    ## 10 1a69e87b-ec61-4e4a40-8f868a-fe24c6a705bd      18 Phase 2 FC
    ## 11 5613d0fe-34dc-474c43-b4b0bd-36a4c8edf902      16 Phase 2 FC
    ## 12 091aef7d-2b31-4f4741-a5a8af-36e8f1bd075a      23 Phase 3 FC
    ## 13 e21a34f5-1a46-42404b-b7b6be-7bc9286d0f13      32 Phase 2 FC
    ## 14 42dc8573-e2d0-43484b-aaada2-c37ef865d041      16 Phase 2 FC
    ## 15 3a180db5-d126-4d4b49-808d88-b3e5c71d908f      33 Phase 3 FC
    ## 16 789a632b-53da-4c4f40-a0a1ad-f53ca2e9074b      31 Phase 2 FC
    ## 17 cd41675b-eb48-444e4f-b8b7b3-1e493cb02f5a      31 Phase 2 FC
    ## 18 f741c29d-b7c5-424a4d-94999c-6018bac9274e      16 Phase 2 FC
    ## 19 2516eba7-789c-4c4b41-afa0ad-f0a7365bd81c      33 Phase 3 FC
    ## 20 c7896215-b36f-40444c-aaa2af-fa4d37c6502e      44 Phase 4 FC

### Example:: Add FEWSNET Food Consumption-Livelihood Matrix (FCLCM)

**Notice that these functions are also pipable**

``` r
df_with_fclcm <- df_with_fcm_1 %>% ## Taken from previous Example
  add_fclcm_phase()
df_with_fclcm %>%
  dplyr::select(uuid, fclcm_phase) %>%
  head(20)
```

    ##                                        uuid  fclcm_phase
    ## 1  eaf540cd-32bd-41474b-b4beb5-d62fc987e45a Phase 3 FCLC
    ## 2  89e706c3-53d8-4a4049-898586-4926085db71e Phase 3 FCLC
    ## 3  afd921c6-e54a-4c4740-919c93-87f59bd0e63a Phase 4 FCLC
    ## 4  d8b05f39-ba85-494c4d-808c84-9dc57823a4f1 Phase 3 FCLC
    ## 5  d6b42f9e-c209-4c4541-808a81-86bea53df142 Phase 3 FCLC
    ## 6  f1b9ec67-20db-47404d-a3ada0-1a37e5c49d02 Phase 4 FCLC
    ## 7  95ea286d-ae86-47404a-828487-feba6d1503c9 Phase 3 FCLC
    ## 8  85b4a96f-cea2-4f4b48-9d929f-5d76892f31b0 Phase 3 FCLC
    ## 9  ef13a764-0af7-4f494c-838b88-6cb31a50842e Phase 4 FCLC
    ## 10 1a69e87b-ec61-4e4a40-8f868a-fe24c6a705bd Phase 3 FCLC
    ## 11 5613d0fe-34dc-474c43-b4b0bd-36a4c8edf902 Phase 3 FCLC
    ## 12 091aef7d-2b31-4f4741-a5a8af-36e8f1bd075a Phase 3 FCLC
    ## 13 e21a34f5-1a46-42404b-b7b6be-7bc9286d0f13 Phase 3 FCLC
    ## 14 42dc8573-e2d0-43484b-aaada2-c37ef865d041 Phase 3 FCLC
    ## 15 3a180db5-d126-4d4b49-808d88-b3e5c71d908f Phase 4 FCLC
    ## 16 789a632b-53da-4c4f40-a0a1ad-f53ca2e9074b Phase 3 FCLC
    ## 17 cd41675b-eb48-444e4f-b8b7b3-1e493cb02f5a Phase 3 FCLC
    ## 18 f741c29d-b7c5-424a4d-94999c-6018bac9274e Phase 3 FCLC
    ## 19 2516eba7-789c-4c4b41-afa0ad-f0a7365bd81c Phase 4 FCLC
    ## 20 c7896215-b36f-40444c-aaa2af-fa4d37c6502e Phase 4 FCLC

## Code of Conduct

Please note that the addindicators project is released with a
[Contributor Code of
Conduct](https://impact-initiatives.github.io/impactR4PHU/CODE_OF_CONDUCT.html).
By contributing to this project, you agree to abide by its terms.
